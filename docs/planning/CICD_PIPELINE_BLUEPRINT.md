# MTGTools CI/CD Pipeline Blueprint

*Generated: August 5, 2025*  
*DevOps Engineer: Claude Code*  
*For: Guillaume Bordes & MTGTools Development Team*

## Overview

This blueprint provides a comprehensive CI/CD strategy for MTGTools, designed to scale from a single static site to a multi-service platform supporting 10,000+ concurrent users with zero-downtime deployments.

---

## 1. PIPELINE ARCHITECTURE

### 1.1 Current State vs Target State

**Current Pipeline:**
```yaml
Trigger: Push to main
Steps:
  1. Checkout code
  2. Build static site
  3. Deploy to GitHub Pages
Limitations:
  - Single environment
  - No testing
  - No rollback capability
  - No monitoring
```

**Target Pipeline:**
```yaml
Trigger: Multiple (push, PR, schedule)
Stages:
  1. Quality Gates (lint, test, security)
  2. Build & Package (Docker images)
  3. Deploy Staging (automated)
  4. Integration Tests (E2E)
  5. Deploy Production (approved)
  6. Monitoring & Validation
Capabilities:
  - Multi-environment
  - Comprehensive testing
  - Automated rollback
  - Full observability
```

### 1.2 Repository Strategy

**Monorepo Structure:**
```
mtgtools/
├── apps/
│   ├── web/                 # Next.js frontend
│   ├── api/                 # Node.js API services
│   ├── mtgo-pipeline/       # MTGO data processing
│   └── discord-bot/         # Discord integration
├── packages/
│   ├── shared/              # Shared utilities
│   ├── ui/                  # Design system
│   └── database/            # Database schemas
├── infrastructure/
│   ├── kubernetes/          # K8s manifests
│   ├── terraform/           # Infrastructure as Code
│   └── monitoring/          # Observability config
└── .github/
    └── workflows/           # CI/CD pipelines
```

---

## 2. GITHUB ACTIONS WORKFLOWS

### 2.1 Main CI Pipeline

**File: `.github/workflows/ci.yml`**

```yaml
name: CI Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 2 * * *'  # Nightly builds

env:
  NODE_VERSION: '20'
  DOCKER_REGISTRY: ghcr.io
  TURBO_TOKEN: ${{ secrets.TURBO_TOKEN }}
  TURBO_TEAM: mtgtools

jobs:
  # Quality Gates - Run in parallel
  quality:
    name: Code Quality
    runs-on: ubuntu-latest
    strategy:
      matrix:
        check: [lint, typecheck, test, security]
    
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'pnpm'
      
      - name: Install pnpm
        uses: pnpm/action-setup@v2
        with:
          version: 8
      
      - name: Install dependencies
        run: pnpm install --frozen-lockfile
      
      - name: Run ${{ matrix.check }}
        run: |
          case "${{ matrix.check }}" in
            lint)
              pnpm turbo lint
              ;;
            typecheck)
              pnpm turbo typecheck
              ;;
            test)
              pnpm turbo test:ci
              ;;
            security)
              pnpm audit --audit-level=moderate
              npx snyk test
              ;;
          esac
      
      - name: Upload coverage
        if: matrix.check == 'test'
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
  
  # Build Docker images
  build:
    name: Build Images
    runs-on: ubuntu-latest
    needs: quality
    strategy:
      matrix:
        app: [web, api, mtgo-pipeline, discord-bot]
    
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      
      - name: Login to Container Registry
        uses: docker/login-action@v3
        with:
          registry: ${{ env.DOCKER_REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      
      - name: Extract metadata
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.DOCKER_REGISTRY }}/mtgtools/${{ matrix.app }}
          tags: |
            type=ref,event=branch
            type=ref,event=pr
            type=sha,prefix={{branch}}-
            type=raw,value=latest,enable={{is_default_branch}}
      
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          file: ./apps/${{ matrix.app }}/Dockerfile
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          cache-from: type=gha
          cache-to: type=gha,mode=max
          platforms: linux/amd64,linux/arm64
```

