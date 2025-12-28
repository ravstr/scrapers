# Business Scraper - Netlify Deployment Guide

This application combines Google Maps business scraping (via Apify) with people search (via Exa API) using Netlify Functions.

## Project Structure

```
your-project/
├── index.html                    # Main application
├── netlify.toml                  # Netlify configuration
├── package.json                  # Node.js dependencies
├── .gitignore                    # Git ignore file
├── env.example                   # Example environment variables
└── netlify/
    └── functions/                # Serverless functions
        ├── apify-scraper.js      # Apify API proxy function
        └── exa-search.js         # Exa API proxy function
```

## Deployment Steps

### Option 1: Deploy via Netlify Dashboard (Easiest)

1. **Create a new Git repository** (GitHub, GitLab, or Bitbucket)
   
2. **Add these files to your repository:**
   - `index.html`
   - `netlify.toml`
   - `package.json`
   - `.gitignore`
   - `netlify/functions/apify-scraper.js`
   - `netlify/functions/exa-search.js`

3. **Push to your Git repository:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

4. **Connect to Netlify:**
   - Go to https://app.netlify.com
   - Click "Add new site" → "Import an existing project"
   - Connect your Git repository
   - Netlify will auto-detect the settings from `netlify.toml`
   - Click "Deploy site"

5. **Add Environment Variables (Required for Security):**
   - Go to Site settings → Environment variables
   - Add these variables:
     - `APIFY_API_TOKEN` = `your-apify-token-here`
     - `EXA_API_KEY` = `your-exa-api-key-here`
   - This keeps your API keys secure and out of the code
   - Get your tokens from:
     - Apify: https://console.apify.com/account/integrations
     - Exa: https://dashboard.exa.ai/api-keys

6. **Done!** Your site will be live at `https://your-site-name.netlify.app`

### Option 2: Deploy via Netlify CLI (For Testing)

1. **Install Netlify CLI:**
   ```bash
   npm install -g netlify-cli
   ```

2. **Login to Netlify:**
   ```bash
   netlify login
   ```

3. **Test locally:**
   ```bash
   netlify dev
   ```
   This will start a local server at `http://localhost:8888` with working functions

4. **Deploy:**
   ```bash
   netlify deploy --prod
   ```

### Option 3: Manual Deploy (Drag & Drop)

1. **Create a folder** with all files
2. **Rename** `apify-scraper.html` to `index.html`
3. **Go to** https://app.netlify.com/drop
4. **Drag and drop** your folder
5. **Note:** Manual deploys don't support serverless functions, so use Option 1 or 2

## Configuration

### Function Paths

The HTML is already configured to use the correct paths:
- `/.netlify/functions/apify-scraper` for the Apify scraper
- `/.netlify/functions/exa-search` for the Exa search

These paths work for both:
- Local testing with Netlify CLI: `http://localhost:8888/.netlify/functions/[function-name]`
- Production: `https://your-site-name.netlify.app/.netlify/functions/[function-name]`

No changes needed! ✅

### Environment Variables (Required)

**Important:** Both API tokens should be set as environment variables for security:

1. In Netlify Dashboard: **Site settings → Environment variables**
2. Add both:
   - `APIFY_API_TOKEN` = `your-apify-token-here`
   - `EXA_API_KEY` = `your-exa-api-key-here`
3. Both functions check for these environment variables

**Where to get your API keys:**
- Apify Token: https://console.apify.com/account/integrations
- Exa API Key: https://dashboard.exa.ai/api-keys

**Why this matters:**
- Keeps API keys out of your code/repository
- Prevents unauthorized use of your API credits
- GitHub won't flag exposed secrets

## Usage

### Business Scraper (Google Maps)
1. Enter a location (e.g., "Houston, Texas")
2. Enter a business segment (e.g., "Education")
3. Click "Run Scraper"
4. Wait for results (10-30 seconds)

### People Search (Exa)
1. Enter a search query (e.g., "GTM execs at xAI")
2. Click "Search People"
3. View names and LinkedIn URLs

## Troubleshooting

**Functions not working:**
- Make sure you deployed via Git (not drag & drop)
- Check function logs in Netlify Dashboard → Functions
- Test locally with `netlify dev` first

**CORS errors:**
- The function already has CORS headers configured
- Clear your browser cache and try again

**API errors:**
- Check that environment variables are set correctly
- Verify API keys are still valid

## Cost

- **Netlify**: Free tier includes 125k function requests/month
- **Apify**: Based on your Apify plan
- **Exa**: Based on your Exa plan

## Local Development

To test everything locally before deploying:

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Run local dev server
netlify dev
```

This starts a server at `http://localhost:8888` with working serverless functions!

## Support

- Netlify Docs: https://docs.netlify.com/functions/overview/
- Exa API Docs: https://docs.exa.ai
- Apify Docs: https://docs.apify.com
