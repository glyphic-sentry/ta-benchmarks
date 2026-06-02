# TA Benchmarks

A queryable knowledge base of recruiting and talent acquisition benchmark reports for Sentry's TA team — and anyone who wants to use it.

Ask questions like:
- *"What's the average offer acceptance rate for tech companies?"*
- *"How does our time-to-fill compare to industry benchmarks?"*
- *"What does the data say about attrition at growth-stage startups?"*
- *"What's a good reply rate for sourcing outreach?"*

---

## How it works

Reports are stored as structured markdown files in [`/reports`](./reports). Each file follows a consistent format (YAML frontmatter + stats tables + key findings + notable quotes) so they're easy to read, diff, and query.

The [`/skill`](./skill) folder contains a [Cowork](https://claude.ai) skill that lets you interrogate all reports in plain English. When you ask a question, the skill reads the relevant reports and returns cited, sourced answers.

---

## Current report library

| Report | Publisher | Year | Topics |
|--------|-----------|------|--------|
| [Recruiting Operations Benchmarks](./reports/ashby-recruiting-ops-benchmarks-2026.md) | Ashby | 2026 | Screen passthrough, offer acceptance, TTF, referrals |
| [Funnel Benchmarks](./reports/careerplug-gem-funnel-benchmarks-2025.md) | CareerPlug / Gem | 2025 | Full funnel conversion, applicants per hire, trend data |
| [Email Outreach Benchmarks](./reports/gem-email-outreach-benchmarks-2026.md) | Gem | 2026 | Open/reply/interested rates, SOBO, subject line, send timing |
| [US Turnover Survey](./reports/mercer-us-turnover-2025.md) | Mercer | 2025 | Voluntary turnover by industry and level, US |
| [Retention Trends](./reports/ravio-attrition-retention-2026.md) | Ravio | 2026 | Attrition by funding stage, function, country (European tech) |
| [US Tech Attrition Benchmarks](./reports/us-tech-attrition-benchmarks-2025.md) | BLS / Synthesis | 2025 | BLS JOLTS quit rates, generational turnover, remote work impact |

---

## Adding a new report

1. **Check the credibility criteria** — [`skill/references/credibility-criteria.md`](./skill/references/credibility-criteria.md) lists what qualifies.
2. **Copy the template** — [`reports/_template.md`](./reports/_template.md) has the exact format to follow.
3. **Name the file** — use the pattern `<publisher-slug>-<topic>-<year>.md` (e.g. `linkedin-talent-trends-2026.md`).
4. **Open a PR** — add the report file and update the table in this README.

That's it. Once merged, the report is immediately queryable via the Cowork skill.

> **Got a PDF?** Upload it in Cowork and say *"Add this doc to the skill"* — it'll extract the data and create the markdown file for you.

---

## Using the Cowork skill

### Install

1. Download [`ta-report-query.skill`](https://github.com/getsentry/ta-benchmarks/releases/latest) from Releases.
2. Open Claude desktop → Cowork mode → drag the `.skill` file in, or go to **Settings → Skills → Install**.
3. Point the skill at this repo's `reports/` folder as its workspace (or clone the repo and set the path).

### Query examples

```
What's the benchmark offer acceptance rate for tech companies?
How does our sourcing outreach reply rate compare to industry?
What does Ashby say about time-to-hire for technical roles?
Show me the trend in applications per hire since 2021.
Find a quote about referral conversion rates.
```

### Set up weekly auto-updates

Ask the skill: *"Set up weekly report discovery"* — it will schedule a Monday morning search for newly published TA reports, evaluate them against the credibility criteria, and add qualifying ones automatically.

---

## Contribution guide

### Report format

Every report file must include:

```markdown
---
title: "Full report title"
publisher: "Publisher name"
year: 2025
url: "https://source-url.com"
methodology: "How data was collected"
sample_size: "N respondents / applications / etc."
date_retrieved: "YYYY-MM-DD"
---

## Key Statistics

| Metric | Value | Context/Notes |
|--------|-------|---------------|

## Key Findings

[Narrative summary]

## Notable Quotes

> "Direct quote." — Source
```

### Credibility bar

Reports must be from a named publisher, contain quantitative data with a disclosed sample size, be published within the last 3 years, and be relevant to TA/recruiting. See [`skill/references/credibility-criteria.md`](./skill/references/credibility-criteria.md) for the full rubric.

### Good sources to watch

See [`skill/references/report-sources.md`](./skill/references/report-sources.md) for the canonical list of high-quality publishers (Ashby, Gem, LinkedIn, SHRM, iCIMS, Korn Ferry, and more).

---

## Repo structure

```
ta-benchmarks/
├── reports/               # Benchmark reports as structured markdown
│   ├── _template.md       # Copy this when adding a new report
│   └── *.md               # One file per report
├── skill/                 # Cowork skill files
│   ├── SKILL.md           # Skill instructions
│   └── references/        # Credibility criteria + source list
└── .github/
    └── ISSUE_TEMPLATE/    # "Suggest a report" issue template
```

---

## License

Reports are structured summaries of publicly available research. Original data belongs to respective publishers. See individual report files for source URLs.
