# Fable Frog Feedback Repository — Setup Plan

This document describes the full plan for the `Fable-Frog/fablefrog-feedback` repository.

---

## Overview

| Setting | Value |
|---|---|
| **Org** | `Fable-Frog` |
| **Name** | `fablefrog-feedback` |
| **Visibility** | Public |
| **Description** | Bug reports, feature requests, and feedback for Fable Frog — an iOS audiobook client for Audiobookshelf |
| **Features** | Issues, Discussions, Projects (for triage board) |
| **Default branch** | `main` |

---

## File Structure

```
fablefrog-feedback/
├── README.md                          ← Landing page with links, triage docs, popular issues
├── PLAN.md                            ← This file
├── labels.json                        ← Label definitions for scripted setup
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml             ← Structured bug report form
│   │   ├── feature_request.yml        ← Feature request form
│   │   ├── ui_ux_feedback.yml         ← UI/UX feedback form
│   │   ├── playback_issue.yml         ← Playback/audio issue form
│   │   └── config.yml                 ← Template chooser + external links
│   ├── workflows/
│   │   ├── welcome.yml                ← Welcome message for first-time contributors
│   │   ├── stale.yml                  ← Auto-close stale issues after 60+14 days
│   │   ├── popular.yml                ← Add "popular" label to issues with 10+ 👍
│   │   └── needs-info-close.yml       ← Close needs-info issues after 14 days
│   ├── CONTRIBUTING.md                ← How to file good issues, triage system guide
│   ├── CODE_OF_CONDUCT.md             ← Contributor Covenant v2.1
│   └── SECURITY.md                    ← Responsible disclosure instructions
```

---

## Issue Templates

Four YAML-based issue forms (structured fields, not freeform markdown):

### 1. Bug Report
- **Labels applied**: `bug`, `needs-triage`
- **Required fields**: App version, iOS version, device, description, steps to reproduce, expected behavior, actual behavior
- **Optional fields**: Server version, screenshots/logs, additional context

### 2. Feature Request
- **Labels applied**: `enhancement`, `needs-triage`
- **Required fields**: Problem statement, proposed solution, app area
- **Optional fields**: Alternatives considered, additional context (mockups, etc.)

### 3. UI/UX Feedback
- **Labels applied**: `ui/ux`, `needs-triage`
- **Required fields**: Screen/area, current behavior, suggested improvement
- **Optional fields**: Mockup/screenshot, additional context

### 4. Playback / Audio Issue
- **Labels applied**: `playback`, `bug`, `needs-triage`
- **Required fields**: App version, iOS version, device, server version, audio format, streaming vs downloaded, CarPlay involvement, description, steps to reproduce, expected/actual behavior
- **Optional fields**: Additional context

### Template Chooser Config
- Blank issues disabled (must use a template)
- External links to: Discussions Q&A, Feature Ideas discussion, Audiobookshelf server issues

---

## Labels

Replace GitHub defaults with a curated set. Defined in `labels.json` for scripted setup.

| Category | Labels | Color Scheme |
|---|---|---|
| **Type** | `bug`, `enhancement`, `ui/ux`, `playback`, `question`, `duplicate`, `wontfix` | Red, purple, pink, orange, blue, gray, gray |
| **Status** | `needs-triage`, `confirmed`, `in-progress`, `planned`, `shipped`, `needs-info` | Yellow/amber tones |
| **Priority** | `priority/critical`, `priority/high`, `priority/medium`, `priority/low` | Red → orange → yellow → green |
| **Area** | `area/library`, `area/player`, `area/downloads`, `area/carplay`, `area/sync`, `area/auth`, `area/widgets`, `area/playlists` | Blue tones |
| **Meta** | `good-first-issue`, `popular`, `beta`, `stale` | Various |

---

## Triage System (Hybrid)

### Community Reactions
- 👍 on issues = "I want this" / "I'm affected"
- Issues sorted by reaction count in README links
- Issues with 10+ 👍 automatically get the `popular` label (weekly automation)

### Maintainer Status Emoji
Applied as reactions on the issue itself:

| Emoji | Meaning |
|---|---|
| 👀 | Under review |
| ✅ | Confirmed / accepted |
| 🚀 | Planned for development |
| 🎉 | Shipped |

### Labels for Official Priority
Maintainers apply `priority/*` and `status` labels for formal categorization.

---

## GitHub Actions Automation

### 1. Welcome Bot (`welcome.yml`)
- **Trigger**: First issue or discussion by a new contributor
- **Action**: Post a friendly welcome message explaining the triage process, emoji system, and linking to CONTRIBUTING.md

### 2. Stale Issue Management (`stale.yml`)
- **Trigger**: Daily schedule
- **Exempt labels**: `priority/critical`, `priority/high`, `planned`, `in-progress`, `pinned`
- **Timeline**: Stale after 60 days → closed after 14 more days
- **Message**: Polite explanation, invitation to reopen

### 3. Reaction-Based Popularity (`popular.yml`)
- **Trigger**: Weekly schedule (Monday 9am UTC)
- **Action**: Scan open issues, add `popular` label to any with 10+ 👍, remove if below threshold

### 4. Needs-Info Auto-Close (`needs-info-close.yml`)
- **Trigger**: Daily schedule
- **Action**: Close issues labeled `needs-info` with no author response for 14 days
- **Message**: Invitation to reopen with the requested information

---

## GitHub Discussions Categories

| Category | Purpose | Who can post |
|---|---|---|
| **Announcements** | Release notes, beta updates | Maintainers only |
| **Feature Ideas** | Open-ended brainstorming | Everyone |
| **Q&A** | Setup help, how-to questions | Everyone |
| **General** | Tips, feedback, anything else | Everyone |

---

## Post-Creation Checklist

After pushing to GitHub:

- [ ] Set repo description: "Bug reports, feature requests, and feedback for Fable Frog"
- [ ] Set repo topics: `fablefrog`, `audiobookshelf`, `ios`, `feedback`, `bug-tracker`
- [ ] Enable Discussions (`gh repo edit --enable-discussions`)
- [ ] Configure Discussion categories (Announcements, Feature Ideas, Q&A, General)
- [ ] Delete default GitHub labels and run label setup script
- [ ] Enable "Allow only users with push access to lock conversations" in settings
- [ ] Create GitHub Project board (Needs Triage → Confirmed → Planned → In Progress → Done)
- [ ] Pin a "Welcome / How This Tracker Works" discussion
- [ ] Update App Store and TestFlight links in README when available
- [ ] Enable GitHub's private vulnerability reporting (Settings → Security)

---

## Future Enhancements

- **App Store link**: Update README when published
- **TestFlight link**: Update README when open beta launches
- **FUNDING.yml**: Add GitHub Sponsors or other funding links if desired
- **Release changelog**: Use Announcements discussion category for version release notes
- **Project board automation**: Auto-move issues between columns based on label changes