### 2.2 Deployment Pipeline

**File: `.github/workflows/deploy.yml`**

```yaml
name: Deploy Pipeline

on:
  workflow_run:
    workflows: ["CI Pipeline"]
    types: [completed]
    branches: [main, develop]
  workflow_dispatch:
    inputs:
      environment:
        description: 'Environment to deploy to'
        required: true
        default: 'staging'
        type: choice
        options:
          - staging
          - production

jobs:
  deploy-staging:
    name: Deploy to Staging
    runs-on: ubuntu-latest
    if: |
      github.event.workflow_run.conclusion == 'success' &&
      (github.event.workflow_run.head_branch == 'develop' ||
       github.event.workflow_run.head_branch == 'main')
    environment:
      name: staging
      url: https://staging.mtgtools.com
    
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup kubectl
        uses: azure/setup-kubectl@v3
        with:
          version: 'v1.28.0'
      
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      
      - name: Update kubeconfig
        run: |
          aws eks update-kubeconfig --region us-east-1 --name mtgtools-staging
      
      - name: Deploy to staging
        run: |
          # Update image tags in manifests
          export IMAGE_TAG="${{ github.event.workflow_run.head_sha }}"
          
          # Deploy using Kustomize
          kubectl apply -k infrastructure/kubernetes/overlays/staging
          
          # Wait for deployment to complete
          kubectl rollout status deployment/web-app -n mtgtools-staging --timeout=300s
          kubectl rollout status deployment/api-service -n mtgtools-staging --timeout=300s
      
      - name: Run smoke tests
        run: |
          # Wait for services to be ready
          sleep 30
          
          # Basic health checks
          curl -f https://staging.mtgtools.com/health || exit 1
          curl -f https://api-staging.mtgtools.com/health || exit 1
      
      - name: Update deployment status
        if: always()
        uses: actions/github-script@v7
        with:
          script: |
            const { context } = require('@actions/github');
            
            await github.rest.deployments.createDeploymentStatus({
              owner: context.repo.owner,
              repo: context.repo.repo,
              deployment_id: context.payload.deployment.id,
              state: '${{ job.status }}' === 'success' ? 'success' : 'failure',
              target_url: 'https://staging.mtgtools.com',
              description: '${{ job.status }}' === 'success' ? 
                'Staging deployment successful' : 'Staging deployment failed'
            });
  
  deploy-production:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: deploy-staging
    if: |
      github.event.workflow_run.head_branch == 'main' ||
      (github.event_name == 'workflow_dispatch' && 
       github.event.inputs.environment == 'production')
    environment:
      name: production
      url: https://mtgtools.com
    
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Production deployment
        run: |
          echo "Deploying to production with blue-green strategy..."
          
          # Blue-green deployment logic
          CURRENT_COLOR=$(kubectl get service web-app -o jsonpath='{.spec.selector.color}')
          NEW_COLOR=$([ "$CURRENT_COLOR" = "blue" ] && echo "green" || echo "blue")
          
          echo "Current: $CURRENT_COLOR, Deploying: $NEW_COLOR"
          
          # Deploy new version
          kubectl patch deployment web-app-$NEW_COLOR -p \
            '{"spec":{"template":{"spec":{"containers":[{"name":"web","image":"ghcr.io/mtgtools/web:${{ github.event.workflow_run.head_sha }}"}]}}}}'
          
          # Wait for deployment
          kubectl rollout status deployment/web-app-$NEW_COLOR --timeout=600s
          
          # Health check
          kubectl port-forward service/web-app-$NEW_COLOR 8080:80 &
          sleep 10
          curl -f http://localhost:8080/health || exit 1
          
          # Switch traffic
          kubectl patch service web-app -p \
            '{"spec":{"selector":{"color":"'$NEW_COLOR'"}}}'
          
          echo "Production deployment completed successfully"
```

### 2.3 Release Pipeline

**File: `.github/workflows/release.yml`**

