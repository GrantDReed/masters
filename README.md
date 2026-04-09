# Masters 2026 Fantasy Challenge

Live fantasy golf dashboard for 10 teams tracking the 2026 Masters Tournament.

## Deploy to Vercel (free, 2 minutes)

1. Install Vercel CLI: `npm i -g vercel`
2. Unzip this project
3. `cd masters-fantasy`
4. `vercel` — follow prompts, done!

Or drag-and-drop the folder at [vercel.com/new](https://vercel.com/new).

## How it works

- `/public/index.html` — the dashboard (React via CDN, no build step)
- `/api/scores.js` — serverless function that fetches live scores from masters.com / ESPN (server-side, no CORS issues)
- Auto-refreshes every 3 minutes
- Scores pulled from masters.com first, ESPN as fallback

## Sharing

Once deployed, Vercel gives you a URL like `masters-fantasy-2026.vercel.app` — share that with your group and everyone can track scores live.
