# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This is an al-folio academic website built with Jekyll, designed for researchers and academics to showcase their work, publications, and portfolio.

## Essential Commands

### Development Environment Setup
```bash
# Using conda environment (recommended)
conda activate website
npm install --save-dev --save-exact prettier @shopify/prettier-plugin-liquid

# Docker development (alternative)
docker compose pull
docker compose up

# Local development
bundle install
bundle exec jekyll serve
```

### Code Quality and Formatting
```bash
# Run prettier formatting check
npx prettier . --check

# Fix formatting issues
npx prettier . --write

# Run pre-commit hooks
pre-commit install
pre-commit run --all-files
```

### Building and Deployment
```bash
# Production build
export JEKYLL_ENV=production
bundle exec jekyll build

# CSS optimization (after build)
purgecss -c purgecss.config.js

# Deploy to GitHub Pages (automatic on push to main)
# Manual deployment
bin/deploy
```

## Architecture and Structure

### Core Technology Stack
- **Jekyll**: Static site generator with Ruby
- **Bootstrap**: Responsive design framework
- **Jekyll Scholar**: BibTeX integration for academic publications
- **Liquid**: Template engine for dynamic content
- **GitHub Actions**: CI/CD automation

### Project Structure
```
├── _bibliography/    # BibTeX files for publications
├── _data/           # YAML data (CV, venues, socials)
├── _includes/       # Reusable Liquid components
├── _layouts/        # Page templates (about, post, CV, distill)
├── _news/           # News/announcements
├── _pages/          # Static pages (about, publications, etc.)
├── _posts/          # Blog posts with various examples
├── _projects/       # Portfolio projects
├── _sass/           # SCSS stylesheets
├── assets/          # Static assets (css, js, images, PDFs)
└── _config.yml      # Main Jekyll configuration
```

### Key Configuration Files
- **_config.yml**: Main site configuration (URL, metadata, plugin settings, CDN libraries)
- **_bibliography/papers.bib**: Academic publications in BibTeX format
- **_data/cv.yml**: CV/resume data in structured YAML
- **.prettierrc**: Code formatting rules (150 char width, Liquid plugin)

### Collections System
The site uses Jekyll collections for organized content:
- **posts**: Blog with categories, tags, and archives
- **projects**: Portfolio with featured/regular categorization
- **news**: Announcements with scrollable display
- **bibliography**: Academic papers with Jekyll Scholar

### Plugin Dependencies
Key Jekyll plugins:
- jekyll-scholar: Academic bibliography management
- jekyll-imagemagick: Image processing and thumbnails
- jekyll-jupyter-notebook: Jupyter notebook rendering
- jekyll-diagrams: Mermaid/PlantUML diagram support
- jekyll-minifier: HTML/CSS/JS minification

### JavaScript Libraries
Managed via CDN with integrity checks:
- Bootstrap 5.3.3
- jQuery 3.7.1
- MathJax 3 for equations
- Mermaid for diagrams
- Chart.js, Plotly, Vega-Lite for visualizations
- PseudoCode.js for algorithms

## GitHub Actions Workflows

### Critical Workflows
1. **deploy.yml**: Builds and deploys to GitHub Pages on push to main
2. **prettier.yml**: Code formatting validation (fails if formatting incorrect)
3. **broken-links.yml**: Link validation across all pages
4. **lighthouse-badger.yml**: Performance monitoring (requires LIGHTHOUSE_BADGER_TOKEN secret)

### Workflow Fixes
- **Prettier failures**: Run `npx prettier . --write` to fix formatting
- **Lighthouse Badger**: Add LIGHTHOUSE_BADGER_TOKEN secret in GitHub settings
- **Broken links**: Check _config.yml external_sources and update URLs

## Development Notes

### Image Processing
- Uses ImageMagick for thumbnail generation
- Responsive images configured in _config.yml
- Lazy loading enabled by default

### Bibliography Management
- Papers stored in _bibliography/papers.bib
- Cite with {% cite key %} in Markdown
- Configure citation style in _config.yml scholar section

### Theme Customization
- Light/dark theme toggle available
- Color schemes in _sass/_themes.scss
- Bootstrap variables in _sass/_variables.scss

### Performance Optimization
- PurgeCSS removes unused CSS in production
- Jekyll minifier compresses HTML/CSS/JS
- CDN assets with subresource integrity

### Deployment Targets
- **GitHub Pages**: Primary deployment (automatic)
- **Netlify**: Alternative with environment variables
- **Docker**: Container deployment with amirpourmand/al-folio image

## Common Tasks

### Adding a new blog post
Create file in _posts/ with format: YYYY-MM-DD-title.md

### Adding publications
Edit _bibliography/papers.bib and use Jekyll Scholar citations

### Updating CV
Modify _data/cv.yml with structured resume data

### Creating project pages
Add markdown files to _projects/ with numbered prefixes for ordering

### Customizing homepage
Edit _pages/about.md and configure sections in front matter