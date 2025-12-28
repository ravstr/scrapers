# Business Scraper

A web application for scraping business data from Google Maps (via Apify) and searching for people (via Exa API).

## Features

- **Business Scraper**: Extract business information from Google Maps based on location and industry
- **People Search**: Find people and their LinkedIn profiles using Exa API

## Setup

1. Clone this repository
2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables (for local development):
   ```bash
   cp env.example .env
   # Edit .env and add your API keys
   ```

## Deployment to Netlify

See [NETLIFY_DEPLOY.md](./NETLIFY_DEPLOY.md) for detailed deployment instructions.

### Quick Deploy Steps:

1. Push your code to GitHub
2. Connect your repository to Netlify
3. Set environment variables in Netlify Dashboard:
   - `APIFY_API_TOKEN` - Your Apify API token
   - `EXA_API_KEY` - Your Exa API key
4. Deploy!

## Environment Variables

- `APIFY_API_TOKEN`: Get from [Apify Console](https://console.apify.com/account/integrations)
- `EXA_API_KEY`: Get from [Exa Dashboard](https://dashboard.exa.ai/api-keys)

## Local Development

```bash
# Install Netlify CLI globally
npm install -g netlify-cli

# Run local development server
netlify dev
```

This will start a local server at `http://localhost:8888` with working serverless functions.

## Project Structure

```
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

## License

MIT

