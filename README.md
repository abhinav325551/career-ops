# Career-Ops — PMM Edition

<p align="center">
  <img src="docs/hero-banner.jpg" alt="Career-Ops — AI-Powered PMM Job Search" width="800">
</p>

<p align="center">
  <em>Product marketing is a relationship game. But finding the right role is still a numbers game.</em><br>
  Companies use AI to filter candidates. <strong>This gives you AI to <em>choose</em> companies.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude_Code-000?style=flat&logo=anthropic&logoColor=white" alt="Claude Code">
  <img src="https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white" alt="Node.js">
  <img src="https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white" alt="Go">
  <img src="https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white" alt="Playwright">
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="MIT">
</p>

<p align="center">
  <strong>Forked from <a href="https://github.com/santifer/career-ops">santifer/career-ops</a> · customized for Product Marketing roles · India · ASEAN · Middle East · Remote US/EMEA</strong>
</p>

---

## What Is This

Career-Ops turns Claude Code into a full PMM job search command center. Instead of manually tracking applications in a spreadsheet, you get an AI-powered pipeline that:

- **Evaluates offers** with a structured A-F scoring system across CV match, GTM fit, comp, culture, and red flags
- **Generates tailored PDFs** — ATS-optimized CVs with your positioning and proof points adapted per JD
- **Scans portals** automatically — 75+ companies + 35 search queries across India, ASEAN, ME, and remote US/EMEA
- **Processes in batch** — evaluate 10+ offers in parallel with sub-agents
- **Tracks everything** in a single source of truth with integrity checks

> **This is NOT a spray-and-pray tool.** Career-ops is a filter — it helps you find the few roles worth your time out of hundreds. The system recommends against applying to anything below 4.0/5. Your time is valuable.

Career-ops is agentic: Claude navigates career pages with Playwright, evaluates fit by reasoning about your CV vs the JD (not keyword matching), and adapts your resume per listing.

> **The first evaluations won't be perfect.** Feed it context — your CV, your proof points, your deal-breakers, what energises you, what drains you. The more context you give it, the sharper its recommendations get. Think of it as onboarding a recruiter: the first week they need to learn about you, then they become invaluable.

## Target Roles (This Fork)

This fork is configured for **Product Marketing** roles:

| Archetype | What it looks like |
|-----------|-------------------|
| **PMM — Enterprise AI / B2B SaaS** | Positioning, messaging, pricing & packaging, sales enablement, win/loss |
| **PMM — Developer Tools / Platform** | Technical storytelling, developer audience, API/platform products |
| **PMM — Growth / PLG** | Funnel, activation, demand gen, ICP definition, pipeline marketing |
| **Developer Marketing / DevRel Marketing** | Community, content strategy, developer adoption |
| **Head / Director of Product Marketing** | PMM charter, team leadership, board-level GTM narrative |

## Target Markets (This Fork)

| Market | Condition |
|--------|-----------|
| **India** (Bengaluru, Mumbai, Delhi NCR, Hyderabad, Pune) | On-site, hybrid, or remote — primary |
| **Singapore** | Any mode — primary |
| **UAE / Saudi Arabia / Qatar** | Any mode — primary |
| **ASEAN** (Malaysia, Indonesia, Thailand, Philippines, Vietnam) | Any mode |
| **US / EMEA** | **Fully remote only**, OR explicit visa sponsorship / relocation |

## Features

| Feature | Description |
|---------|-------------|
| **Auto-Pipeline** | Paste a job URL, get a full evaluation + tailored PDF + tracker entry |
| **6-Block Evaluation** | CV match, GTM fit, comp research, culture signals, red flags, global score |
| **Interview Story Bank** | Accumulates STAR+Reflection stories across evaluations |
| **Negotiation Scripts** | Market-specific salary scripts for India, Singapore, UAE, and remote USD |
| **ATS PDF Generation** | Keyword-injected CVs with Space Grotesk + DM Sans design |
| **Portal Scanner** | 75+ companies + 35 search queries across India, ASEAN, ME, and global |
| **Batch Processing** | Parallel evaluation with `claude -p` workers |
| **Dashboard TUI** | Terminal UI to browse, filter, and sort your pipeline |
| **Human-in-the-Loop** | AI evaluates and recommends, you decide and act — never auto-submits |
| **Pipeline Integrity** | Automated merge, dedup, status normalization, health checks |