```yaml
name: Release Pipeline

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  release:
    name: Create Release
    runs-on: ubuntu-latest
    permissions:
      contents: write
      packages: write
    
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      
      - name: Generate changelog
        id: changelog
        run: |
          # Generate changelog since last tag
          LAST_TAG=$(git describe --tags --abbrev=0 HEAD~1 2>/dev/null || echo "")
          if [ -z "$LAST_TAG" ]; then
            CHANGELOG=$(git log --pretty=format:"- %s (%h)" --no-merges)
          else
            CHANGELOG=$(git log $LAST_TAG..HEAD --pretty=format:"- %s (%h)" --no-merges)
          fi
          
          echo "changelog<<EOF" >> $GITHUB_OUTPUT
          echo "$CHANGELOG" >> $GITHUB_OUTPUT
          echo "EOF" >> $GITHUB_OUTPUT
      
      - name: Create GitHub Release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          body: |
            ## Changes in this release
            
            ${{ steps.changelog.outputs.changelog }}
            
            ## Docker Images
            
            ```bash
            # Pull latest images
            docker pull ghcr.io/mtgtools/web:${{ github.ref_name }}
            docker pull ghcr.io/mtgtools/api:${{ github.ref_name }}
            docker pull ghcr.io/mtgtools/mtgo-pipeline:${{ github.ref_name }}
            ```
          draft: false
          prerelease: false
```

---

## 3. ENVIRONMENT STRATEGY

### 3.1 Environment Configuration

**Development Environment:**
```yaml
Trigger: Every push to feature branches
Infrastructure: Shared Kubernetes namespace
Database: Ephemeral PostgreSQL containers
External Services: Mock/stub implementations
Testing: Unit tests + integration tests
Lifecycle: Automatic cleanup after 7 days
```

**Staging Environment:**
```yaml
Trigger: Push to develop or main branch
Infrastructure: Production-like EKS cluster
Database: Dedicated RDS instance (smaller)
External Services: Staging versions or mocks
Testing: Full E2E test suite
Data: Synthetic data + sanitized production subset
```

**Production Environment:**
```yaml
Trigger: Manual approval after staging success
Infrastructure: Multi-AZ EKS with auto-scaling
Database: Production RDS with read replicas
External Services: Live integrations
Testing: Smoke tests + canary deployments
Monitoring: Full observability stack
```

### 3.2 Configuration Management

**Environment Variables:**
```yaml
# Base configuration (all environments)
DATABASE_URL: "postgresql://..."
REDIS_URL: "redis://..."
LOG_LEVEL: "info"

# Environment-specific overrides
staging:
  API_BASE_URL: "https://api-staging.mtgtools.com"
  FEATURE_FLAGS: "new-ui=true,beta-features=true"
  
production:
  API_BASE_URL: "https://api.mtgtools.com"
  FEATURE_FLAGS: "new-ui=false,beta-features=false"
```

---

## 4. TESTING STRATEGY

### 4.1 Test Pyramid

```
        E2E Tests (5%)
       /               \
      /   Integration    \
     /    Tests (25%)    \
    /                     \
   /     Unit Tests       \
  /        (70%)          \
 /_________________________\
```

**Unit Tests (Jest/Vitest):**
```yaml
Scope: Individual functions and components
Location: Colocated with source code
Coverage Target: >80%
Execution: Every commit

Example:
# apps/api/src/services/__tests__/user.test.ts
# apps/web/src/components/__tests__/Button.test.tsx
```

**Integration Tests (Testcontainers):**
```yaml
Scope: API endpoints with real database
Location: apps/api/tests/integration/
Database: PostgreSQL testcontainer
Execution: CI pipeline only

Example:
# Test user registration with real database
# Test MTGO data ingestion pipeline
```

**E2E Tests (Playwright):**
```yaml
Scope: Critical user journeys
Location: tests/e2e/
Browser: Chrome, Firefox, Safari
Execution: Staging deployment

Scenarios:
- User registration and login
- Tournament data viewing
- Premium subscription flow
```

### 4.2 Performance Testing

