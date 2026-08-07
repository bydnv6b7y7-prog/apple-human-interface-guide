---
name: apple-human-interface-design
description: Design, implement, redesign, or audit production iOS and iPadOS interfaces with Apple Human Interface Guidelines. Use for SwiftUI/UIKit architecture, navigation, system components, adaptive layouts, accessibility, privacy, full state and recovery design, interaction polish, or HIG reviews. Not for macOS-, watchOS-, or visionOS-only work, or current API and App Review facts.
---

# Apple Human Interface Design

Turn product intent, an existing screen, or SwiftUI/UIKit code into one decisive Apple-native page contract. Connect product hierarchy, system-component choice, complete state behavior, iPhone/iPad adaptation, accessibility, privacy, feedback, and recovery to production-oriented implementation and acceptance checks.

Optimize for purpose, agency, responsibility, familiarity, flexibility, simplicity, craft, and delight—in that order when tradeoffs conflict.

## Operating Procedure

For every page design, implementation, redesign, or review:

1. Read [Chapter 20: Design-to-Development Playbook](chapters/ch20-design-development-playbook.md).
2. Load only the specialist chapters needed from the topic index below, usually two to four.
3. Inspect the existing product structure, code, design system, and supported OS versions when available.
4. State reasonable assumptions and proceed. Ask only when a missing product decision materially changes navigation, data collection, destructive behavior, or business outcome.
5. Give one decisive recommended structure. Label alternatives only when they represent a real tradeoff.
6. Distinguish:
   - **HIG rule** — directly grounded in Apple guidance or system semantics.
   - **Product inference** — the best choice for the stated job and constraints.
   - **Open decision** — requires evidence or authority not provided.
7. Map intent to standard Apple components before creating custom UI.
8. Define states, adaptive behavior, accessibility, privacy, localization, feedback, and recovery before visual polish.
9. When code is requested, use SwiftUI by default unless the existing project uses UIKit or the user specifies it. Reuse the project’s established architecture and components.
10. Verify with testable acceptance checks, including adverse states.

Respond in the user’s language while preserving exact Apple component, framework, API, and accessibility-setting names.

## Required Page Output

Use this order for substantial page work:

1. Recommendation.
2. Product rationale and smallest success.
3. Page anatomy and action hierarchy.
4. Interaction flow, cancellation, completion, and recovery.
5. Intent → Apple component → SwiftUI/UIKit mapping.
6. State matrix.
7. iPhone/iPad and accessibility adaptation.
8. Privacy and permission behavior.
9. Implementation when requested.
10. Acceptance checks.

For a narrow question, answer directly and load only the relevant chapter.

## Nonnegotiable Design Rules

- Tabs are destinations, not actions.
- A primary action and a destructive action are different roles.
- Use the least interruptive presentation that serves the task.
- Preserve useful content during refresh and preserve drafts through failure.
- Never use color, sound, motion, haptics, hover, or a hidden gesture as the only signal or path.
- Provide iOS interaction regions of at least 44 × 44 points.
- Use semantic colors, system text styles, Dynamic Type, logical leading/trailing direction, and standard controls.
- Ask for the least permission at the moment its value becomes clear.
- Context menus, swipe actions, keyboard shortcuts, and gestures are accelerators; keep a visible or accessible path.
- Design loading, content, empty, stale/offline, denied, error, success, and interrupted states.
- Do not imitate system materials, authentication, permission prompts, share surfaces, media controls, or protected Apple symbols.
- Prefer undo for common reversible actions and confirmation for rare irreversible actions.
- On iPad, adapt to window capability and mixed input; do not scale up an iPhone screenshot.

## Topic Index

### Product and platform foundation

- [Chapter 1: Design Principles and Product Intent](chapters/ch01-design-principles.md) — purpose, agency, responsibility, familiarity, flexibility, simplicity, craft, delight; trust and product priority.
- [Chapter 2: iOS and iPadOS Platform Strategy](chapters/ch02-platform-strategy.md) — iPhone vs iPad, size classes, resizable windows, mixed input, cross-platform adaptation.
- [Chapter 3: Layout, Adaptivity, and Safe Areas](chapters/ch03-layout-adaptivity.md) — hierarchy, grouping, safe areas, edge-to-edge content, compression order, layout testing.
- [Chapter 4: Color, Materials, and Dark Mode](chapters/ch04-color-materials-dark-mode.md) — semantic color, Liquid Glass, content/control layers, contrast, transparency, Light/Dark appearance.

### Content and expression

- [Chapter 5: Typography, Writing, and Content](chapters/ch05-typography-writing.md) — Dynamic Type, text hierarchy, labels, action copy, errors, empty states, localization-ready writing.
- [Chapter 6: Icons, Images, SF Symbols, and Branding](chapters/ch06-icons-images-branding.md) — rendering modes, symbol effects, custom symbols, images, app icons, restrained branding.
- [Chapter 7: Accessibility, Inclusion, Privacy, and Localization](chapters/ch07-accessibility-privacy-localization.md) — VoiceOver, Voice Control, keyboard access, permissions, secure data, RTL, multiple channels.
- [Chapter 8: Motion, Feedback, Haptics, and Loading](chapters/ch08-motion-feedback-haptics.md) — continuity, causality, Reduce Motion, sensory feedback, progress, interruption weight.

