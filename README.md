# Aimer

> A Slack bot that keeps a remote team connected — brewed over a weekend at an internal hackathon.

Aimer is a Python/Flask Slack bot built at an internal company hackathon in November 2019. It was designed to make a distributed customer-support team feel a little less distributed: scheduling spontaneous coffee/tea/game breaks, responding to keyword triggers with encouragement, and occasionally dropping a dog picture into the channel when someone needed one.

## Why we built it

Our team was split across offices and time zones and we'd noticed the small social moments — "want to grab coffee?", "anyone up for a quick game?" — didn't survive the jump to Slack. Aimer's job was to take those moments, which used to die in DMs, and broadcast them to the whole team with a one-click join button.

## When

Built in ~24 hours at an internal hackathon, November 2019.

## Team

This was a four-person project. Crediting honestly:

- **Phoebe Gong** — Developer (primary author of the bot)
- **Oscar Leung** — QA (that's me — I tested the slash commands and response flows, helped shape the interaction model, and pushed on edge cases around time parsing)
- **Jessica Mock** — Product Design
- **Casondra Burnard** — Customer Support domain expertise

## What it does

- **Slash commands** — `/coffee`, `/tea`, and `/hanabi` broadcast a message to a shared channel inviting teammates to join at a parsed time ("3pm", "@4pm", etc.). Includes inline Yes / No voting buttons.
- **Keyword responder** — scans channel and DM messages for keywords defined in `KW_response_phrases.json` and replies with the matching phrase. Falls back to a small set of default "tell me more" responses in DMs.
- **Encouragement bank** — drops a positive image from `Encouragements/` on request.
- **Dog pictures** — obviously.

## Tech stack

- **Python 3.7** + Flask for the HTTP endpoints
- **slackclient** (Slack Web API) for posting messages and interactive attachments
- **Flask-SQLAlchemy** + **PyMySQL** against JawsDB (MySQL on Heroku) for vote tracking
- **gunicorn** for production serving, deployed to Heroku (`Procfile` included)
- **pytz** for time-zone-aware parsing of `/coffee 3pm` style inputs

## What I learned

- **Slack's Events API and interactive components** — how verification tokens, action callbacks, and message updates fit together.
- **Testing a messaging bot is its own problem** — the interaction surface is chat, which is inherently fuzzy; a small harness that replays recorded messages through `interaction.reply` is worth its weight.
- **Time parsing is never as simple as it looks** — `"3"`, `"3pm"`, `"@3pm"`, `"at 3"` all came up in the first hour of dogfooding.
- **Hackathon scope discipline** — shipping a rough-but-working bot beats a polished-but-unfinished one.

## Run it locally

```bash
pip install -r requirements.txt
export SLACK_API_TOKEN=xoxb-...           # from a Slack app with chat:write + commands
export VERIFICATION_TOKEN=...             # Slack app verification token
export COFFEE_CHANNEL=C01234567           # channel ID for the coffee break broadcast
export JAWSDB_URL=mysql://user:pw@host/db # MySQL connection string
gunicorn app:app
```

Then wire the `/coffee`, `/tea`, `/hanabi` slash commands to your deployed URL in the Slack app configuration.

## Repo layout

```
app.py                    # Flask routes + slash command handlers
bot.py                    # Slack WebClient wrapper
interaction.py            # Keyword matching + reply logic
coffee.py / tea.py /
  hanabi.py               # Per-activity broadcast + vote tracking
KW_response_phrases.json  # Keyword -> response phrase map
Dogs/                     # Dog image assets
Encouragements/           # Encouragement image assets
models/                   # SQLAlchemy models (vote tallies)
Procfile + runtime.txt    # Heroku deployment config
```

## Status

Archived as a hackathon artifact — the Slack API and `slackclient` library have moved on since 2019, so this would need dependency updates to run today. Kept here as an honest record of what a weekend of hackathon code looks like.

---

Repo maintained by **Oscar Leung** — [github.com/oscar-leung](https://github.com/oscar-leung)
