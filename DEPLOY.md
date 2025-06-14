# GitHub Pages Deployment Guide

To deploy your Vue Vben Admin project to GitHub Pages, follow these steps:

1. First, create a `.env.production` file in the `apps/web-antd` directory with the following content:

```env
# Base API URL
VITE_GLOB_API_URL=/api

# Base URL
VITE_PUBLIC_PATH=/vue-vben-admin/

# Upload URL
VITE_GLOB_UPLOAD_URL=/upload

# App title
VITE_GLOB_APP_TITLE=Vue Vben Admin

# App short name
VITE_GLOB_APP_SHORT_NAME=Vue Vben Admin

# Enable gzip compression
VITE_COMPRESS=gzip

# Enable PWA
VITE_PWA=true
```

2. Create a new file `.github/workflows/deploy-gh-pages.yml` with the following content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node
        uses: ./.github/actions/setup-node

      - name: Install dependencies
        run: pnpm install

      - name: Build
        run: pnpm run build:antd

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./apps/web-antd/dist
          publish_branch: gh-pages
```

3. Enable GitHub Pages in your repository settings:

   - Go to your repository settings
   - Navigate to "Pages" in the sidebar
   - Under "Source", select "Deploy from a branch"
   - Select the "gh-pages" branch and "/ (root)" folder
   - Click "Save"

4. Push your changes to the main branch:

```bash
git add .
git commit -m "Add GitHub Pages deployment configuration"
git push origin main
```

The GitHub Action will automatically build and deploy your site to GitHub Pages. Your site will be available at `https://ahmd-m-elgaml.github.io/vue-vben-admin/`.

Note: Make sure your repository has the necessary permissions to create and push to the gh-pages branch. The GitHub Action will handle this automatically.
