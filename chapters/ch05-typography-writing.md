# Chapter 5: Typography, Writing, and Content

## Core Idea

People experience words and type as one system. Typography establishes hierarchy and reading comfort; writing establishes meaning, expectation, and tone. Both must remain clear when text grows, localization expands, or the situation becomes stressful.

## Frameworks Introduced

### System text styles

Apple platforms provide semantic text styles such as large title, title, headline, body, callout, subheadline, footnote, and caption. They encode hierarchy and participate in Dynamic Type. Select a role by meaning, not by trying to match a screenshot’s point size.

### Interface-copy roles

- **Orientation:** titles, headings, labels, and scope.
- **Action:** buttons, links, menu commands, and next steps.
- **Instruction:** concise guidance needed to continue.
- **Feedback:** status, success, validation, errors, and empty states.
- **Explanation:** optional detail that helps a person decide.

## Key Concepts

### Establish a small, logical hierarchy

Use size, weight, color role, spacing, and placement together. A page normally needs only a few clearly differentiated levels. Too many weights and point sizes create visual noise without improving understanding.

Prefer the system font for body text, captions, controls, and dense interfaces. A custom typeface can express brand in prominent display roles, but it must remain legible, support required scripts and weights, and work with large text and bold-text settings.

### Design for Dynamic Type, not around it

Support text enlargement to at least 200% where feasible, including accessibility categories. Do not lock controls to fixed heights or truncate essential meaning. At large sizes:

- Stack label-value or control-label pairs vertically.
- Reduce columns before reducing text.
- Let rows and controls grow.
- Keep headings visually distinct.
- Allow scrolling while preserving a clear dismissal and primary action.

### Make every word earn its place

Use familiar, specific, plain language. Prefer direct verbs and concrete nouns. Remove throat-clearing, repeated titles, implementation jargon, and text that only narrates what the interface already shows.

Write in a respectful, neutral voice:

- Address the person as “you” when useful.
- Avoid unnecessary “we,” “our,” “my,” and “your” in labels.
- Avoid blame, jokes in serious situations, and idioms that localize poorly.
- Match the interaction term to the device when instruction is unavoidable: tap for touch, click for pointer.

### Label actions by outcome

Buttons and menu commands should predict the result: “Save Draft,” “Share,” “Delete Account,” or “Add Card.” Avoid vague “Yes,” “Submit,” or “OK” when a specific result exists.

For a multistep flow, use consistent progression:

- Get Started for the first commitment.
- Continue or Next while progressing.
- Done, Save, or another result-specific verb at completion.
- Back or Cancel when the person can leave.

If an action requires more input before it completes, a menu command can use an ellipsis according to platform convention.

### Put guidance and errors where the decision happens

Use a persistent field label; do not rely on placeholder text that disappears after typing. Add a hint only when the required format is not obvious.

Validation should:

- Appear near the problem.
- State what needs correction.
- Avoid codes, blame, and generic “invalid” language.
- Preserve the person’s input.
- Be accessible without relying on color.

“Choose a password with at least 8 characters” is more useful than “Invalid password.”

### Empty states should lead somewhere

Explain what belongs in the space and provide the next meaningful action. Do not put critical information only in an empty state because it disappears after content arrives.

## Mental Models

### Scan, understand, act

A person should be able to:

1. Scan headings and labels to find the relevant region.
2. Understand the state and consequence without decoding jargon.
3. Act from a specific, visible verb.

If prose is required to explain a nearby icon or unconventional layout, reconsider the interface.

### The expansion budget

Assume localization may make labels substantially longer and Dynamic Type may make each character larger. Design with flexible containers, alternate stacking, and concise source copy before resorting to truncation.

### Stress copy

Review permission, payment, deletion, health, security, and error copy as if the person were rushed or worried. The language should remain factual, specific, and calm.

## Anti-patterns

- Fixed point sizes and heights for text-bearing controls.
- Placeholder-only form labels.
- All-caps body copy or several nearly indistinguishable weights.
- Long centered paragraphs in task-oriented interfaces.
- Button labels such as “Yes,” “No,” “Submit,” or “Click Here.”
- Error titles such as “Error 329347,” “Oops,” or “Something went wrong” with no recovery.
- Empty-state prose without a next step.
- Explaining standard platform controls in permanent interface text.
- Brand voice that becomes cute, accusatory, or ambiguous during a serious event.

## Implementation Bridge

- Use semantic SwiftUI Font text styles and relative custom fonts rather than fixed sizes.
- Let text wrap and let containers grow; apply line limits only when loss of information is acceptable.
- Use scaled metrics for dimensions that must grow with text.
- Keep the accessibility reading order aligned with the visual hierarchy.
- Test Bold Text, the largest accessibility size, right-to-left layouts, and long strings.
- Centralize product terminology and action labels so equivalent operations use the same words.

## Reference Table

| Content role | Good pattern | Weak pattern |
| --- | --- | --- |
| Page title | Names the object or task | App logo or repeated app name |
| Button | Verb/result: “Save Changes” | Vague: “Submit” |
| Field label | Persistent noun: “Email address” | Placeholder only |
| Validation | “Enter a valid email address” | “Invalid input” |
| Destructive confirmation | Names consequence and exact action | Generic warning |
| Empty state | Meaning plus next step | Decorative slogan only |
| Progress action | “Checking out…” while busy | Unchanged button with hidden spinner |

## Worked Example: Edit Profile Form

The draft has a large brand font for every label, placeholders instead of labels, a “Submit” button, and a red border for invalid biography length.

Reconstruct it:

1. Use a navigation title for “Edit Profile,” system body styles for labels and values, and the brand typeface only where it adds identity without hurting scanning.
2. Keep “Name,” “Pronouns,” and “Bio” labels visible above or beside their fields.
3. Show character guidance before the limit matters; if exceeded, add “Shorten your bio to 160 characters” near the field and expose it to assistive technology.
4. Label the primary action “Save.”
5. Preserve changes if an upload or network operation fails; explain the next step inline.
6. At accessibility text sizes, stack labels and inputs, let the bio area grow, and keep Save reachable through scrolling or a safe toolbar placement.

## Key Takeaways

- Choose text style by semantic role and support Dynamic Type throughout.
- Use plain, specific words and outcome-oriented action labels.
- Keep labels persistent and errors local, actionable, and neutral.
- Plan for text expansion and reflow before truncating.
- Review critical copy for clarity under stress.

## Connects To

- Chapter 3: Layout and Adaptivity
- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 12: Forms and Data Entry
- Chapter 19: State, Status, and Progress

## Source Focus

Typography; Writing; Inclusion; Accessibility; Text fields; Text views; Alerts; Onboarding; Launching.
