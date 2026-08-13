# Aimer

**2nd place, Location Labs (Avast) Hackday 2019.** A Slack bot that brings encouragement and team connection to the workplace.

Aimer listens for keywords in Slack channels and replies with configurable encouragement: motivational responses from a JSON keyword map, dog photos, coffee and tea break prompts, and a playable Hanabi mini game.

## Team

| Role | Person |
| --- | --- |
| Development | Phoebe Gong |
| QA and Testing | [Oscar Leung](https://github.com/oscar-leung) |
| Product Design | [Jessica Mock](https://jessicamockdesign.com/) |
| Customer Support | Casondra Burnard |

## How it works

The Slack bot entry point lives in `app.py` and `bot.py`, keyword detection and response logic in `interaction.py`, and the configurable keyword to response map in `KW_response_phrases.json`. Break time interactions live in `coffee.py` and `tea.py`, the Hanabi mini game in `hanabi.py`, and response media in `Dogs/` and `Encouragements/`.

## Stack

Python, Slack API, Heroku (Procfile)

## Running

Install dependencies with `pip install -r requirements.txt`, set your Slack bot token as an environment variable, then run `python app.py`.

Built in one day at the Location Labs Hackday 2019, placing 2nd out of 23 teams.