**Load Testing (K6):**
```javascript
// tests/performance/api-load.js
import http from 'k6/http';
import { check } from 'k6';

export let options = {
  stages: [
    { duration: '5m', target: 100 },   // Ramp up
    { duration: '10m', target: 1000 }, // Load test
    { duration: '5m', target: 0 },     // Ramp down
  ],
  thresholds: {
    http_req_duration: ['p(95)<100'], // 95% < 100ms
    http_req_failed: ['rate<0.01'],   // Error rate < 1%
  },
};

export default function() {
  let response = http.get('https://api.mtgtools.com/tournaments');
  check(response, {
    'status is 200': (r) => r.status === 200,
    'response time < 100ms': (r) => r.timings.duration < 100,
  });
}
```

---

## 5. DEPLOYMENT STRATEGIES

### 5.1 Blue-Green Deployment

**Implementation:**
```yaml
Architecture:
  - Two identical production environments (blue/green)
  - Load balancer switches traffic instantly
  - Zero downtime deployments
  - Instant rollback capability

Process:
  1. Deploy new version to inactive environment
  2. Run health checks and smoke tests
  3. Switch load balancer to new environment
  4. Monitor for issues
  5. Keep old environment for quick rollback
```

**Kubernetes Blue-Green:**
```yaml
# Service definition
apiVersion: v1
kind: Service
metadata:
  name: web-app
spec:
  selector:
    app: web-app
    color: blue  # Switch between blue/green
  ports:
    - port: 80
      targetPort: 3000

---
# Blue deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
      color: blue
  template:
    metadata:
      labels:
        app: web-app
        color: blue
    spec:
      containers:
      - name: web
        image: ghcr.io/mtgtools/web:stable
        ports:
        - containerPort: 3000
```

### 5.2 Canary Deployment

**For High-Risk Changes:**
```yaml
Strategy:
  - Deploy new version to small subset of users (5%)
  - Monitor key metrics (error rate, latency)
  - Gradually increase traffic if metrics are good
  - Automatic rollback if metrics degrade

Implementation:
  - Istio service mesh for traffic splitting
  - Prometheus metrics for decision making
  - Automated promotion/rollback based on SLIs
```

---

## 6. MONITORING & OBSERVABILITY

### 6.1 Pipeline Monitoring

**GitHub Actions Metrics:**
```yaml
Dashboard Metrics:
  - Build success rate (target: >95%)
  - Build duration (target: <10 minutes)
  - Deployment frequency (target: >1/day)
  - Lead time for changes (target: <4 hours)
  - Mean time to recovery (target: <30 minutes)
```

**Deployment Health Checks:**
```yaml
Checks:
  - HTTP health endpoints
  - Database connectivity
  - External service availability
  - Memory and CPU usage
  - Application-specific metrics

Actions:
  - Automatic rollback on failure
  - Slack/Discord notifications
  - PagerDuty alerts for production
```

### 6.2 Application Monitoring

**Key Metrics:**
```yaml
Golden Signals:
  - Latency: API response times
  - Traffic: Requests per second
  - Errors: Error rate by endpoint
  - Saturation: Resource utilization

Business Metrics:
  - User registration rate
  - Tournament data ingestion rate
  - API usage by endpoint
  - Feature adoption rates
```

---

## 7. SECURITY & COMPLIANCE

### 7.1 Pipeline Security

**Secret Management:**
```yaml
GitHub Secrets:
  - AWS_ACCESS_KEY_ID (encrypted)
  - AWS_SECRET_ACCESS_KEY (encrypted)
  - DOCKER_REGISTRY_TOKEN (encrypted)
  - DATABASE_PASSWORD (encrypted)

Rotation Policy:
  - Quarterly rotation for long-lived secrets
  - Immediate rotation on compromise
  - Audit trail for all secret access
```

**Container Security:**
```yaml
Scanning:
  - Base image vulnerability scanning
  - Dependency vulnerability scanning
  - SAST (Static Application Security Testing)
  - License compliance checking

Policies:
  - No high/critical vulnerabilities in production
  - Regular base image updates
  - Minimal container privileges
```

