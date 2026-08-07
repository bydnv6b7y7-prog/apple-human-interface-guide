# Chapter 19: State, Status, Progress, Empty, Error, and Recovery

## Core Idea

A page is a state machine, not a successful-data screenshot. Design what people see before content exists, while work happens, when data becomes stale or unavailable, after success, when access is denied, and when recovery is required. State should be local, honest, persistent enough to inspect, and proportionate to urgency.

## Frameworks Introduced

### Minimum page-state matrix

- Initial or not started.
- Loading or preparing.
- Loaded with content.
- Loaded but empty.
- Refreshing with existing content.
- Partially available or stale.
- Permission denied or restricted.
- Offline.
- Validation error.
- Recoverable operation failure.
- Destructive or terminal failure.
- Success or completion.

Not every page needs a separate visual for every row, but every reachable condition needs defined behavior.

### Feedback placement

- **Control-level:** Pressed, selected, disabled, busy.
- **Field-level:** Validation and format correction.
- **Item-level:** Upload, sync, retry, or per-object error.
- **Page-level:** Empty, offline, or unavailable collection.
- **App/system-level:** Notification or alert only when the event exceeds the current page context.

## Key Concepts

### Preserve useful content during refresh

Keep existing content visible while refreshing and place progress near the update. Avoid replacing a useful page with a full-screen spinner. If data is stale, label it and offer Retry or Refresh without pretending it is current.

Use pull to refresh only when people expect content to update and it has a clear source. Do not make it the only refresh path when freshness is critical.

### Choose determinate progress whenever reliable

Use determinate progress for measurable work and indeterminate progress for brief or unknown-duration work. Change from indeterminate to determinate when trustworthy measurement becomes available. Do not change a spinner into a visually unrelated bar in a way that makes the operation appear to restart.

Keep progress honest and spatially stable. Allow Pause or Cancel for long work when safe, and explain the consequence. Expose a numeric or descriptive accessibility value.

Use a spinner for brief background work or constrained space. It usually does not need a separate “Loading” label if surrounding context makes the task obvious.

### Make empty states actionable

Differentiate:

- **First-use empty:** Explain what belongs here and offer creation/import.
- **Filtered empty:** State that no results match and provide Clear Filters or scope change.
- **Completed empty:** Confirm that there is nothing requiring attention.
- **Unavailable empty:** Explain permission, offline, or service state and recovery.

Do not place essential permanent instruction only in a first-use empty state.

### Keep errors close to the problem

Use inline messages for field and item errors, page-level recovery for a failed collection, and alerts only when immediate interruption is necessary. Use notifications for useful background events outside the foreground app, not errors already visible.

An error should state:

1. What could not happen.
2. What remains safe or preserved.
3. What the person can do next.

Avoid blame, codes, “Oops,” and generic messages with no recovery.

### Do not disable without explanation

A disabled action is acceptable when the missing requirement is visible and obvious. Otherwise keep the control actionable and explain the problem at the right time, or add nearby guidance. Disabled appearance alone is not instruction.

### Distinguish status from decoration

Use badges only for current unread or unresolved information, and pair them with another accessible cue. Use gauges for a current value within a meaningful range, with current and endpoint labels. Use the Apple Activity rings only for their established Move, Exercise, and Stand meanings; do not reuse them for branding or unrelated progress.

### Preserve recovery and idempotence

Retry should not duplicate a purchase, upload, message, or mutation. Persist drafts and local intent. For long operations, show which items succeeded and which failed instead of rolling the entire batch back without explanation.

## Mental Models

### Content continuity

Prefer this sequence:

1. Preserve the last useful truth.
2. Mark its freshness or pending change.
3. Show local progress.
4. Replace only when the new state is ready.

### Urgency × scope

The more local the issue, the closer the message belongs to it. The more urgent and globally consequential the issue, the stronger the presentation can become. Most errors are local and recoverable.

### State owns the UI

Derive visible controls, labels, navigation availability, and feedback from one explicit state model. Avoid independent booleans such as isLoading, hasError, isEmpty, and didSucceed that can produce impossible combinations.

## Anti-patterns

- Designing only loaded and ideal states.
- Full-screen spinner during every refresh.
- Removing old content before replacement is ready.
- Fake progress that stalls near completion.
- Spinner with no operation context for an extended task.
- Generic “Something went wrong” and one Dismiss button.
- Alert for an inline validation issue.
- Error notification while the person is looking at the failed action.
- Empty state that cannot distinguish no data from failed loading.
- Color-only badges or status lights.
- Reusing Activity rings for arbitrary metrics.
- Retry that submits the same transaction twice.

## Implementation Bridge

- Model page state with an enum and associated data rather than overlapping booleans.
- Use ProgressView, refreshable, ContentUnavailableView, gauge, badge, and standard alert/confirmation components according to scope.
- Keep prior content in the model during refresh and distinguish loadingInitial from refreshing.
- Give mutations stable request identity and make retry idempotent.
- Persist drafts separately from remote submission state.
- Announce meaningful state changes through accessible status without repeatedly stealing focus.
- Test slow network, offline, stale cache, partial data, denied permission, canceled task, duplicate tap, backgrounding, and retry.

## Reference Table

| State | Preferred presentation |
| --- | --- |
| Initial load | Skeleton or standard progress if content cannot appear |
| Refresh | Existing content plus local refresh feedback |
| First-use empty | Explanation plus primary creation/import action |
| Filtered empty | Active scope plus Clear Filters |
| Item failure | Inline item status and Retry |
| Form error | Message adjacent to field |
| Page unavailable | Page-level explanation, preserved context, Retry |
| Irreversible critical problem | Alert with specific outcomes |
| Background completion | Notification only if useful outside app |

## Worked Example: Offline Inbox

The draft replaces the inbox with a spinner during refresh, then shows an alert saying “Network Error” and clears the badge.

Reconstruct it:

1. Keep cached messages visible and show a small refresh state near the list.
2. If refresh fails, label the inbox “Updated 12 min ago” and provide Retry without blocking reading.
3. Preserve unread counts from the last known data and identify them as stale if necessary.
4. Queue safe outbound drafts with item-level sending state; a failed message remains visible with Retry.
5. Use idempotent message identifiers so retry cannot send twice.
6. When no cached messages exist, show an offline page state that explains the limitation and offers Retry—not a generic alert.
7. Announce the connectivity change without repeatedly moving VoiceOver focus.

## Key Takeaways

- Treat every page as an explicit state machine.
- Preserve useful content during refresh and show honest local progress.
- Distinguish first-use, filtered, completed, and unavailable empty states.
- Put errors near their scope and always provide a specific recovery.
- Make retry safe and test adverse conditions deliberately.

## Connects To

- Chapter 5: Typography and Writing
- Chapter 8: Motion, Feedback, and Haptics
- Chapter 15: System Experiences
- Chapter 20: Design-to-Development Playbook

## Source Focus

Progress indicators; Refreshing content; Feedback; Alerts; Notifications; Writing; Empty states; Gauges; Activity rings; Status bars.
