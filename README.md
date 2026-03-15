# bibliometrics-review

> A Claude Code / Cowork skill that guides researchers through the **full workflow** of writing a high-quality bibliometric review article — from research question design to submission-ready manuscript.

[![Claude Skill](https://img.shields.io/badge/Claude-Skill-blue)](https://claude.ai)
[![Version](https://img.shields.io/badge/version-0.5.0-green)](CHANGELOG.md)
[![License](https://img.shields.io/badge/license-MIT-orange)](LICENSE)

---

## What It Does

This skill turns Claude into an **academic mentor and writing co-pilot** for bibliometric review papers. It covers every stage of the research-to-publication pipeline:

| Stage | What Claude does | What you do |
|-------|-----------------|-------------|
| 0 — Topic Diagnosis | Evaluates your draft title with FINER framework; flags scope/novelty issues | Decide whether to adjust the title |
| 0 — Article Type | Explains Type A (pure bibliometrics) vs Type B (bibliometrics + content analysis) | Choose the type that fits your goal |
| 1 — Search Strategy | Designs WoS/Scopus query strings and PRISMA flow | Run the search and export records |
| 2 — Data Validation | Checks your raw export for completeness | Run deduplication and screening |
| 3 — Chapter Structure | Proposes a two-level chapter outline; negotiates until you confirm | Approve or reshape the structure |
| 4 — Section Drafting | Provides logic brief + tiered figure menu before each section, then writes the draft | Select figures and give feedback |
| 5 — Polish & Integration | Tightens transitions, checks consistency, PRISMA compliance | Final review |
| 6 — Journal Targeting | Recommends Q1 journals; formats reference list | Submission |

**Key behaviours:**
- **User-will-first**: Claude warns once on risky decisions, then follows your lead — it never blocks your workflow.
- **Persistent learning**: `lesson.md` accumulates your preferences across all projects so Claude improves over time.
- **Reference paper parsing**: Upload a PDF of an exemplar review and Claude extracts its structure, logic, and figure inventory, then asks whether to update the skill's knowledge base.
- **PDF dependency**: PDF extraction uses the `pdf` skill (declared in `compatibility`).

---

## Skill Structure

```
bibliometrics-review/
├── SKILL.md                     # Main orchestration file (the skill brain)
├── lesson.md                    # Cross-project persistent learning log
└── references/
    ├── analysis_guide.md        # Tiered figure menu for all analysis sections
    ├── journal_standards.md     # Q1 journal profiles (Scientometrics, JoI, JASIST, IJERPH, TFSC, JBR)
    ├── prisma_checklist.md      # PRISMA 2020 checklist with bibliometrics-specific notes
    └── writing_examples.md      # Section logic briefs + annotated exemplar passages
```

---

## Installation

### Option A — Install the `.skill` package (Cowork / Claude desktop app)

1. Download [`bibliometrics-review.skill`](bibliometrics-review.skill) from the Releases page.
2. In the Claude desktop app, open **Cowork** → **Skills** → **Install from file**.
3. Select the `.skill` file. Claude will validate and register it automatically.

### Option B — Clone and reference manually (Claude Code CLI)

```bash
git clone https://github.com/njitclass/bibliometrics-review.git
```

Then add the skill path to your Claude Code project config or invoke it directly in a session.

---

## Compatibility

| Dependency | Required | Reason |
|------------|----------|--------|
| `pdf` skill | Recommended | Needed to extract text from uploaded reference PDF files. Without it, Claude can only process pasted text. |

---

## Supported Analysis Methods

- **Publication trend analysis** — annual output, growth rate, predictive extrapolation
- **Productive sources** — journals, authors, countries/regions, institutions (Lotka / Bradford / Price laws)
- **Citation analysis** — co-citation, bibliographic coupling (VOSviewer)
- **Co-word & thematic analysis** — keyword co-occurrence, strategic diagrams, thematic evolution (Bibliometrix R)
- **Content analysis** *(Type B only)* — coding scheme, inter-rater reliability (Cohen's κ), category statistics

## Target Journals

| Journal | IF (approx.) | Q |
|---------|-------------|---|
| Journal of Informetrics | 10.5 | Q1 |
| Scientometrics | 4.1 | Q1 |
| JASIST | 3.5 | Q1 |
| TFSC (Technological Forecasting & Social Change) | 12.9 | Q1 |
| IJERPH | 4.6 | Q1 |
| Journal of Business Research | 11.3 | Q1 |

---

## Usage Examples

**Start a new project:**
> "I want to write a bibliometric review on carbon neutrality in supply chains."

**Parse an exemplar paper:**
> *[Upload a PDF of a published review]* "Please analyze this paper and compare it with the skill's knowledge base."

**Jump to a specific stage:**
> "Skip to chapter structure — I've already completed the search and screening."

---

## File Descriptions

### `SKILL.md`
The orchestration file Claude reads at session start. Contains:
- YAML frontmatter (`name`, `description`, `compatibility`)
- Startup sequence (load `lesson.md` → check `PROJECT_STATE.md`)
- Reference paper parsing trigger (Step 0: PDF extraction → structural analysis → knowledge update)
- All 7 stage definitions with gate conditions
- `lesson.md` update rules

### `lesson.md`
A persistent log of learned user preferences, organized into 9 categories: writing style, chapter structure, figure preferences, tools/tech, methodology choices, journal/domain standards, workflow habits, reference paper learning log, and pending observations. Survives across projects — the more you use the skill, the better it knows you.

### `references/analysis_guide.md`
A tiered figure menu covering every analysis section. For each figure: tier (🟢 Basic / 🟡 Intermediate / 🔴 Advanced), chart type, required data, role in the paper, recommended tool, and notes. Includes VOSviewer parameter quick-reference and Bibliometrix R function cheatsheet.

### `references/journal_standards.md`
Detailed profiles for 6 Q1 journals: positioning, accepted article types, reviewer focus, style preferences, word limits, and formatting requirements. Includes a comparison table and universal Q1 submission checklist.

### `references/prisma_checklist.md`
Full PRISMA 2020 checklist (30 items) annotated with bibliometrics-specific guidance and Q1 publication advice. Includes an extra section on bibliometrics-only requirements beyond the standard PRISMA items.

### `references/writing_examples.md`
Section-by-section writing guidance with underlying logic, excellence criteria, common failure points, transition logic, word count targets, and annotated exemplar passages in English.

---

## Roadmap

- **V2**: Automated web search integration (WoS/Scopus API query assistant)
- **V2**: Data preprocessing script templates (R/Python for VOSviewer export cleaning)
- **V3**: Multi-language output support (Chinese abstract + English manuscript)
- **V3**: Journal submission letter template generator

---

## Contributing

Issues and PRs are welcome. If you have:
- A Q1 bibliometrics paper you'd like to add as a reference case → open an Issue with the DOI
- A journal profile to add → submit a PR editing `references/journal_standards.md`
- A bug in the stage logic → open an Issue describing the unexpected behavior

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

## Citation

If this skill assists your research workflow, a mention in the Acknowledgements section is appreciated:

> "The manuscript workflow was assisted by the `bibliometrics-review` Claude Code skill (https://github.com/njitclass/bibliometrics-review)."
