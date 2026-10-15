# Deployment note

## Important: this repository is a Streamlit application

The main UI in `app.py` imports Streamlit and builds a Streamlit dashboard. Vercel's Python runtime expects a supported web application entry point (for example an ASGI `app`), so it fails while trying to interpret this Streamlit script. Adding an `app = ...` variable would not convert the Streamlit dashboard into a Vercel-compatible app.

## Recommended deployment: Streamlit Community Cloud

1. Push this repository to GitHub.
2. Open https://share.streamlit.io/ and sign in with GitHub.
3. Choose **Create app**, select the repository and branch.
4. Set **Main file path** to `app.py`.
5. Add required API keys and credentials in **Advanced settings → Secrets**. Never commit `.env` files or service-account credentials.
6. Deploy and inspect the logs for missing modules or configuration.

## Before deployment

This repository's `app.py` imports `ml_engine` and `integrations` modules that are not present in the uploaded ZIP, so additional runtime import errors may occur after the hosting-platform mismatch is resolved. Those modules must be restored from the original project or the imports refactored to match the modules that are actually included. The repository also contains `run.py`, but its imports do not match all files present in this ZIP; it should not be used as the Streamlit entry point.

## If Vercel is mandatory

Separate the project into a Vercel-compatible frontend and an API backend hosted on a Python-compatible service. Keep Streamlit on Streamlit Community Cloud, or rebuild its UI as a supported frontend. This is an architectural change, not just a one-line fix.
