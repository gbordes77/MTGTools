# MTGTools API Documentation Standards

*Version 1.0 - August 2025*
*Ensuring every API is self-documenting and developer-friendly*

## 🎯 API Documentation Philosophy

> "An API without documentation is like a deck without a sideboard guide - technically playable but missing critical information for success."

## 📐 OpenAPI Specification Standards

### 1. Base Structure

```yaml
openapi: 3.1.0
info:
  title: MTGTools {Service} API
  version: 1.0.0
  description: |
    ## Overview
    Brief description of what this API does and its role in MTGTools ecosystem.
    
    ## Authentication
    All endpoints require API key authentication via `X-API-Key` header.
    
    ## Rate Limiting
    - Anonymous: 100 requests/hour
    - Authenticated: 1000 requests/hour
    - Burst: 10 requests/second
    
    ## Status Page
    https://status.mtgtools.com
    
  contact:
    name: MTGTools API Support
    email: api@mtgtools.com
    url: https://discord.gg/mtgtools
  
  license:
    name: MIT
    url: https://opensource.org/licenses/MIT

servers:
  - url: https://api.mtgtools.com/v1
    description: Production
  - url: https://staging-api.mtgtools.com/v1
    description: Staging
  - url: http://localhost:3000/v1
    description: Local Development

tags:
  - name: Metagame
    description: Metagame analysis and statistics
  - name: Decks
    description: Deck management and analysis
  - name: Tournaments
    description: Tournament data and results
```

### 2. Endpoint Documentation

```yaml
paths:
  /metagame/current:
    get:
      operationId: getCurrentMetagame
      summary: Get current metagame breakdown
      description: |
        Returns the current metagame distribution for the specified format.
        Data is cached for 1 hour and updated after each major event.
        
        **Use Cases:**
        - Display metagame pie chart
        - Calculate deck positioning
        - Track meta shifts over time
        
      tags:
        - Metagame
      
      parameters:
        - name: format
          in: query
          required: true
          description: MTG format to analyze
          schema:
            type: string
            enum: [modern, legacy, pioneer, standard, pauper]
          example: modern
        
        - name: timeframe
          in: query
          required: false
          description: Time period for analysis
          schema:
            type: string
            enum: [24h, 7d, 14d, 30d]
            default: 7d
          example: 7d
      
      responses:
        200:
          description: Successful metagame data retrieval
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/MetagameResponse'
              examples:
                modern:
                  summary: Modern metagame example
                  value:
                    format: modern
                    lastUpdated: "2025-08-05T12:00:00Z"
                    sampleSize: 1847
                    archetypes:
                      - name: "Rakdos Scam"
                        percentage: 14.3
                        count: 264
                        performance:
                          winRate: 52.1
                          topCuts: 18
        
        400:
          $ref: '#/components/responses/BadRequest'
        
        429:
          $ref: '#/components/responses/RateLimited'
```

### 3. Schema Documentation

```yaml
components:
  schemas:
    MetagameResponse:
      type: object
      required:
        - format
        - lastUpdated
        - sampleSize
        - archetypes
      properties:
        format:
          type: string
          description: MTG format analyzed
          example: modern
        
        lastUpdated:
          type: string
          format: date-time
          description: When this data was last refreshed
          example: "2025-08-05T12:00:00Z"
        
        sampleSize:
          type: integer
          minimum: 0
          description: Number of decks analyzed
          example: 1847
        
        archetypes:
          type: array
          description: List of archetypes in the metagame
          items:
            $ref: '#/components/schemas/Archetype'
    
    Archetype:
      type: object
      required:
        - name
        - percentage
        - count
      properties:
        name:
          type: string
          description: Canonical archetype name
          example: "Rakdos Scam"
        
        percentage:
          type: number
          format: float
          minimum: 0
          maximum: 100
          description: Percentage of metagame
          example: 14.3
        
        count:
          type: integer
          minimum: 0
          description: Number of decks
          example: 264
        
        performance:
          $ref: '#/components/schemas/Performance'
```

## 📝 Documentation Requirements by Endpoint Type

### 1. GET Endpoints (Data Retrieval)

Must document:
- [ ] Caching behavior and TTL
- [ ] Pagination parameters if applicable
- [ ] Sorting options
- [ ] Filter parameters with examples
- [ ] Response size considerations

### 2. POST Endpoints (Data Creation)

Must document:
- [ ] Required vs optional fields
- [ ] Validation rules
- [ ] Idempotency keys if supported
- [ ] Rate limits for creation
- [ ] Success response structure

### 3. PUT/PATCH Endpoints (Updates)

Must document:
- [ ] Partial vs full updates
- [ ] Optimistic locking if used
- [ ] Field-level permissions
- [ ] Audit trail behavior
- [ ] Conflict resolution

### 4. DELETE Endpoints

Must document:
- [ ] Soft vs hard delete
- [ ] Cascading behavior
- [ ] Recovery options
- [ ] Confirmation requirements
- [ ] Side effects

## 🔍 API Examples Standards

### 1. Request Examples

```yaml
# Always provide multiple examples covering:
# - Minimal required parameters
# - Common use case
# - Advanced filtering
# - Edge cases

examples:
  minimal:
    summary: Get modern metagame with defaults
    value:
      format: modern
  
  filtered:
    summary: Get last 24h with performance data
    value:
      format: modern
      timeframe: 24h
      includePerformance: true
  
  tournament:
    summary: Get metagame for specific event
    value:
      format: legacy
      eventId: "0a7b9f42"
      minDecks: 8
```

### 2. Response Examples

