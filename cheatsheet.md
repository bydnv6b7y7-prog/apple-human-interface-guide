# Apple HIG iOS Design and Development Cheatsheet

## Start Here

1. Name the person’s job and smallest success.
2. Choose navigation/presentation from task semantics.
3. Map actions and values to system components.
4. Define the complete state matrix.
5. Specify compact/wide, Dynamic Type, RTL, and input adaptation.
6. Implement semantic structure, then visual finish.
7. Verify on real adverse states and configurations.

## Fast Component Choice

| Intent | Use |
| --- | --- |
| Top-level destination | Tab bar / TabView |
| Hierarchy | NavigationStack |
| Wide persistent hierarchy | NavigationSplitView |
| Short distinct task | Sheet |
| Small temporary wide-layout controls | Popover |
| Critical immediate action | Alert |
| Choices after initiated action | Confirmation dialog/action sheet |
| Immediate command | Button |
| Binary state | Toggle |
| Few related modes | Segmented Picker |
| Ordered choices | Picker |
| Several secondary commands | Menu |
| Search | searchable |
| Progress | ProgressView |
| Share | ShareLink |

## High-Value Numbers

- iOS interaction region: **at least 44 × 44 pt**.
- Custom ordinary text contrast: **at least 4.5:1**; strive toward **7:1**.
- Text enlargement: aim to support **200% or more**.
- Segmented control: generally **up to about 5** items on iPhone; **5–7** only with width.
- Page control: reconsider beyond **about 10** pages.
- Content tabs: avoid more than **about 6**.
- Home Screen quick actions: **up to 4**.
- Toolbar structure: roughly **up to 3 logical groups**, one prominent trailing action.
- Widget text: generally **11 pt or larger**.
- Widget margins: commonly **16 pt**, sometimes **11 pt** for tight groups.
- Live Activity: ideally **within about 8 hours**; completion often **15–30 min**, system may retain up to **4 hours**.
- Rating prompt opportunity: system may show at most **3 times in 365 days**.

These are design heuristics from the source snapshot, not substitutes for testing or current API documentation.

## State Matrix

Always consider:

- Initial
- Loading
- Content
- First-use empty
- Filtered empty
- Refreshing with content
- Offline/stale
- Permission denied/restricted
- Validation error
- Operation failure/retry
- Success/completion
- Background/interrupted

## Never Rely On

- Color alone.
- Sound or haptic alone.
- Motion alone.
- A hidden gesture alone.
- Placeholder text as the only label.
- Context menu as the only action route.
- More as the home of a primary action.
- A notification for a foreground error.
- A custom control without semantic and accessible behavior.

## Copy Rules

- Actions use specific verbs: Save, Share, Delete, Retry.
- Cancel is always “Cancel.”
- Avoid Yes/No and vague Submit/OK.
- Errors say what failed and what to do next.
- Permission copy connects access to a visible feature.
- Empty states include a relevant next step.
- Keep navigation titles concise; do not repeat the app name.

## Adaptation Order

When space shrinks:

1. Reflow.
2. Tighten secondary spacing.
3. Move tertiary actions to overflow.
4. Collapse inspector/utility.
5. Stage hierarchy.
6. Never shrink essential type or touch targets.

## Pre-Ship Checks

- Small iPhone portrait/landscape.
- Compact and regular iPad windows.
- Largest Dynamic Type and Bold Text.
- VoiceOver, Voice Control, keyboard-only, pointer.
- Light/Dark, Increase Contrast, Reduce Transparency, Reduce Motion.
- Long localization and RTL.
- Offline, slow, denied, empty, stale, failed, retry, duplicate tap.
- Background/restore and unsaved work.
- Locked notification/widget/Live Activity privacy.
- Actual hardware for touch latency, haptics, audio, and rendering.
