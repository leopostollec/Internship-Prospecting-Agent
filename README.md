# Internship Prospecting Agent

An n8n + AI agent that finds internship offers every morning, scores them against my profile, identifies who to contact and drafts a personalized LinkedIn outreach, all logged in Notion. **Running cost: €0.**

![Workflow](workflow.png)

## How it works

Every day at 9:00, the agent:

1. **Sources** recent offers from Google for Jobs (LinkedIn, Indeed, Welcome to the Jungle…) via the JSearch API
2. **Filters** offers already seen on previous days and non-internship contracts
3. **Scores** each offer from 0 to 10 with Gemini; only 7+ continue
4. **Finds** the right contact (public LinkedIn profiles) and recent company news with Tavily
5. **Drafts** a short connection note and a follow-up message built on a verified, specific hook
6. **Logs** everything in a Notion pipeline (To contact → Connection sent → Reply → Interview)

## Design choices

- **Human in the loop**: the agent drafts, I review and send. Each row shows the source of the hook so it can be checked in seconds.
- **No LinkedIn scraping or login automation**: only public, search-indexed data.
- **Anti-hallucination prompts**: facts must come from retrieved data, and generic flattery is banned.
- **Free-tier friendly**: filters run before every quota-consuming step, with batching and retries.

## Stack

n8n (self-hosted) · JSearch API · Google Gemini · Tavily · Notion

## Setup

Import `internship-prospecting-agent.json` into n8n, add your JSearch, Gemini, Tavily and Notion credentials, point the **Envoi Notion** node to your database, and edit the candidate profile in the two AI prompts.

---

Built by [Léo Postollec](https://github.com/leopostollec), Master's student at SKEMA Business School.