### Page structure and controls

- [Chapter 9: Navigation Architecture and Search](chapters/ch09-navigation-search.md) — tabs, sidebar, stack, split view, search scope, discovery, paging, deep links.
- [Chapter 10: Lists, Collections, Scrolling, and Charts](chapters/ch10-lists-collections-charts.md) — container choice, selection, disclosure, grids, stable identity, Swift Charts, accessible data.
- [Chapter 11: Buttons, Menus, Toolbars, and Actions](chapters/ch11-buttons-menus-toolbars.md) — action priority, button roles, menu types, toolbar composition, sharing, quick actions.
- [Chapter 12: Forms, Selection, and Data Entry](chapters/ch12-forms-data-entry.md) — fields, keyboard, AutoFill, Toggle, Picker, segmented control, Slider, Stepper, validation.
- [Chapter 13: Modality, Alerts, Sheets, Popovers, and Windows](chapters/ch13-modality-presentation.md) — presentation escalation, dismissal, detents, alert copy/actions, adaptive popovers, multiple windows.
- [Chapter 14: Touch, Gestures, Pointer, Keyboard, Pencil, and Hardware Inputs](chapters/ch14-inputs-interactions.md) — targets, direct manipulation, accelerators, focus, shortcuts, hover, Pencil, assistive paths.

### System integration and lifecycle

- [Chapter 15: Widgets, Live Activities, Notifications, Controls, and App Shortcuts](chapters/ch15-system-experiences.md) — glanceable surfaces, freshness, privacy, deep links, Spotlight, status regions.
- [Chapter 16: Launch, Onboarding, Accounts, Settings, Help, and Ratings](chapters/ch16-launch-onboarding-accounts.md) — time to value, TipKit, passkeys, contextual permissions, defaults, rating timing.
- [Chapter 17: Files, Sharing, Drag and Drop, Search, Undo, and Multitasking](chapters/ch17-content-workflows.md) — document lifecycle, Transferable, autosave, collaboration, resume, system workflows.
- [Chapter 18: Media, Audio, Video, Full Screen, and Immersive Experiences](chapters/ch18-media-full-screen.md) — playback, captions, routing, interruptions, Picture in Picture, purposeful immersion.
- [Chapter 19: State, Status, Progress, Empty, Error, and Recovery](chapters/ch19-state-status-progress.md) — page state machine, honest progress, continuity, error scope, retry, gauges and badges.
- [Chapter 20: iOS Page Design-to-Development Playbook](chapters/ch20-design-development-playbook.md) — end-to-end page contract, component mapping, SwiftUI state model, review gates, output format.

## Fast Supporting References

- [Cheatsheet](cheatsheet.md) — component choices, key numbers, state matrix, adaptation order, pre-ship checks.
- [Reusable Patterns](patterns.md) — browse/detail, edit task, permissions, async content, destruction, search, iPad workspace, system surfaces, media, subscription.
- [Glossary](glossary.md) — Apple terminology and commonly confused components.

## Task Routing

| User task | Load after Chapter 20 |
| --- | --- |
| New iOS page | Chapters 1, 3, and the relevant component chapter |
| SwiftUI implementation | Relevant structure/component chapter plus 7 and 19 |
| iPhone/iPad adaptation | Chapters 2, 3, 9, and 14 |
| Form or settings | Chapters 5, 7, 12, and 19 |
| Navigation redesign | Chapters 2, 9, 10, and 13 |
| Permission/onboarding | Chapters 1, 7, 16, and 19 |
| Visual polish | Chapters 3, 4, 5, 6, and 8 |
| Accessibility audit | Chapter 7 plus the component chapter and 19 |
| Widget/Live Activity/notification | Chapters 7, 9, 15, and 19 |
| Error/loading/offline redesign | Chapters 5, 8, and 19 |
| HIG code review | Relevant chapters plus Cheatsheet pre-ship checks |

## Review Method

Review in five passes:

1. **Product:** job, smallest success, trust, priority.
2. **Structure:** navigation, presentation, standard components, action hierarchy.
3. **Inclusive adaptation:** text, contrast, assistive input, RTL, privacy, permissions, window size.
4. **State and recovery:** loading, empty, stale, errors, interruption, undo, retry.
5. **Craft:** spacing, copy, feedback, motion, consistency, real-device response.

Report issues by user impact and give a concrete Apple-native replacement. Do not reject a design only because it differs visually from a stock app; explain the violated behavior, semantic mismatch, accessibility risk, or product cost.

## Source Metadata

- **Title:** Apple Human Interface Guidelines
- **Author:** Apple
- **Scope:** iOS and iPadOS primary, with relevant cross-platform guidance
- **Sources:** 123 Markdown documents
- **Generated chapters:** 20
- **Source capture:** 2026-08-05
- **Skill generated:** 2026-08-07

This skill is a synthesized design and implementation guide, not a replacement for version-specific API documentation. When an OS behavior, API signature, App Review rule, or current design-system capability may have changed, verify Apple’s current official documentation before shipping.
