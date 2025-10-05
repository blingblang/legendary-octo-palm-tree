# Project Overview
- Purpose: Fast static frontend built with Astro, consuming content from headless Drupal CMS backend
- Tech stack: Astro 5.x, Tailwind CSS 4.x, Node.js 18+, Drupal 10+ (JSON:API), DigitalOcean Droplet (backend), Vercel (frontend hosting)
- Architecture: Headless/decoupled - Drupal provides content via JSON:API, Astro builds static site with dynamic content fetching

# Key Directories & Files
- docs/: product and developer docs;
- src/: Astro components, pages, and layouts
- src/pages/: File-based routing for static and dynamic pages[20][23]
- src/components/: Reusable Astro and framework components
- src/styles/: Global CSS and Tailwind configuration files[2][5]
- src/lib/: Utility functions for Drupal API calls and data transformation
- public/: Static assets (images, fonts, etc.)
- astro.config.mjs: Astro configuration with Vercel adapter and integrations[25][28]

# Commands (do not guess)
- Setup: npm install
- Dev server: npm run dev (starts on localhost:4321)[1][4]
- Build: npm run build (generates dist/ folder for deployment)[1][4]
- Preview: npm run preview (preview production build locally)[1][4]  
- Type check: npm run astro check[1]
- Tailwind: Integrated via @tailwindcss/vite plugin[14]
- Deploy: Automatic via Vercel Git integration, or vercel deploy[3][9]

# Code Style & Conventions
- Use TypeScript for type safety; avoid any types
- Astro component syntax: frontmatter in --- blocks, HTML-like templates
- Tailwind utility classes; avoid custom CSS unless necessary[21][24]
- File naming: kebab-case for pages/components, PascalCase for TypeScript interfaces
- Import styles: Import global CSS in layouts, not individual components[27]
- API calls: Use fetch() in Astro frontmatter for build-time data fetching[25]

# "Do Not Touch" / Caution Zones
- Do not modify astro.config.mjs without testing build process[6]
- Do not change Vercel deployment settings without backup
- Do not alter Drupal JSON:API endpoints without coordinating with backend team
- Do not bypass Tailwind's utility-first approach with custom CSS

# Drupal Integration
- Backend URL: Environment variable DRUPAL_BASE_URL (set in .env and Vercel dashboard)
- API endpoints: Use Drupal JSON:API format (/jsonapi/node/article)[36][39]
- Content fetching: Build-time fetching in getStaticPaths() and frontmatter[25]
- Media handling: Process Drupal file URLs and image styles for optimization[20]
- CORS: Ensure Drupal CORS settings allow Vercel domain requests[20]
- **CRITICAL - Drupal Structure**: Backend MUST conform to docs/drupal-canonical-folder-structure.md
- **Drupal Root**: Always /var/www/html inside containers (never /opt/drupal/web)
- **Key Tools**: Composer at /usr/local/bin/composer, Drush at /var/www/html/vendor/bin/drush

# Deployment & Hosting
- Frontend: Vercel with automatic deployments from GitHub main branch[3][9]
- Backend: Drupal on DigitalOcean Droplet (managed separately)[18][21]
- Environment variables: Set DRUPAL_BASE_URL in Vercel dashboard and .env.local[3]
- Build output: Static site generation (SSG) by default, hybrid rendering if needed[9]
- Vercel adapter: @astrojs/vercel configured for static deployment[6][9]

# Performance & Optimization
- Astro Islands: Use client directives (client:load, client:visible) sparingly
- Image optimization: Use Astro's built-in image optimization with Drupal media[25]
- Tailwind purging: Ensure content paths in tailwind.config include all template files[5][8]
- Bundle analysis: Use astro build --analyze for bundle insights[1]

# Content & API Management
- Content types: Sync with Drupal content model and field configurations
- API rate limiting: Implement caching for Drupal API responses during build
- Content preview: Consider Drupal preview integration for content editors
- Error handling: Graceful fallbacks when Drupal API is unavailable

# Development Workflow
- Local development: Run both Astro dev server and Drupal backend locally or use staging Drupal URL
- Git flow: Feature branches, PRs required for main branch
- Testing: Test API integrations and responsive design across devices
- Staging: Use Vercel preview deployments for feature branch testing[22]

# Security & Environment
- API keys: Store sensitive credentials in Vercel environment variables, not in code
- CORS: Whitelist Vercel domains in Drupal CORS configuration[39]
- Content validation: Validate and sanitize Drupal API responses
- Rate limiting: Implement request throttling for Drupal API calls

# How to Work With Me (Claude)  
- Always use the exact commands listed above; ask before creating new scripts[20][23]
- For Drupal integration questions, specify the content type and field structure
- When modifying Tailwind config, ensure it matches Astro's integration approach[33]
- For performance issues, check both Astro build output and Vercel deployment logs
- Prefer minimal, targeted changes over large refactors
- **NEVER use heredoc (cat << EOF) commands** - they break in terminals. Use nano/vim or echo instead
- **NEVER use exclamation marks in passwords** - they cause bash history expansion errors
- For file creation: Use `nano filename` or `echo "content" > filename` only

# Pointers
- Drupal API documentation: /jsonapi URLs on your Drupal instance
- Astro docs: https://docs.astro.build for component patterns and integrations[20]
- Tailwind utilities: Use Tailwind IntelliSense for class suggestions[2]
- Vercel deployment logs: Check Vercel dashboard for build and runtime errors[3]
- Local env file: .env.local for local development environment variables
