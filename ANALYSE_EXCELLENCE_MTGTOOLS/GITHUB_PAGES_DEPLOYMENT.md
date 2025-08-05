# GitHub Pages Deployment Guide

## Overview

This document provides comprehensive instructions for deploying the MTGTools website to GitHub Pages with automated CI/CD, performance optimizations, and monitoring.

## Prerequisites

- GitHub repository with admin access
- Git installed locally
- Basic understanding of GitHub Actions

## Initial Setup

### 1. Enable GitHub Pages

1. Navigate to your repository on GitHub
2. Go to **Settings** → **Pages**
3. Under **Source**, select **GitHub Actions**
4. Save the changes

### 2. Verify Files

Ensure these files exist in your repository:

- ✅ `.nojekyll` - Bypasses Jekyll processing
- ✅ `.github/workflows/deploy-pages.yml` - Automated deployment workflow
- ✅ `index.html` - Main landing page
- ✅ `sw.js` - Service worker for offline support
- ✅ `robots.txt` - SEO configuration
- ✅ `sitemap.xml` - Site structure for search engines

## Deployment Process

### Automatic Deployment

The site automatically deploys when:

1. **Push to main branch**: Any commit to `main` triggers deployment
2. **Manual trigger**: Use Actions tab → Deploy to GitHub Pages → Run workflow

### Manual Deployment Steps

```bash
# 1. Ensure you're on main branch
git checkout main

# 2. Pull latest changes
git pull origin main

# 3. Make your changes
# Edit files as needed

# 4. Commit changes
git add .
git commit -m "Update: description of changes"

# 5. Push to trigger deployment
git push origin main
```

## Workflow Details

### Build Process

1. **Checkout code**: Retrieves latest repository content
2. **Setup Pages**: Configures GitHub Pages environment
3. **Optimize assets**: 
   - Removes unnecessary files (markdown, archives, etc.)
   - Keeps only web assets
4. **Minify HTML**: Reduces file size for faster loading
5. **Create 404 page**: Custom error page
6. **Upload artifact**: Prepares files for deployment

### Deploy Process

1. **Environment setup**: Configures production environment
2. **Deploy to Pages**: Publishes optimized site
3. **URL generation**: Creates accessible link

## Performance Features

### 1. Asset Optimization

- **HTML Minification**: Removes whitespace and comments
- **CDN Usage**: Leverages external CDNs for libraries
- **DNS Prefetching**: Speeds up external resource loading

### 2. Offline Support

The service worker (`sw.js`) provides:
- Offline page viewing
- Resource caching
- Faster subsequent loads

### 3. SEO Optimization

- Meta tags for social media
- Sitemap for search engines
- Robots.txt for crawler guidance

## Monitoring and Maintenance

### Check Deployment Status

1. Go to repository → **Actions** tab
2. Look for "Deploy to GitHub Pages" workflow
3. Green checkmark = successful deployment
4. Click on run for detailed logs

### View Live Site

After successful deployment:
- URL: `https://[username].github.io/MTGTools/`
- Or check Settings → Pages for exact URL

### Common Issues and Solutions

#### Build Fails

**Issue**: Workflow fails during build
**Solution**: 
- Check Actions logs for specific error
- Verify all file paths are correct
- Ensure no syntax errors in HTML

#### 404 Errors

**Issue**: Pages not found
**Solution**:
- Verify `.nojekyll` file exists
- Check file paths are relative
- Wait 10 minutes for CDN propagation

#### Slow Loading

**Issue**: Site loads slowly
**Solution**:
- Check browser developer tools Network tab
- Verify CDN resources are loading
- Clear browser cache

## Updates and Versioning

### Updating Content

1. Edit files locally
2. Test changes with local server
3. Commit and push to main
4. Monitor deployment status

### Cache Busting

The service worker uses versioned cache:
```javascript
const CACHE_NAME = 'mtgtools-v1';
```

To force cache refresh:
1. Update version number in `sw.js`
2. Deploy changes
3. Users get fresh content

## Security Considerations

- ✅ HTTPS enforced by GitHub Pages
- ✅ No sensitive data in public files
- ✅ Dependencies locked to specific versions
- ✅ Regular Dependabot updates configured

## Best Practices

1. **Test Locally First**
   ```bash
   python -m http.server 8000
   # Visit http://localhost:8000
   ```

2. **Use Pull Requests**
   - Create feature branches
   - Test in PR preview
   - Merge after review

3. **Monitor Performance**
   - Use PageSpeed Insights
   - Check Core Web Vitals
   - Review Analytics

## Rollback Procedure

If deployment causes issues:

1. **Immediate Rollback**:
   ```bash
   git revert HEAD
   git push origin main
   ```

2. **Specific Commit Rollback**:
   ```bash
   git revert <commit-hash>
   git push origin main
   ```

3. **Manual Rollback**:
   - Go to Actions → Select last successful run
   - Re-run deployment

## Contact and Support

For deployment issues:
1. Check GitHub Actions logs
2. Review this documentation
3. Contact: Guillaume Bordes (Project Lead)

## Next Steps

1. Enable GitHub Pages in repository settings
2. Push to main branch to trigger first deployment
3. Verify site is accessible at provided URL
4. Set up custom domain (optional)
5. Configure analytics (optional)