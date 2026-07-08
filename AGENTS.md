# AGENTS.md — owasp-mas-cheat-sheet

## Project Overview

This repo contains **interactive HTML cheat sheets** for the OWASP MAS (Mobile Application Security) project. Target audience: mobile engineers who want to quickly catch up with OWASP MAS standards (MASVS, MASWE, MASTG).

Each cheat sheet is a **single-file HTML artifact** — self-contained, no external dependencies, opens directly in any browser.

## Repo Structure

```
owasp-mas-cheat-sheet/
├── AGENTS.md                          # This file — project context for AI agents
├── README.md                          # Public repo description
├── LICENSE                            # License file
├── masvs.html                         # MASVS v2.1.0 cheat sheet (8 groups, 24 controls)
├── maswe.html                         # MASWE cheat sheet (8 groups, 119 weaknesses)
├── mastg.html                         # MASTG cheat sheet (TODO)
└── skills/
    └── owasp-mas-design/
        └── SKILL.md                   # Design system for HTML cheat sheets
```

## Content Conventions

- **Description text**: Bahasa Indonesia (group descriptions, item descriptions)
- **Control/weakness text**: English (as per OWASP original)
- **Prompt text**: English (for copy-pasting into AI agents)
- **Prompt format**: 3-8 lines, mention platform (Android/iOS), tool names, MASTG references, code examples in Kotlin/Swift

## Data Sources

| Artifact | Source | URL |
|----------|--------|-----|
| MASVS | OWASP MASVS v2.1.0 PDF + GitHub | https://github.com/OWASP/masvs |
| MASWE | OWASP MASWE GitHub (branch: main) | https://github.com/OWASP/maswe |
| MASTG | OWASP MASTG GitHub (branch: master) | https://github.com/OWASP/owasp-mastg |

Relevant MASTG data:
- 200 V2 test cases (tests-beta/) — 112 Android + 88 iOS
- 167 techniques — 78 Android + 76 iOS + 13 generic
- 135 tools — 48 Android + 54 iOS + 22 generic + 11 network

## Skill: owasp-mas-design

Before creating or editing any HTML cheat sheet, **load the skill**:

```
skill_view(name='owasp-mas-design')
```

The skill contains:
- Color palette (OWASP brand colors, profile/status badge colors)
- Typography rules
- Layout structure (page shell, container, collapsible groups)
- Component specs (item card, badges, prompt box, search & filter bar)
- Animation patterns
- JavaScript patterns (group toggle, prompt toggle, copy clipboard, search & filter)
- Data attributes for filtering (`data-id`, `data-category`, `data-profiles`, `data-status`, `data-platform`)
- Content rules (prompt format, description length)
- Accessibility requirements
- File naming convention
- 12-point verification checklist

## Workflow: Add a New Cheat Sheet

1. **Load skill**: `skill_view(name='owasp-mas-design')` — get the design system
2. **Collect data**: Fetch from OWASP GitHub repos (MASVS/MASWE/MASTG)
3. **Generate HTML**: Single-file, self-contained, follow SKILL.md spec
4. **Verify checklist**: Run the 12-point checklist in SKILL.md section 14
5. **Test**: Open in a browser, ensure collapsible, copy button, search & filter (if applicable) work

## File Naming Convention

| Artifact | Filename |
|----------|----------|
| MASVS Summary | `masvs.html` |
| MASWE Summary | `maswe.html` |
| MASTG Tests | `mastg.html` |
| MASTG Tools | `mastg-tools.html` (optional) |

## Current Status

- [x] `masvs.html` — done (24 controls, 8 groups)
- [x] `maswe.html` — done (119 weaknesses, 8 groups)
- [ ] `mastg.html` — todo (200 V2 tests + 167 techniques + 135 tools, needs filtering to critical ones)
- [ ] `mastg-tools.html` — optional

## Target Audience

Mobile engineers (primarily Android/iOS) preparing for:
- Mobile security role interviews (e.g., Verihubs Mobile Platform & Security Engineer)
- Quick reference for OWASP MAS controls/weaknesses/tests
- Self-directed learning of mobile app security