```yaml
# Provide examples for:
# - Successful response with data
# - Empty results
# - Partial data scenarios
# - Error responses

examples:
  success:
    summary: Typical metagame response
    value:
      # Full response object
  
  noData:
    summary: No data available
    value:
      format: vintage
      lastUpdated: "2025-08-05T12:00:00Z"
      sampleSize: 0
      archetypes: []
      message: "Insufficient data for vintage format"
  
  error:
    summary: Invalid format error
    value:
      error:
        code: "INVALID_FORMAT"
        message: "Format 'commander' is not supported"
        validFormats: ["modern", "legacy", "pioneer", "standard", "pauper"]
```

## 🧪 Interactive Documentation

### 1. Try It Out Configuration

```javascript
// Swagger UI configuration
const swaggerOptions = {
  tryItOutEnabled: true,
  requestInterceptor: (req) => {
    // Add default API key for testing
    if (!req.headers['X-API-Key']) {
      req.headers['X-API-Key'] = 'demo-api-key';
    }
    return req;
  },
  
  // Prefill common values
  defaultModelRendering: 'model',
  defaultModelsExpandDepth: 2,
  
  // Custom theme
  theme: {
    colors: {
      primary: '#facc15', // MTGTools yellow
    }
  }
};
```

### 2. Code Generation Examples

Each endpoint should include code examples in multiple languages:

```yaml
x-code-samples:
  - lang: JavaScript
    label: fetch
    source: |
      const response = await fetch('https://api.mtgtools.com/v1/metagame/current?format=modern', {
        headers: {
          'X-API-Key': 'your-api-key'
        }
      });
      const data = await response.json();
      
  - lang: Python
    label: requests
    source: |
      import requests
      
      response = requests.get(
        'https://api.mtgtools.com/v1/metagame/current',
        params={'format': 'modern'},
        headers={'X-API-Key': 'your-api-key'}
      )
      data = response.json()
      
  - lang: cURL
    label: cURL
    source: |
      curl -X GET "https://api.mtgtools.com/v1/metagame/current?format=modern" \
        -H "X-API-Key: your-api-key"
```

## 📊 API Documentation Metrics

### What to Track

```javascript
// Documentation analytics
track('api_docs_interaction', {
  endpoint: '/metagame/current',
  action: 'try_it_out',
  success: true,
  language: 'javascript',
  timeToSuccess: 3.2
});
```

### Success Metrics
- Time to first successful API call < 5 minutes
- "Try it out" success rate > 90%
- Code sample copy rate > 50%
- Support ticket reduction > 40%

## 🔄 Versioning Strategy

### 1. Version in URL

```yaml
servers:
  - url: https://api.mtgtools.com/v1
    description: Version 1 (Current)
  - url: https://api.mtgtools.com/v2
    description: Version 2 (Beta)
```

### 2. Deprecation Notices

```yaml
paths:
  /decks/analyze:
    post:
      deprecated: true
      x-deprecation-date: "2025-12-31"
      x-sunset-date: "2026-03-31"
      x-replacement: "/analysis/deck"
      description: |
        ⚠️ **DEPRECATED**: This endpoint will be removed on March 31, 2026.
        Please migrate to `/analysis/deck` for improved functionality.
        
        Migration guide: https://docs.mtgtools.com/migrations/deck-analysis
```

## 🛡️ Security Documentation

### 1. Authentication Section

```yaml
components:
  securitySchemes:
    ApiKey:
      type: apiKey
      in: header
      name: X-API-Key
      description: |
        ## Obtaining an API Key
        1. Sign up at https://mtgtools.com/signup
        2. Navigate to Account → API Keys
        3. Generate a new key with appropriate scopes
        
        ## Key Security
        - Never commit keys to version control
        - Rotate keys every 90 days
        - Use environment variables
        
        ## Scopes
        - `read:public` - Public data access
        - `read:private` - Your private data
        - `write:decks` - Create/modify decks
        - `admin:tournaments` - Tournament management
```

### 2. Error Response Standards

```yaml
components:
  responses:
    Unauthorized:
      description: Missing or invalid API key
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            error:
              code: "UNAUTHORIZED"
              message: "Invalid API key provided"
              help: "https://docs.mtgtools.com/api/authentication"
```

## 📚 SDK Documentation Integration

### Generated SDK Docs

```typescript
/**
 * Get current metagame breakdown
 * 
 * @param format - MTG format to analyze
 * @param options - Additional query parameters
 * @returns Promise<MetagameResponse>
 * 
 * @example
 * ```typescript
 * const metagame = await mtgtools.metagame.getCurrent('modern', {
 *   timeframe: '7d',
 *   includePerformance: true
 * });
 * 
 * console.log(`Top deck: ${metagame.archetypes[0].name}`);
 * ```
 * 
 * @see {@link https://docs.mtgtools.com/api/metagame#current}
 */
async getCurrent(
  format: Format,
  options?: MetagameOptions
): Promise<MetagameResponse> {
  // Implementation
}
```

## ✅ API Documentation Checklist

Before releasing any API endpoint:

- [ ] OpenAPI spec complete and validated
- [ ] All parameters documented with examples
- [ ] Response schemas with realistic examples
- [ ] Error responses documented
- [ ] Authentication requirements clear
- [ ] Rate limits specified
- [ ] Code samples in 3+ languages
- [ ] Interactive "Try it out" tested
- [ ] Deprecation strategy defined
- [ ] Performance considerations noted
- [ ] Related endpoints linked
- [ ] Changelog entry added

---

*"A well-documented API is the foundation of a thriving developer ecosystem."*