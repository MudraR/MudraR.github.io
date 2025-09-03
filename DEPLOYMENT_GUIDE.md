# Multi-Site GitHub Pages Setup

This repository now supports deploying multiple applications to different sub-paths on GitHub Pages:

## Site Structure

- **Root (`/`)**: Landing page with navigation to all projects
- **Blog (`/blog/`)**: Jekyll blog using Chirpy theme 
- **ICD10 Search (`/icd10-search/`)**: Static ICD-10 code search application

## Configuration Changes

### Jekyll Configuration (`_config.yml`)
- Set `baseurl: "/blog"` to deploy Jekyll to `/blog` sub-path
- All Jekyll-generated links will be relative to `/blog/`

### GitHub Actions Workflow (`.github/workflows/deploy-app.yml`)
The unified deployment workflow:
1. Builds Jekyll blog to `_site/blog/` directory
2. Copies ICD10 search app to `_site/icd10-search/`
3. Creates a root index page for navigation
4. Creates a custom 404 page
5. Deploys everything to GitHub Pages

### 404 Error Handling
- **Jekyll Blog**: Custom 404.html page with styling consistent with blog theme
- **Root Site**: Standalone 404.html with modern styling and navigation back to home

### File Structure
```
├── blog/                    # Jekyll blog (accessible at /blog/)
│   ├── posts/
│   ├── categories/
│   ├── tags/
│   └── 404.html            # Blog-specific 404 page
├── icd10-search/           # ICD10 search app (accessible at /icd10-search/)
│   └── index.html
├── index.html              # Root landing page
└── 404.html                # Site-wide 404 page
```

## Benefits

1. **Independent Deployment**: Each application can be updated independently
2. **No Conflicts**: Jekyll build doesn't override other static sites
3. **Proper Routing**: Each app has its own sub-path and maintains correct internal links
4. **Professional Navigation**: Root landing page provides clean access to all projects
5. **Error Handling**: Proper 404 pages at both root and blog levels

## Accessing Sites

- **Landing Page**: `https://mudrar.github.io/`
- **Blog**: `https://mudrar.github.io/blog/`
- **ICD10 Search**: `https://mudrar.github.io/icd10-search/`

## Deployment Triggers

The GitHub Actions workflow triggers on:
- Pushes to `main` branch
- Manual workflow dispatch
- Excludes changes to `.gitignore`, `README.md`, and `LICENSE`

This setup ensures both applications can coexist without conflicts while maintaining clean, navigable URLs.