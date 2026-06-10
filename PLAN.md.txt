# Project Plan - Student Assistant AI Agent

## Phase 1: Infrastructure & Authentication (Days 1-3)
* Set up Python environment using `uv` for local configuration.
* Complete Google Auth Platform registration under Desktop Application credentials.
* Establish secure local environments by generating and localizing `credentials.json`.

## Phase 2: Gmail & Calendar API Integration (Days 4-6)
* Implement foundational code using `google-api-python-client` to scan and fetch unread emails.
* Integrate logic for reading/writing calendar entries through the Google Calendar API service.
* Implement token token management (`token.json`) with automated refresh token handlers.

## Phase 3: Semantic Analysis & LLM Connection (Days 7-9)
* Design dynamic prompts to enforce strict structured data extraction from unstructured emails (Date, Time, Prerequisites).
* Integrate the selected LLM to convert incoming natural language into strict JSON structures.

## Phase 4: Business Logic & Refusal Flow (Days 10-12)
* Write conflict-checking loops comparing requested slots against existing calendar events.
* Create logic for auto-generating a Gmail draft reply if a schedule conflict occurs.

## Phase 5: Verification & Deployment (Days 13-14)
* Run end-to-end simulation tests with mock academic deadlines and career interview invites.
* Finalize the root `README.md` and push all verified code and tracking markdown files to GitHub.