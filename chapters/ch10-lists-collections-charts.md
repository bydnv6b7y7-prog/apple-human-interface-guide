# Chapter 10: Lists, Collections, Scrolling, and Charts

## Core Idea

Choose a content container from the information people need to scan and compare. Lists prioritize readable rows and predictable rhythm; collections prioritize visual items and flexible arrangement; charts prioritize relationships in data. In every case, content should remain primary, selection should be unambiguous, and interaction should not cause surprising layout movement.

## Frameworks Introduced

### Container choice

- **List or table:** Text-heavy, repeated rows, settings, hierarchy, or values that benefit from aligned scanning.
- **Collection or grid:** Images, cards, variable-size items, spatial browsing, or layouts that need multiple columns.
- **Chart:** Trends, comparisons, distributions, ranges, or composition that are harder to understand as raw values.
- **Disclosure:** Secondary detail that remains closely associated with one content region.
- **Tab view within content:** A small set of related, self-contained panes—not app-level destinations.

### Selection models

- **Navigation selection:** The selected row remains highlighted because its detail is visible.
- **Option selection:** A checkmark or control indicates one or more chosen values.
- **Action row:** Selecting performs a command; it should not look like persistent selection.

## Key Concepts

### Make rows scannable

Keep each row concise and structurally consistent. Put the primary label first, use secondary text only when it changes the decision, and align accessories predictably. Avoid making every row a miniature dashboard.

Use a disclosure indicator when a row opens deeper hierarchy. Use an info button only when the row’s primary selection does something else and separate supporting detail is genuinely needed.

### Use standard list behavior

Standard list styles, content configurations, edit modes, swipe actions, reordering, and selection already communicate familiar behavior. Customize only what the content model needs. Preserve full-row hit regions and visible pressed or selected states.

Swipe actions are useful shortcuts, not the only route to an important command. Keep destructive actions recognizable and recoverable when possible.

### Keep collections stable

Choose a grid or row layout that makes item boundaries and reading order clear. Make selection easy and persistent. Avoid moving unrelated items or changing column structure unexpectedly after an item is selected, loaded, or hovered.

Use lazy containers for large data sets, but preserve stable identity so state, focus, animation, and scrolling remain correct.

### Use disclosure sparingly

Disclosure works for optional detail within the current context. Keep the trigger near the content it controls and generally use one disclosure control for one view or section. If several levels of disclosure create a hidden hierarchy, use navigation instead.

### Keep content tabs small

A tab view inside a page can switch among a few closely related panes. Keep each pane self-contained and the set small—avoid more than about six. Do not confuse this with the app’s top-level tab bar.

### Begin charts with the question

Select a mark based on what a person needs to learn:

- Line or area for change over ordered time.
- Bar for categorical comparison.
- Point or scatter for relationship and distribution.
- Rectangle or sector only when area or part-to-whole comparison remains legible.

Combine marks only when the combination improves the message. Keep data visually stronger than gridlines, chrome, and decoration.

### Choose honest scales

Use a fixed domain when the true limits matter, such as battery percentage from 0 to 100. Use a dynamic domain when variation within the observed range is the point. Bar charts often begin at zero, but a different baseline can be valid for bounded physiological or scientific data when clearly communicated.

Use familiar tick sequences and units. State the main message in text and provide a readable summary.

### Make charts accessible and directly explorable

Do not distinguish series by color alone; also use marks, line styles, labels, or grouping. Support VoiceOver and Audio Graphs where appropriate. Critical values and conclusions must be available without a gesture.

When a chart is interactive, expand the hit region across the plot and reveal exact values without requiring pixel-perfect contact.

## Mental Models

### Scan density

Ask what comparison people make:

- Across labels: favor a list.
- Across imagery: favor a grid.
- Across numeric patterns: favor a chart.
- Within one object: favor detail or disclosure.

### Stable identity

Every item needs a durable identity independent of position. Sorting, filtering, asynchronous loading, and updates should not cause the selected item, edit state, or scroll position to jump to another object.

### Message before mark

Write the sentence the chart should communicate, then select a mark, domain, labels, and interaction that make that sentence inspectable. If the sentence remains clearer as two numbers, a chart may be unnecessary.

## Anti-patterns

- Dense cards where a simple list would scan faster.
- Rows containing several competing primary actions.
- Using a checkmark for navigation selection or persistent highlight for a one-time option.
- Swipe as the only way to access an important action.
- Dynamic grid shifts that move the item someone is trying to select.
- Multiple nested disclosures replacing a real hierarchy.
- Decorative charts without a defined question.
- Truncated axes or arbitrary scales that exaggerate change.
- Color-only data series.
- Requiring interaction to learn the chart’s central value.

## Implementation Bridge

- Use List, Section, standard list styles, swipe actions, edit mode, and selection binding for row-based content.
- Use LazyVGrid, LazyHGrid, or custom Layout only when the content needs a collection.
- Give data items stable identifiers; do not use array positions for mutable collections.
- Use Swift Charts marks, axes, selections, annotations, and accessibility descriptions.
- Provide textual summaries and accessibility representations for complex visualizations.
- Preserve scroll position and selection across refresh, filter, and navigation updates.

## Decision Table

| Content | Container | Key behavior |
| --- | --- | --- |
| Settings | Grouped list/Form | Consistent labels and controls |
| Message inbox | List | Fast scan, stable selection, swipe shortcuts |
| Photo library | Adaptive grid | Visual browsing and multi-selection |
| Product comparison | List/table or aligned grid | Comparable fields stay aligned |
| Weekly trend | Chart | Honest scale, summary, accessible values |
| Optional metadata | Disclosure | Stays near its content |

## Worked Example: Health Trends

The page shows six metric cards, each with a tiny colorful chart, hidden exact values, and a grid that reorders when a card is tapped.

Reconstruct it:

1. Use a list for metric summaries so name, current value, change, and status scan consistently.
2. Open one metric detail with a sufficiently large chart and a textual summary of the trend.
3. Choose a scale based on the metric’s real domain; label units and meaningful time ticks.
4. Pair color with symbols, line styles, or labels.
5. Add a broad chart-selection hit region and accessible values, while keeping the current and important extremes visible without interaction.
6. Keep item order and selection stable during refresh.
7. On iPad, preserve the metric list and selected chart detail side by side when width permits.

## Key Takeaways

- Pick lists, collections, and charts based on the comparison people need.
- Keep rows concise, selection explicit, and item identity stable.
- Use disclosure for nearby optional detail, not hidden hierarchy.
- Start a chart with a question and use an honest, labeled scale.
- Make the message and critical data available without color or precision gestures.

## Connects To

- Chapter 3: Layout and Adaptivity
- Chapter 9: Navigation and Search
- Chapter 14: Inputs and Interactions
- Chapter 17: Content Workflows

## Source Focus

Lists and tables; Collections; Disclosure controls; Tab views; Charts; Scroll views; Drag and drop; Accessibility.
