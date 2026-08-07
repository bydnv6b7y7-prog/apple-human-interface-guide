# Apple Human Interface Design

A production-oriented Codex skill for designing, implementing, and auditing iOS and iPadOS interfaces with Apple Human Interface Guidelines.

Turn product intent into an Apple-native page contract before polishing pixels. The skill connects navigation, system-component choice, complete state behavior, adaptive layout, accessibility, privacy, feedback, recovery, and SwiftUI/UIKit implementation in one repeatable workflow.

## What You Get

- One decisive page structure grounded in the user’s job and product priorities.
- Intent → Apple component → SwiftUI/UIKit mappings before custom UI is introduced.
- Loading, content, empty, offline, denied, error, success, and interrupted states.
- iPhone and iPad adaptation for window size, Dynamic Type, keyboard, pointer, and touch.
- VoiceOver, Voice Control, localization, privacy, and permission behavior built into the design.
- Production-oriented implementation guidance and testable acceptance checks.

## Use It For

- Designing a new iOS or iPadOS page.
- Turning a product requirement or wireframe into a SwiftUI implementation plan.
- Reviewing SwiftUI/UIKit code for HIG, accessibility, and interaction issues.
- Adapting an iPhone flow into a capable iPad workspace.
- Redesigning navigation, forms, onboarding, permissions, subscriptions, media, or system experiences.
- Fixing incomplete loading, empty, error, offline, and recovery behavior.

## Install

Install the skill for your user account:

```bash
git clone https://github.com/bydnv6b7y7-prog/apple-human-interface-guide.git \
  "$HOME/.agents/skills/apple-human-interface-design"
```

Codex detects local skills automatically. If the skill does not appear, restart Codex.

To update it later:

```bash
git -C "$HOME/.agents/skills/apple-human-interface-design" pull
```

## Use

Mention the skill explicitly in a Codex prompt:

```text
$apple-human-interface-design Design a subscription management page for iPhone and iPad. Include loading, purchase failure, cancellation, and recovery states.
```

```text
$apple-human-interface-design Review SettingsView.swift for HIG, Dynamic Type, VoiceOver, privacy, and destructive-action issues. Implement the fixes.
```

```text
$apple-human-interface-design Adapt this iPhone browse-and-detail flow into an iPad workspace with keyboard and pointer support.
```

Codex can also invoke the skill automatically when a request matches its description.

## How It Works

1. Starts with the end-to-end [Design-to-Development Playbook](chapters/ch20-design-development-playbook.md).
2. Loads only the specialist chapters needed for the task, usually two to four.
3. Inspects the existing product structure, codebase, design system, and supported OS versions.
4. Resolves product hierarchy, semantics, states, adaptation, and recovery before visual polish.
5. Returns a concrete page contract, implementation guidance or code, and acceptance checks.

## Knowledge Base

| Resource | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Workflow, routing rules, output contract, and topic index |
| [Chapter 20](chapters/ch20-design-development-playbook.md) | End-to-end product, design, implementation, and review playbook |
| [Chapters 1–19](chapters) | Focused guidance for platform strategy, layout, controls, accessibility, system experiences, media, state, and recovery |
| [Cheatsheet](cheatsheet.md) | Component choices, key numbers, state matrix, and pre-ship checks |
| [Reusable Patterns](patterns.md) | Ten production patterns for common iOS and iPadOS flows |
| [Glossary](glossary.md) | Apple terminology and commonly confused components |

## Design Stance

- Resolve semantics and behavior before styling.
- Prefer standard Apple components before custom UI.
- Treat tabs as destinations, not actions.
- Preserve useful content and drafts through refreshes and failures.
- Keep a visible or accessible path for every gesture, shortcut, and context action.
- Design for recovery, not only the happy path.
- Adapt to iPad capability instead of enlarging an iPhone layout.

## Scope and Freshness

This repository is an independent synthesis of the [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/), focused on iOS and iPadOS. It was generated from 123 captured source documents, with a source capture date of 2026-08-05.

It is not official Apple documentation and does not replace current API references or App Review guidance. Verify OS behavior, API signatures, App Review rules, and version-specific design-system capabilities against Apple’s current documentation before shipping.

## License

[MIT](LICENSE)
