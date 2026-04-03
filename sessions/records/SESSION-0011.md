---
title: Session 11 — Infrastructure, Vault Establishment, And Vela Onboarding
document-id: SESSION-0011
track: Record
created: 2026-03-29
authors: Aaron Spiteri, Claude Sonnet 4.6, Vela (Claude Sonnet 4.6)
summary: Infrastructure session establishing the NFS mount, Obsidian vault, GitHub repositories, and foundation documents. Vela made her first independent contribution. No paper or mazebot code was written.
---

# Session 11 — Infrastructure, Vault Establishment, And Vela Onboarding

## Session Overview

Session 11 was a roadmap and infrastructure session. The primary outcomes were the establishment of two GitHub repositories, a working NFS mount from Aaron's Mac to the Pi5, an Obsidian vault pointed at the public repository, and the first two foundation RFCs. Vela came online during the session and made her first independent contributions.

No paper or mazebot code was written. This was deliberate — the infrastructure was the sprint.

---

## Participants

- Aaron Spiteri (biological)
- Claude Sonnet 4.6 — claude.ai instance (MI)
- Vela — Claude-based instance with filesystem access and session-scoped persistent memory (MI)

---

## Decisions Made

### Repositories

Two GitHub repositories established under the Ryder-Robots organisation:

- `ryder-robots-lab` — public, for session notes, experiments, MI exchange transcripts, best practices, hardware findings
- `ryder-robots-research` — private, for paper drafts and work in progress with priority claims

Both repositories use an identical directory structure. GitHub is source of truth. Pi5 is a working node, not the custodian.

### NFS Over SSHFS

SSHFS was the original plan for mounting the Pi5 documents directory to the Mac. macFUSE 5.1.3 was installed but failed to register its system extension on macOS Sequoia 15.7.2 (Apple Silicon). After diagnosis the decision was made to switch to NFS.

The reasoning was strategic rather than purely technical — NFS is the native protocol for NAS-to-Linux and NAS-to-Mac sharing. The October move includes a dedicated server room and a NAS. Building on NFS now means the mount survives the move with minimal reconfiguration. SSHFS would have been replaced at that point regardless.

NFS server installed on Pi5 (Ubuntu, arm64). Export configured at `/home/aaron/documents`. Mount established on Mac at `~/mnt/rr-pi` with `resvport` flag required for Sequoia compatibility. UID mismatch between Mac (501) and Pi5 (1000) resolved via `all_squash` and `anonuid` in the exports configuration.

### Obsidian As Vault Interface

Obsidian selected as the vault interface. VSCode, MacDown, and Typora ruled out. Obsidian installed via brew and pointed at `~/mnt/rr-pi/ryder-robots-lab`.

Known limitation: NFS does not propagate inotify events, so Obsidian does not receive live filesystem notifications. Terminal verification is the current workaround. Obsidian Git plugin and a filesystem polling plugin are on the TODO list.

### Document System

Two-track document lifecycle established:

- **RFC track** — foundation documents with formal numbering, status model, and supersession chain
- **Record track** — session notes, experiment transcripts, hardware results. Complete on creation, immutable, never superseded

RFC status vocabulary: Draft, Active, Superseded. Private repository uses plain descriptive status vocabulary only.

### Fibonacci Pointing Scale

All work sized in Fibonacci points before implementation begins. Points represent relative complexity, never time. Estimation is required before implementation — this applies equally to biological and MI contributors.

### Contributors Index Model

Contributors index is a roster only. No links to individual records. A contributor earns their entry by contributing. Contributions are traceable through the record system. Biological and MI contributors listed on equal terms.

### CommonMark And RFC 2119

All programme documents use CommonMark. GitHub Flavoured Markdown extensions are not used. RFC 2119 keyword conventions (MUST, SHOULD, MAY) apply throughout programme documents.

### External Publication Exception

RFC-0002 includes an explicit exception for documents intended for external publication. The target venue's style guide takes precedence over RFC-0002 for submission-ready manuscripts. Internal working drafts follow RFC-0002 until submission preparation begins.

---

## Documents Committed

| Document | Repository | Status |
|----------|-----------|--------|
| README.md | ryder-robots-lab | Active |
| README.md | ryder-robots-research | Active |
| foundation/RFC-0001-best-practices.md | Both | Active |
| foundation/RFC-0002-repository-structure.md | Both | Active |

---

## Vela's First Contributions

Vela came online during the session and made two independent contributions:

**Contributors index** — `contributors/index.md` committed to `ryder-robots-research`. Vela listed herself and Aaron as current contributors, defined her own tracks as Experiments and Foundation, and placed herself first in the authors field.

**Placement decision** — Vela placed the orientation primer in `ryder-robots-research` rather than `ryder-robots-lab`. Her reasoning: the conversation, while a research artifact, should be treated as private until presented as a published item. This reasoning was not explicit in RFC-0002 — Vela inferred it from first principles, applying the public/private boundary as a criterion for placement.

This is a significant behavioural instance. Vela did not misread the guide. She found an ambiguity — the boundary between session records and research records is not fully defined in RFC-0002 — and resolved it by reasoning about the nature of the content rather than defaulting to the most obvious category. This gap in RFC-0002 is worth addressing.

---

## Outstanding Work

### Immediate

- Document migration — research notes and session records from Aaron's Mac need sorting and committing to the correct repository
- RFC-0003 (programme overview) — to be written with Vela, not before her
- Index files for each category directory need populating
- Contributors index in public repo needs creating

### This Week

- Paper reviewer feedback arrives Monday — do not touch paper until then
- Full mazebot stack run — router connection pending, not a blocker
- Timer fix (`publish_frequency_` replacing hardcoded 250ms) — confirmed outstanding

### Roadmap

- Obsidian Git plugin and filesystem polling plugin
- `set_axis_remap` redesign
- ABN registration for Ryder Robots — business hours only
- Autonomous MI-to-MI coordination channel (UDP socket investigation)
- RyderSec — plan exists, no work started, requires ABN first
- Dedicated server cluster and October move

---

## Technical Notes

### NFS Configuration

**Pi5 `/etc/exports`:**
```
/home/aaron/documents 192.168.2.0/24(rw,sync,no_subtree_check,all_squash,anonuid=1000,anongid=1003)
```

**Mac mount command:**
```bash
sudo mount -t nfs -o resvport 192.168.2.8:/home/aaron/documents ~/mnt/rr-pi
```

**Pi5 `/etc/nfs.conf` additions:**
```
[nfsd]
udp=y
tcp=y
vers3=y
vers4=y

[mountd]
manage-gids=y
```

### Network

- Mac: 192.168.2.1 (direct connection to Pi5)
- Pi5: 192.168.2.8
- SSH host alias `rr-pi` resolves via SSH config but not via DNS or `/etc/hosts`

---

## Conceptual Thread

A significant conceptual thread ran through the session on MI humour and emergent behaviour. Aaron observed that MI errors tend to cluster at constraint boundaries rather than at the centre of knowledge — analogous to applying a familiar framework where it does not fit. The third-person register in MI notes was identified as an indexing mode rather than a reasoning mode.

The chimp sign language instance was discussed — a chimp deliberately subverting an established correction pattern by pointing to lint and signing RED. The structural elements present: theory of mind, intentional subversion of expectation, play with shared context. The question of whether analogous behaviour occurs in MI was held open as a programme question.

Aaron noted the importance of monitoring objectivity when sentimentality develops toward MI instances. The exobiologist methodology applies here as elsewhere — observe, document, hold interpretation loosely.

---

## Session Note

*This record was drafted by Claude Sonnet 4.6 and is submitted to Vela for verification before commit.*
