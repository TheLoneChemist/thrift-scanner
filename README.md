# Thrift Flip — Price Scanner

Snap a photo of any thrift store item and instantly see what it sells for on eBay.

## How it works

1. You take a photo of an item at Goodwill (or any thrift store)
2. Claude AI identifies the item — brand, model, condition
3. It searches eBay's sold listings for real sale prices
4. You see the average price, range, and recent sales

## Local setup

```bash
npm install
cp .env.example .env
# Add your Anthropic API key to .env
npm run dev
# Open http://localhost:3000
```

Get an Anthropic API key at https://console.anthropic.com

## Deploy to Railway

1. Push this repo to GitHub
2. Go to https://railway.app → New Project → Deploy from GitHub repo
3. Select this repo
4. Add environment variable: `ANTHROPIC_API_KEY` = your key
5. Railway auto-detects Node.js and deploys — done

## Project structure

```
├── server.js          # Express server — proxies API calls (keeps key secure)
├── package.json
├── public/
│   └── index.html     # Single-page app — camera, AI, results
└── .env.example
```

## Can this run without AI?

**Image recognition:** No — identifying items from photos requires a vision AI model.
You could replace Claude with OpenAI GPT-4o or Google Gemini by changing the 
`identifyItem()` function in `public/index.html` to call their APIs instead.

**Price lookup:** Yes — eBay has an official API (Browse API + Finding API) that returns 
sold listing data without any AI. This would require an eBay developer account and 
OAuth setup, but would remove that AI dependency entirely.

The image recognition step will always need some AI model. The server proxies the 
Anthropic API so your key stays safe and is never exposed to the browser.
