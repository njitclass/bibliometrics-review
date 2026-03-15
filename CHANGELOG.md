# Changelog

All notable changes to `bibliometrics-review` are documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Version numbering follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.5.0] — 2026-03-15

### Added
- **`lesson.md` cross-project learning mechanism**: Claude now maintains a persistent preference log across all projects. Observed user preferences are promoted to formal entries after two independent confirmations (two-strike rule). Nine categories tracked: writing style, chapter structure, figure preferences, tools/tech, methodology, journal/domain standards, workflow habits, reference paper learning log, and pending observations.
- **Reference paper parsing & skill self-update mechanism**: When a user uploads or pastes an exemplar bibliometrics review, Claude automatically extracts (1) chapter structure overview, (2) per-section core logic, and (3) figure inventory. Parsed results are compared against the four knowledge-base files and the user is asked whether to update them.
- **PDF skill dependency declaration**: `SKILL.md` frontmatter now declares `compatibility.required_skills` with a dependency on the `pdf` skill. When a PDF is uploaded, Claude invokes the `pdf` skill for full-text extraction before entering the parsing flow.
- **Step 0 in reference parser**: Explicit routing table for PDF files, pasted text, and DOI-only inputs — Claude never proceeds with analysis when it has no actual content.

### Changed
- `SKILL.md` startup sequence updated to load `lesson.md` first and surface active preferences at session start.

---

## [0.4.0] — 2026-03-15

### Added
- **Pre-section logic brief**: Before drafting each section, Claude outputs the underlying academic logic and excellence criteria for that section.
- **Tiered figure menu** (`references/analysis_guide.md`): For every analysis section, Claude presents a menu of figures/charts organized into three tiers — 🟢 Basic, 🟡 Intermediate, 🔴 Advanced — with type, required data, functional role in the paper, and recommended tool. Users select based on their own capability.
- VOSviewer parameter quick-reference table (minimum thresholds, normalization methods, clustering).
- Bibliometrix R function cheatsheet.
- Cohen's κ interpretation table for Type B inter-rater reliability.

---

## [0.3.0] — 2026-03-15

### Added
- **Article type classification (A / B)**: Type A = pure bibliometrics; Type B = bibliometrics + content analysis. Type is selected at Stage 0 and gates all subsequent stage and chapter logic.
- **Chapter structure negotiation mechanism**: Claude proposes a two-level chapter outline and iterates with the user before any drafting begins. Users may override any structural suggestion.
- **Section-by-section drafting workflow**: Draft → user feedback → consolidated revision cycle. Users can also request a full draft in one pass.
- `references/writing_examples.md`: Section logic briefs and annotated exemplar passages for Abstract, Introduction, Methodology, Results (3.1–3.4), Discussion, and Conclusion.
- `references/journal_standards.md`: Profiles for Scientometrics, JoI, JASIST, TFSC, IJERPH, and Journal of Business Research.
- `references/prisma_checklist.md`: Full PRISMA 2020 checklist with bibliometrics-specific annotations.

---

## [0.2.0] — 2026-03-15

### Added
- **User-will-first principle**: If a user overrides Claude's suggestion (e.g., insists on a title), Claude warns once with specific risks, then proceeds without further resistance.
- **Title-driven topic diagnosis (Stage 0)**: Claude extracts research object, dimensions, time range, and domain from the draft title, runs a FINER evaluation, and surfaces specific issues.
- Warning message template with structured risk enumeration.

---

## [0.1.0] — 2026-03-15

### Added
- Initial skill scaffold with YAML frontmatter (`name`, `description`).
- Stage-Gate model covering Stages 0–6: Topic Diagnosis → Search Strategy → Data Validation → Chapter Structure → Section Drafting → Polish & Integration → Journal Targeting.
- `PROJECT_STATE.md` mechanism for session-persistent project state.
- Gate conditions for each stage transition.
- Stage 0 FINER framework evaluation template.
- Stage 1 WoS/Scopus query string design and PRISMA flow guidance.
- Stage 3 chapter structure templates for both Type A and Type B articles.
- Stage 6 journal recommendation logic.
