---
name: ta-report-query
description: >
  Query recruiting and TA benchmark reports for data, stats, and benchmarks.
  Use this skill whenever someone asks about industry benchmarks, offer acceptance
  rates, time-to-fill, pipeline conversion, source-of-hire, recruiter capacity,
  compensation bands, diversity hiring data, or any TA / recruiting metric.
  Also trigger when someone wants to add new benchmark reports to the knowledge
  base, refresh the report library, compare year-over-year trends, find a quote
  from a published report, or set up automated weekly report updates.
  Trigger even on casual phrasings like "what does the data say about X",
  "how do we compare to industry", "any benchmarks for Y", or "pull the
  Ashby numbers on Z".
---

# TA Report Query

This skill turns a folder of recruiting benchmark PDFs and web reports into a
queryable knowledge base that anyone on the TA team can interrogate in plain
English. There are three phases: **Collect**, **Query**, and **Update**. Jump
into whichever phase the user needs.

---

## Phase 1: Collect — Build the Knowledge Base

Use this phase when the user wants to add reports to the knowledge base for the
first time, or wants to top it up with new sources.

### 1a. Set up the storage folder

Reports are saved as structured markdown files in the workspace. Check whether
`reports/` exists in the workspace; if not, create it.

```
<workspace>/reports/
  ashby-talent-trends-2024.md
  gem-outreach-benchmarks-2024.md
  linkedin-global-talent-2024.md
  ...
```

### 1b. Fetch each report

Read `references/report-sources.md` for the canonical list of URLs and
publishers. For each source:

1. Fetch the report page with `mcp__workspace__web_fetch`. If the page is
   client-rendered and returns a shell with no content, switch to
   `mcp__Claude_in_Chrome__navigate` + `mcp__Claude_in_Chrome__get_page_text`.
2. Extract the following fields into a structured markdown file:

```markdown
---
title: "Report Title"
publisher: "Publisher Name"
year: 2024
url: "https://..."
methodology: "Brief description of how data was collected"
sample_size: "N respondents / job postings / etc."
date_retrieved: "YYYY-MM-DD"
---

## Key Statistics

| Metric | Value | Context/Notes |
|--------|-------|---------------|
| Offer acceptance rate | 89% | Enterprise companies >500 employees |
| Median time-to-fill (tech) | 38 days | IC roles only |
| ...   |       |               |

## Key Findings

[Narrative summary of major themes and findings]

## Notable Quotes

> "Direct quote from report." — Section / Page reference

## Methodology Notes

[Any caveats about methodology, sample bias, year of data collection, etc.]
```

3. Save the file as `reports/<publisher-slug>-<year>.md` in the workspace.
4. Tell the user which report was just added and one headline stat from it.

### 1c. Discover additional reports

After processing the canonical list, run a targeted web search for reports
not on the list. Read `references/credibility-criteria.md` to evaluate whether
a newly discovered report qualifies. Add only those that meet the bar. Briefly
tell the user what you found and why each one was included or excluded.

**Good search queries to try:**
- `"recruiting benchmarks report" 2024 site:gem.com OR site:ashbyhq.com OR site:shrm.org`
- `"talent acquisition benchmarks" filetype:pdf 2024`
- `"time to hire benchmark" "source of hire" report 2025`

---

## Phase 2: Query — Answer Questions in Plain English

Use this phase whenever someone asks a recruiting or TA data question.

### 2a. Clarify the year(s)

Before searching, ask: **"Which year are you looking for — or would you like a
year-over-year comparison?"** Year matters because acceptance rates, time-to-fill,
and other metrics shift significantly across cohorts. If the user says "latest"
or "most recent", use the highest year available.

### 2b. Search the knowledge base

List all files in `<workspace>/reports/`. For each relevant file, read it and
extract the stats, quotes, or context that answers the question. Prefer specific
numeric values with their context (sample size, segment, role type) over vague
qualitative statements.

### 2c. Compose the answer

Structure your answer like this:

**[Metric / question answered]**

[Direct answer with numbers]

**Sources:**
- *[Report Title]* ([Publisher], [Year]) — [stat with context]
- *[Report Title]* ([Publisher], [Year]) — [stat with context]

If multiple reports disagree, surface the discrepancy and explain possible
reasons (different sample populations, methodologies, time periods).

### 2d. Quote search

If the user asks to "find a quote" or "what does [report] say about X", scan
the `## Notable Quotes` sections across relevant reports and return verbatim
quotes with full attribution (publisher, year, section).

---

## Phase 3: Update — Automate Weekly Report Discovery

Use this phase when the user wants the knowledge base to stay current
automatically without manual effort.

### 3a. Set up the scheduled task

Use the `schedule` skill to create a weekly recurring task. The task should:

1. Search the web for newly published recruiting/TA benchmark reports
2. For each candidate report, evaluate against `references/credibility-criteria.md`
3. Fetch and extract qualifying reports using the same structure as Phase 1b
4. Save new reports to `<workspace>/reports/`
5. Send a Slack message (or email if Slack isn't connected) summarizing what
   was added

Suggested prompt for the scheduled task:
```
Search the web for recruiting and talent acquisition benchmark reports published
in the last 7 days. Evaluate each against the credibility criteria in
references/credibility-criteria.md. For any that qualify, fetch the full report,
extract structured data, and save it to the reports/ folder in the workspace.
Then send me a Slack message listing what was added.
```

Suggested cadence: **every Monday at 9 AM** (or ask the user their preference).

### 3b. Confirm setup

Show the user exactly what the scheduled task will do and when it will run.
Offer to adjust the cadence or notification channel before finalizing.

---

## Tips & Edge Cases

- **Gated reports** (login-required): Note in the markdown that the report was
  not fully accessible and save what was visible on the landing page. Prompt
  the user to manually upload the PDF if they have access.
- **PDFs**: If a URL leads to a PDF, use the `pdf` skill to extract text before
  structuring it.
- **Year-over-year comparisons**: When multiple years of the same report exist
  in `reports/`, present the comparison in a table with a delta column.
- **No reports yet**: If `reports/` is empty or doesn't exist, offer to kick
  off Phase 1 collection immediately.
- **Conflicting data**: When reports give different numbers for the same metric,
  always show both with the publisher and methodology context rather than
  picking one as "correct".