## Quick Start

```bash
# 1. Clone and install
git clone https://github.com/abhinav325551/career-ops.git
cd career-ops && npm install
npx playwright install chromium   # Required for PDF generation

# 2. Check setup
npm run doctor                     # Validates all prerequisites

# 3. Configure your profile
cp config/profile.example.yml config/profile.yml
# Edit config/profile.yml with your name, email, target roles, comp targets

# 4. Add your CV
# Create cv.md in the project root with your CV in markdown

# 5. Portals are pre-configured
# portals.yml is already set up for India/ASEAN/ME + remote US/EMEA PMM roles
# Edit it to add/remove companies as needed

# 6. Open Claude Code and start
claude
# Then paste a job URL or description, or run /career-ops
```

> **portals.yml is already configured** for PMM roles in India, ASEAN, and the Middle East — no need to copy from the template. Just update `config/profile.yml` with your personal details.

See [docs/SETUP.md](docs/SETUP.md) for the full setup guide.

## Usage

```
/career-ops                → Show all available commands
/career-ops {paste a JD}   → Full auto-pipeline (evaluate + PDF + tracker)
/career-ops scan           → Scan portals for new PMM offers
/career-ops pdf            → Generate ATS-optimized CV
/career-ops batch          → Batch evaluate multiple offers
/career-ops tracker        → View application status
/career-ops apply          → Fill application forms with AI
/career-ops pipeline       → Process pending URLs
/career-ops contacto       → LinkedIn outreach message
/career-ops deep           → Deep company research
/career-ops training       → Evaluate a course/cert
/career-ops project        → Evaluate a portfolio project
```

Or just paste a job URL or description directly — career-ops auto-detects it and runs the full pipeline.

## How It Works

```
You paste a job URL or description
        │
        ▼
┌──────────────────────┐
│  Archetype Detection │  PMM-SaaS / PMM-AI / PMM-Growth / DevMarketing / Head-PMM
└────────┬─────────────┘
         │
┌────────▼─────────────┐
│  A-F Evaluation      │  CV match, GTM fit, comp research, STAR stories
│  (reads cv.md)       │
└────────┬─────────────┘
         │
┌────────▼─────────────┐
│  Location Check      │  India/ASEAN/ME → full score
│  (_profile.md rules) │  Remote US/EMEA → 4.0 max
│                      │  On-site US/EU  → 1.5, skip
└────────┬─────────────┘
         │
    ┌────┼────┐
    ▼    ▼    ▼
 Report  PDF  Tracker
  .md   .pdf   .tsv
```

## Pre-configured Company Hotlist (75 companies)

### India B2B SaaS
Freshworks · BrowserStack · Postman · Chargebee · Whatfix · Sprinklr · Icertis · Zenoti · Druva · Darwinbox · Leadsquared · Razorpay · Zoho

### Enterprise AI & Agentic Platforms
Glean · Moveworks · Kore.ai · Yellow.ai · Leena AI · Writer · Observe.AI · Uniphore

### Sales Enablement & Revenue Intelligence
Mindtickle · Highspot · Seismic · Gong · Clari · Outreach

### Customer Engagement / CDP
CleverTap · MoEngage · Braze · Amplitude · Pendo · Mixpanel · Intercom

### ASEAN
Grab · Carousell · PropertyGuru · Traveloka

### Middle East
Careem · Tabby · Unifonic · Noon · Salla

### Global Premium (remote-friendly)
HubSpot · Atlassian · Salesforce · Notion · Figma · Canva · Anthropic · Perplexity

### Global / Tier 8 (remote or visa relocation only)
**AI Labs:** OpenAI · Mistral · Cohere · LangChain · Pinecone
**Voice AI:** ElevenLabs · PolyAI · Parloa · Hume AI · Deepgram · Vapi · Bland AI
**AI Platforms:** Retool · Airtable · Vercel · Temporal · Arize AI
**Contact Center AI:** Ada · LivePerson · Sierra · Decagon · Talkdesk · Genesys
**Enterprise:** Twilio · Dialpad
**LLMOps:** Weights & Biases · Langfuse · Lindy · Cognigy · Speechmatics
**Automation:** n8n · Zapier · Make.com
**European:** Factorial · Attio · Tinybird · Clarity AI · TravelPerk

