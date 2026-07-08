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
├── index.html                         # Landing page (3 topic cards + quick links)
├── masvs.html                         # MASVS v2.1.0 cheat sheet (8 groups, 24 controls)
├── maswe.html                          # MASWE cheat sheet (8 groups, 119 weaknesses)
├── mastg-index.html                   # MASTG sub-index (links to MASTG files)
├── mastg-tests-android.html          # MASTG Android V2 tests (112 + orphan V1)
├── mastg-tests-ios.html              # MASTG iOS V2 tests (88 + orphan V1)
├── mastg-tools-android.html           # MASTG Android tools (48)
├── mastg-tools-ios.html               # MASTG iOS tools (54)
├── mastg-tools-generic.html           # MASTG generic + network tools (33)
├── mastg-techniques-android.html      # MASTG Android techniques (78)
├── assets/
│   ├── masvs_cover.png                # MASVS book cover image
│   ├── maswe_cover.png                # MASWE book cover image
│   └── mastg_cover.png                # MASTG book cover image
└── skills/
    └── owasp-mas-design/
        └── SKILL.md                   # Design system for HTML cheat sheets
```

## Content Conventions

- **Description text**: Bahasa Indonesia (group descriptions, item descriptions)
- **Control/weakness text**: English (as per OWASP original)
- **Prompt text**: English (for copy-pasting into AI agents)
- **Prompt format**: 3-8 lines, mention platform (Android/iOS), tool names, MASTG references, code examples in Kotlin/Swift
- **No "Generated:" timestamps** in any HTML footer — only source URL and disclaimer

## Landing Page Cover Image Design (FINAL — do not change)

The `index.html` landing page uses cover images as **full-bleed card backgrounds** with these locked settings:

- `object-fit: cover` + `object-position: top center` — image fills entire card, no gaps
- Card background: gradient per topic (MASVS green-teal, MASWE teal-green, MASTG blue)
- Overlay: bottom 50% only, gradient transparent → semi-dark for text readability
- No `<h2>` title in card body (cover image already contains the title)
- Card body: label badge + description + meta tags, white text, positioned at bottom
- `min-height: 480px` per card

**Do not change this approach.** It has been verified and approved by the user.

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
| Landing page | `index.html` |
| MASVS Summary | `masvs.html` |
| MASWE Summary | `maswe.html` |
| MASTG Sub-index | `mastg-index.html` |
| MASTG Android Tests | `mastg-tests-android.html` |
| MASTG iOS Tests | `mastg-tests-ios.html` |
| MASTG Android Tools | `mastg-tools-android.html` |
| MASTG iOS Tools | `mastg-tools-ios.html` |
| MASTG Generic Tools | `mastg-tools-generic.html` |
| MASTG Android Techniques | `mastg-techniques-android.html` |

## Current Status

- [x] `index.html` — done (landing page with 3 topic cards + quick links)
- [x] `masvs.html` — done (24 controls, 8 groups)
- [x] `maswe.html` — done (119 weaknesses, 8 groups)
- [x] `mastg-index.html` — done (sub-index for MASTG)
- [x] `mastg-tests-android.html` — done (112 V2 + orphan V1, 0 Untitled, 0 empty IDs)
- [x] `mastg-tests-ios.html` — done (88 V2 + orphan V1, 0 Untitled, 0 empty IDs)
- [x] `mastg-tools-android.html` — done (48 tools)
- [x] `mastg-tools-ios.html` — done (54 tools)
- [x] `mastg-tools-generic.html` — done (33 tools)
- [x] `mastg-techniques-android.html` — done (78 techniques)
- [ ] `mastg-techniques-ios.html` — todo (only if explicitly requested)
- [ ] `mastg-demos.html` — todo (only if explicitly requested)
- [ ] `mastg-best-practices.html` — todo (only if explicitly requested)
- [ ] `mastg-knowledge.html` — todo (only if explicitly requested)

## Target Audience

Mobile engineers (primarily Android/iOS) preparing for:
- Mobile security role interviews (e.g., Verihubs Mobile Platform & Security Engineer)
- Quick reference for OWASP MAS controls/weaknesses/tests
- Self-directed learning of mobile app security