### 7.2 Compliance Automation

**GDPR Compliance:**
```yaml
Data Protection:
  - Automated data retention policies
  - User data deletion workflows
  - Consent management validation
  - Audit log generation

Monitoring:
  - Data processing activity logs
  - Cross-border data transfer tracking
  - User consent status monitoring
```

---

## 8. DISASTER RECOVERY

### 8.1 Backup Strategy

**Database Backups:**
```yaml
RDS Automated Backups:
  - Point-in-time recovery (35 days)
  - Cross-region backup replication
  - Encrypted backups
  - Automated restore testing

Application Data:
  - S3 versioning for static assets
  - Git repository backups
  - Configuration backup automation
```

### 8.2 Recovery Procedures

**RTO/RPO Targets:**
```yaml
Recovery Time Objective (RTO): 15 minutes
Recovery Point Objective (RPO): 5 minutes

Procedures:
  - Automated failover to standby region
  - Database point-in-time recovery
  - Application rollback procedures
  - Communication templates
```

---

## 9. IMPLEMENTATION TIMELINE

### 9.1 Phase 1: Pipeline Foundation (Week 1-2)

**Week 1:**
```yaml
Tasks:
  - Setup GitHub Actions workflows
  - Create Dockerfile for each service
  - Implement basic CI pipeline
  - Setup container registry

Deliverables:
  - Working CI pipeline
  - Docker images building
  - Basic test execution
```

**Week 2:**
```yaml
Tasks:
  - Setup staging environment
  - Implement deployment pipeline
  - Add quality gates
  - Create monitoring dashboards

Deliverables:
  - Staging deployments working
  - Quality gates enforced
  - Basic monitoring in place
```

### 9.2 Phase 2: Advanced Features (Week 3-4)

**Week 3:**
```yaml
Tasks:
  - Implement blue-green deployment
  - Add performance testing
  - Setup production environment
  - Create runbooks

Deliverables:
  - Zero-downtime deployments
  - Performance benchmarks
  - Production-ready infrastructure
```

**Week 4:**
```yaml
Tasks:
  - Add security scanning
  - Implement disaster recovery
  - Create team training materials
  - Optimize pipeline performance

Deliverables:
  - Security-hardened pipeline
  - Disaster recovery procedures
  - Team documentation
```

---

## 10. TEAM ADOPTION

### 10.1 Developer Experience

**Local Development:**
```yaml
Tools:
  - Docker Compose for local services
  - Pre-commit hooks for quality
  - VS Code dev containers
  - Automated database migrations

Workflow:
  1. Clone repository
  2. Run `make dev-setup`
  3. Start coding with hot reload
  4. Automated testing on save
```

**Documentation:**
```yaml
Required Docs:
  - Pipeline architecture overview
  - Deployment procedures
  - Troubleshooting guide
  - Security best practices
  - Incident response procedures
```

### 10.2 Training Plan

**Week 1: Pipeline Overview**
- CI/CD concepts and benefits
- MTGTools pipeline walkthrough
- Hands-on workshop

**Week 2: Deployment Procedures**
- Environment management
- Rollback procedures
- Monitoring and alerting

**Week 3: Advanced Topics**
- Security best practices
- Performance optimization
- Disaster recovery

---

## CONCLUSION

This CI/CD blueprint provides MTGTools with:

1. **Automated Quality**: Every change is tested and validated
2. **Zero-Downtime Deployments**: Blue-green strategy ensures availability
3. **Scalable Architecture**: Supports growth from 100 to 10,000+ users
4. **Security-First**: Built-in security scanning and compliance
5. **Developer Productivity**: Streamlined development workflow

**Key Success Metrics:**
- Deployment frequency: >1 per day
- Lead time for changes: <4 hours
- Change failure rate: <5%
- Mean time to recovery: <30 minutes

The pipeline evolves with the platform, starting simple and adding sophistication as the team and user base grow.

---

*Next Document: [MONITORING_STRATEGY.md](./MONITORING_STRATEGY.md)*