# Just Wright

A creative writing studio: story sparks, world building, character creation, three-act structure lessons, a community library with critique modes, and AI writing mentors. Accounts save your work and track XP.

AI runs on Google Gemini's free tier by default (Claude is optional). If no key is set or Gemini is busy, the app shows built-in sample content instead of failing.

## Run locally

Requires Python 3.10+.

```bash
cp .env.example .env      # then put your key in GEMINI_API_KEY
./run.sh                  # opens on http://localhost:8000
```

## Deploy to Render

1. In Render, choose **New → Blueprint** and connect this repository. Render reads `render.yaml`.
2. When prompted, paste your Gemini key into `GEMINI_API_KEY`. `SECRET_KEY` is generated for you.
3. Apply. The site will be live at `https://just-wright.onrender.com` (or a similar name).

The database is a SQLite file on a 1 GB persistent disk mounted at `/var/data`, so accounts and stories survive redeploys. Persistent disks require a paid Render instance (`plan: starter`).

## Configuration

| Variable | Default | Purpose |
|---|---|---|
| `AI_PROVIDER` | `gemini` | `gemini`, `claude`, or `auto` |
| `GEMINI_API_KEY` | — | Key from https://aistudio.google.com/app/apikey |
| `GEMINI_MODELS` | `gemini-flash-latest,gemini-3.6-flash,gemini-flash-lite-latest` | Tried in order when a model is busy |
| `ANTHROPIC_API_KEY` | — | Optional, for `claude` |
| `SECRET_KEY` | dev value | Signs login tokens — must be set in production |
| `DB_PATH` | `./just_wright.db` | SQLite file location |
| `FREE_DAILY_LIMIT` / `AUTH_DAILY_LIMIT` | `50` / `200` | Daily AI requests for guests / signed-in users |
