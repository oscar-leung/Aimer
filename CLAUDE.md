# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

Aimer is a Python Slack bot built at the Location Labs (Avast) Hackday 2019, where it placed 2nd out of 23 teams. It replies to keywords in Slack channels with encouragement: phrases from a JSON keyword map, dog photos, coffee and tea break prompts, and a Hanabi mini game.

## Layout

`app.py` and `bot.py` hold the entry point and Slack event handling. `interaction.py` has keyword detection and response logic. `KW_response_phrases.json` is the configurable keyword to response map. `coffee.py` and `tea.py` handle break interactions, `hanabi.py` the mini game. `Dogs/` and `Encouragements/` hold response media, `models/` holds game state.

## Conventions

Python 3, no test suite. Deployed Heroku style via `Procfile`. The Slack token comes from an environment variable; never commit tokens. Keep response phrases in the JSON config rather than hardcoding them in Python.
