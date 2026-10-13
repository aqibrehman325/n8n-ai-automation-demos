# n8n AI automation demos

Six working automations built on a self-hosted n8n server (DigitalOcean, Docker, PostgreSQL). Every workflow here runs live with sample data, so you can click the links and try them before reading the code.

| # | Workflow | Try it live | What it does |
|---|----------|-------------|--------------|
| 1 | [Client intake form with instant estimate & lead scoring](workflows/01-client-intake-instant-estimate.json) | https://n8n.rixgpt.com/form/project-inquiry | A prospect fills in a form and sees an estimated effort and price range right away. Each enquiry is scored 0-100 (hot / warm / cold) and shown on a private owner dashboard with a suggested next step. No paid APIs. |
| 2 | [RAG knowledge assistant with source citations (Google Gemini)](workflows/02-rag-knowledge-assistant-gemini.json) | https://n8n.rixgpt.com/webhook/rag-chat?kb=client (staff version: `?kb=staff`, upload your own PDF: https://n8n.rixgpt.com/form/rag-upload) | Documents are split into passages, embedded with `gemini-embedding-001` and searched by meaning. Answers cite the passages they came from and the bot says "I don't know" instead of guessing. Rate limits and follow-up questions included. |
| 3 | [Proposal & quote generator](workflows/03-proposal-quote-generator.json) | internal form (private) | An internal form turns a few choices (package, add-ons, discount, rush) into a printable proposal page with pricing, scope, payment terms and an expiry date. |
| 4 | [Team leave requests with manager approval](workflows/04-leave-requests-approvals.json) | https://n8n.rixgpt.com/form/leave-request | Employees request time off, n8n counts working days, checks the annual allowance and adds the request to an approvals page. The owner approves or rejects with one click and sees who is off in the next 7 days. |
| 5 | [Website uptime monitor & public status page](workflows/05-uptime-monitor-status-page.json) | https://n8n.rixgpt.com/webhook/status | Checks a list of sites every 5 minutes, keeps 24 hours of history and serves a public status page with uptime % and recent incidents. |
| 6 | [GitHub activity digest](workflows/06-github-activity-digest.json) | https://n8n.rixgpt.com/webhook/github-digest | A daily page with commits, pull requests and releases for the accounts and repos you watch, using the public GitHub API. |

![Client intake dashboard](images/01-intake-dashboard.jpg)

![RAG chat with citations](images/02-rag-chat.jpg)

![Leave approvals page](images/04-leave-approvals.jpg)

![Status page](images/05-status-page.jpg)

## How to use these workflows

1. In your n8n instance open **Workflows → Import from file** and pick one of the JSON files in `workflows/`.
2. Private pages (owner dashboard, approvals page, proposal builder, re-index URL) use webhook paths ending in `CHANGE-ME-1` … `CHANGE-ME-4`. Replace them with your own random strings so nobody can guess the URLs.
3. Workflow 2 needs a Google Gemini API credential (the free tier is enough): open the four Gemini nodes and select your credential. Then open the re-index URL once to build the vectors.
4. Workflow 1, 3, 4 and 5 use no external APIs at all. Data is kept in the workflow's static data, which is fine for demos and small teams; for larger volumes point the Code nodes at PostgreSQL (or pgvector / Qdrant for the RAG workflow).
5. Activate the workflow. Form URLs are `/form/<path>`, pages and APIs are `/webhook/<path>`.

Tested on n8n 2.35 with the Code, Form Trigger, Webhook, Respond to Webhook, Schedule Trigger, HTTP Request, Extract from File and LangChain (Gemini) nodes.

## Notes

- All names, documents and numbers in the demos are fictional ("Harborline Software", "Northwind", etc.).
- The workflows are kept deliberately small so they are easy to read: one Code node per step, comments at the top of each node, and a sticky note in each workflow that explains the flow.
- Built and maintained by Aqib ur Rehman — AI agent and n8n automation developer. Upwork profile: https://www.upwork.com/freelancers/aqibrehman

## License

MIT — use them in your own projects.