## Job Portals Searched (35 queries)

**India (22 queries):** Naukri · iimjobs · Indeed India · Foundit · HiRist · Cutshort · Instahyre · Wellfound India · LinkedIn India · Greenhouse/Ashby/Lever with India location filter · Peak XV Partners · Accel India · Lightspeed India · Elevation Capital · Matrix Partners India · Nexus Venture Partners · Blume Ventures · 3one4 Capital · Chiratae Ventures

**Singapore / ASEAN (4 queries):** MyCareersFuture · LinkedIn ASEAN · JobStreet · Greenhouse/Ashby APAC

**Middle East (4 queries):** LinkedIn UAE/Saudi · Bayt · GulfTalent · Naukrigulf

**Remote US/EMEA (5 queries):** Ashby remote · Greenhouse remote · Himalayas · WeWorkRemotely · YC Jobs

## Dashboard TUI

The built-in terminal dashboard lets you browse your pipeline visually:

```bash
cd dashboard
go build -o career-dashboard .
./career-dashboard --path ..
```

Features: 6 filter tabs, 4 sort modes, grouped/flat view, lazy-loaded previews, inline status changes.

## Project Structure

```
career-ops/
├── AGENTS.md                    # Canonical agent instructions
├── CLAUDE.md                    # Claude Code wrapper (imports AGENTS.md)
├── cv.md                        # Your CV in markdown (gitignored)
├── portals.yml                  # Scanner config — PMM/India/ASEAN/ME (tracked)
├── config/
│   ├── profile.example.yml      # Profile template (PMM-configured)
│   └── profile.yml              # Your personal profile (gitignored)
├── modes/
│   ├── _shared.md               # Scoring system + PMM archetype detection
│   ├── _profile.md              # Your PMM archetypes + location policy (tracked)
│   ├── _profile.template.md     # Starter template for _profile.md
│   ├── oferta.md                # Single offer evaluation
│   ├── pdf.md                   # PDF generation
│   ├── scan.md                  # Portal scanner
│   ├── batch.md                 # Batch processing
│   └── ...
├── templates/
│   ├── cv-template.html         # ATS-optimized CV template
│   ├── portals.example.yml      # Scanner config template (PMM-configured)
│   └── states.yml               # Canonical application statuses
├── batch/                       # Batch processing scripts
├── dashboard/                   # Go TUI pipeline viewer
├── data/                        # Tracking data (gitignored)
├── reports/                     # Evaluation reports (gitignored)
├── output/                      # Generated PDFs (gitignored)
├── fonts/                       # Space Grotesk + DM Sans
└── docs/                        # Setup, customization, architecture
```

## Tech Stack

![Claude Code](https://img.shields.io/badge/Claude_Code-000?style=flat&logo=anthropic&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![Bubble Tea](https://img.shields.io/badge/Bubble_Tea-FF75B5?style=flat&logo=go&logoColor=white)

- **Agent**: Claude Code with custom skill modes and PMM archetypes
- **PDF**: Playwright + HTML template
- **Scanner**: Playwright + Greenhouse API + WebSearch (35 queries, India-first)
- **Dashboard**: Go + Bubble Tea + Lipgloss (Catppuccin Mocha theme)
- **Data**: Markdown tables + YAML config + TSV batch files

## Disclaimer

**career-ops is a local, open-source tool — NOT a hosted service.** By using this software, you acknowledge:

1. **You control your data.** Your CV, contact info, and personal data stay on your machine and are sent directly to Anthropic. We do not collect, store, or have access to any of your data.
2. **You control the AI.** The default prompts instruct the AI not to auto-submit applications. Always review AI-generated content before submitting.
3. **You comply with third-party ToS.** Use this tool in accordance with the Terms of Service of career portals you interact with. Do not use it to spam employers.
4. **No guarantees.** Evaluations are recommendations, not truth. The authors are not liable for employment outcomes or any other consequences.

See [LEGAL_DISCLAIMER.md](LEGAL_DISCLAIMER.md) for full details. Licensed under [MIT](LICENSE).

## Credits

Built on top of [santifer/career-ops](https://github.com/santifer/career-ops) by Santiago — an excellent open-source job search system. This fork customizes it for Product Marketing roles across India, ASEAN, and the Middle East.
