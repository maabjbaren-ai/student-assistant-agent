# Product Requirements Document (PRD)

## 1. Executive Summary & Backstory
* **Target User:** A 3rd-year university student facing an overwhelming end-of-semester workload, including final exams, project submissions, continuous resume tailoring, and developing portfolio projects for job applications.
* **The Problem:** Extreme time management strain. The user struggles to track academic deadlines, interview invitations, and project milestones across multiple disconnected channels. Missing a single email or mismanaging a calendar slot directly impacts her academic success and career entry.
* **The Solution:** An autonomous AI Agent that bridges the gap between text-based communication (Gmail) and calendar scheduling (Google Calendar). The agent continuously monitors incoming emails, extracts semantic scheduling data, cross-references availability, and dynamically updates a centralized schedule with contextual descriptions and actionable task associations.

---

## 2. System Objectives & Scope
* **Automated Extraction:** Parse unstructured natural language from emails to identify potential events, deadlines, exams, or interviews.
* **Contextual Enrichment:** Instead of basic titles, enrich calendar events with brief analytical summaries, required documents (e.g., "Bring updated CV"), and follow-up flags.
* **Conflict Resolution:** Query the user's Google Calendar to evaluate availability and autonomously draft appropriate responses if schedule overlaps occur.
* **Secure Engineering Standards:** Adhere strictly to the Google OAuth 2.0 verification protocol without exposing sensitive keys or tokens in public repositories.

---

## 3. Functional Requirements (FR)

### FR-1: Email Ingestion and Filtering
* The system must scan the user's Gmail inbox (filtering for unread messages or specific labels within a sliding time window, e.g., last 48 hours).
* The system must filter out irrelevant promotional/spam emails and focus exclusively on actionable academic or career-related queries.

### FR-2: Semantic Entity Extraction via LLM
* For every relevant email, an LLM must analyze the unstructured text to extract:
  * **Event Type:** Exam, Project Submission, Job Interview, Team Meeting.
  * **Temporal Data:** Date, Start Time, and End Time (or default duration).
  * **Contextual Description:** A 1–2 sentence breakdown of what the event is about.
  * **Action Items / Prerequisites:** Material to prepare, emails to reply to, or documents to bring (e.g., CV, Presentation slides).

### FR-3: Calendar Verification & Event Creation
* **Availability Check:** The agent must query Google Calendar for the extracted time slot.
* **Scenario A (Slot is Free):** The agent creates an event titled logically (e.g., `[Exam] Logistics Systems` or `[Interview] Software Co.`) and populates the description field with the enriched LLM context.
* **Scenario B (Conflict Detected):** The agent blocks the creation and triggers an autonomous refusal flow.

### FR-4: Automated Response Formulation
* If an event is successfully scheduled, the agent can flag it as completed.
* If a conflict occurs, the agent must leverage the LLM to draft a professional response email to the sender, explaining the conflict and politely requesting an alternative slot.

---

## 4. Non-Functional Requirements (NFR)
* **Security & Credentials Separation:** Absolute isolation of environment variables. `credentials.json` and `token.json` must remain local and explicitly blacklisted in `.gitignore`.
* **Reliability & Error Handling:** Graceful failure modes when API rate limits are hit or when natural language text lacks explicit dates/times (fallback to asking for clarification).
* **Execution Environment:** Fast, reproducible virtual environment dependency resolution using `uv`.