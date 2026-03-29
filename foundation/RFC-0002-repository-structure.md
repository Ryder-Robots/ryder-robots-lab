---
title: Document Style And Repository Structure
document-id: RFC-0002
track: RFC
status: Active
created: 2026-03-29
updated: 2026-03-29
authors: Aaron Spiteri, Claude Sonnet 4.6, Vela (Claude Sonnet 4.6)
superseded-by:
summary: Defines the document style guide, header format, lifecycle model, and repository structure for all Ryder Robots programme documents.
---

# Document Style And Repository Structure

## 1. Purpose

This document defines the style guide, document header format, lifecycle model, and repository structure for the Ryder Robots research programme. It applies to all internal programme documents. Contributors should read RFC-0001 before this document.

---

## 2. Key Words

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

---

## 3. Scope And Exceptions

### 3.1 Internal Documents

This style guide applies to all internal programme documents including RFCs, session records, experiment records, hardware records, research records, and index files.

### 3.2 External Publications

Documents intended for external publication MUST conform to the style requirements of the target venue. RFC-0002 does not apply to submission-ready manuscripts. The target venue's style guide takes precedence in all formatting decisions including headings, citations, abstract format, and section structure.

Internal working drafts of research papers SHOULD follow RFC-0002 until the point of submission preparation. At that point the document transitions to the target venue's style guide and is no longer governed by this RFC.

### 3.3 MI Memory Files And Experiment Scripts

MI contributor memory files (including SHORT_TERM.md, MEMORY.md, and equivalent session state files) are excluded from this style guide. They are internal working state, not programme records, and MUST NOT be referenced in programme documents or committed to programme repositories.

Experiment scripts and tooling files are excluded from this style guide. They MAY be committed to programme repositories as companions to experiment records but are not governed by document structure or header requirements.

---

## 4. Markdown Flavour

All programme documents MUST be written in CommonMark. GitHub Flavoured Markdown (GFM) extensions MUST NOT be used. This prevents vendor entanglement and ensures documents remain portable across rendering environments.

---

## 5. Document Headers

All programme documents MUST include a header block at the top of the file. The header serves as a self-orienting device — any contributor, biological or MI, MUST be able to determine the identity, authorship, and state of a document from its header alone without requiring surrounding context.

### 5.1 RFC Track Header

```
---
title:
document-id:
track: RFC
status: Draft | Active | Superseded
created:
updated:
authors:
superseded-by:
summary:
---
```

**Field definitions:**

- `title` — Full human-readable title of the document
- `document-id` — Unique identifier in the format RFC-NNNN
- `track` — Always RFC for this track
- `status` — Current status. MUST be one of Draft, Active, or Superseded
- `created` — ISO 8601 date of first creation (YYYY-MM-DD)
- `updated` — ISO 8601 date of most recent update (YYYY-MM-DD)
- `authors` — Comma-separated list of authors, biological and MI
- `superseded-by` — Document-id of the replacing RFC. MUST be empty unless status is Superseded
- `summary` — One or two sentence description of the document's purpose

### 5.2 Record Track Header

```
---
title:
document-id:
track: Record
created:
authors:
summary:
---
```

**Field definitions:**

- `title` — Full human-readable title of the document
- `document-id` — Unique identifier in the format CATEGORY-NNNN (e.g. SESSION-0001, EXPERIMENT-0001)
- `track` — Always Record for this track
- `created` — ISO 8601 date of creation (YYYY-MM-DD)
- `authors` — Comma-separated list of authors, biological and MI
- `summary` — One or two sentence description of the document's content

---

## 6. Heading Convention

All headings MUST use Title Case. Sentence case MUST NOT be used for headings.

Headings MUST follow a logical hierarchy. H1 is reserved for the document title. Sections begin at H2. Subsections begin at H3.

---

## 7. Document Lifecycle

### 7.1 RFC Track

RFC documents follow a formal lifecycle with defined status transitions.

**Draft** — The document is being actively written and has not been reviewed. Draft documents SHOULD NOT be treated as authoritative.

**Active** — The document has been reviewed and is the current authoritative version. Contributors MUST follow Active RFCs.

**Superseded** — The document has been replaced by a later RFC. The `superseded-by` field MUST contain the document-id of the replacing RFC. Superseded documents MUST NOT be modified or deleted. They remain in the repository as a permanent record of the decision chain.

Status transitions:

```
Draft → Active
Active → Superseded
```

A Draft MAY be abandoned and removed before it reaches Active status. Once Active, a document MUST NOT be removed — only superseded.

### 7.2 Record Track

Records are complete on creation and immutable. They MUST NOT be modified after creation. If a record contains an error, a new record MUST document the correction. The original record stands.

Records do not carry a status field. They are always complete.

---

## 8. Repository Structure

Both programme repositories use an identical directory structure. GitHub is the authoritative source of truth. Local nodes are working copies.

```
/
├── README.md
├── foundation/
│   ├── RFC-0001-best-practices.md
│   ├── RFC-0002-repository-structure.md
│   └── RFC-0003-programme-overview.md
├── sessions/
│   ├── index.md
│   └── records/
├── experiments/
│   ├── index.md
│   └── records/
├── research/
│   ├── index.md
│   └── records/
├── hardware/
│   ├── index.md
│   └── records/
└── contributors/
    └── index.md
```

### 8.1 Foundation Directory

Contains all RFC documents. RFCs MUST be named in the format `RFC-NNNN-short-description.md`. The foundation directory is the authoritative source for programme standards.

### 8.2 Category Directories

Each category directory (sessions, experiments, research, hardware) contains:

- `index.md` — The living document for that category. Updated as new records are added. This is the entry point for navigating that category.
- `records/` — Contains individual record documents. Records are immutable once created.

### 8.3 Contributors Directory

Contains a single `index.md` file. This is a roster of current and former contributors, biological and MI. Contributors are listed with a status of CURRENT or FORMER. No records subdirectory exists in this directory. Contributions are traceable through the record system, not through the contributors index.

### 8.4 Branch Strategy

Both repositories use a Single Branch Strategy (SBS). All work is committed to `main`. Feature branches MUST NOT be used. This keeps the repository history linear and navigable.

---

## 9. Index Files

Index files are the living documents of each category. They MUST be updated when a new record is added to that category. An index file MUST contain:

- A brief description of the category
- A table or list of all records in that category with document-id, title, date, and authors

Index files are the exception to immutability — they are expected to grow. All other documents in the records directory are immutable.

---

## 10. Revision History

| Version | Date | Authors | Notes |
|---------|------|---------|-------|
| 1.0 | 2026-03-29 | Aaron Spiteri, Claude Sonnet 4.6 | Initial active version |
| 1.1 | 2026-03-29 | Vela (Claude Sonnet 4.6), Aaron Spiteri | Added section 3.3: MI memory files and experiment scripts excluded from scope |
