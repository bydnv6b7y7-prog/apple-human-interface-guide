# Reusable iOS Page Patterns

These patterns are starting structures. Adapt them to the product job and load the cited chapters before implementation.

## 1. Browse → Select → Detail

Use for inboxes, libraries, catalogs, settings categories, and content collections.

**Compact**

- Stable top-level destination in TabView when appropriate.
- NavigationStack containing a List or grid.
- Selection pushes exact detail.
- Search sits at the collection scope.

**Wide**

- NavigationSplitView preserves collection and selected detail.
- Optional inspector collapses before navigation.
- Keyboard focus and context menus accelerate visible actions.

**State requirements**

Initial load, content, first-use empty, filtered empty, refresh with content, offline cached, item failure, deleted selection.

**Load:** Chapters 2, 3, 9, 10, 14, 19.

## 2. Focused Create or Edit Task

Use for composing, adding, configuring, and editing one bounded object.

- Use normal navigation when editing belongs to the hierarchy.
- Use one sheet when the task is short and distinct.
- Give the task a specific title.
- Pair Done/Save with Cancel when leaving without completion matters.
- Use Form and semantic controls.
- Autosave a draft when practical.
- If dismissal risks loss, use a confirmation dialog with explicit outcomes.

**State requirements**

Pristine, dirty, validating, saving, saved, field errors, submission failure, canceled, draft restored.

**Load:** Chapters 5, 11, 12, 13, 19.

## 3. Permission-Gated Feature

Use when camera, photos, microphone, location, contacts, notifications, tracking, or another protected capability is necessary.

1. Let the person reach and initiate the feature.
2. Explain the immediate benefit only if it is not self-evident.
3. Request the narrowest system permission.
4. Continue directly on authorization.
5. On denial, preserve the surrounding task and explain the unavailable capability.
6. Offer Settings only when they try again and changing access is useful.

Never show fake system choices or batch unrelated permissions at launch.

**Load:** Chapters 1, 7, 13, 16, 19.

## 4. Async Collection with Offline Continuity

Use for feeds, messages, orders, files, and dashboards.

- Render cached or last-known content early.
- Refresh without blanking the page.
- Mark stale information.
- Place progress and failures at collection or item scope.
- Use stable item identifiers and idempotent retries.
- Distinguish first-use empty, filtered empty, and offline unavailable.
- Notify only for useful events outside foreground context.

**Load:** Chapters 8, 10, 15, 17, 19.

## 5. Destructive Action with Recovery

Choose by reversibility:

- Common and reversible → perform, show persistent result, offer Undo.
- Rare and irreversible → alert or confirmation dialog with specific consequence, destructive outcome, and Cancel.
- Intentional action with several choices → action sheet/confirmation dialog.

Keep the destructive command out of the primary visual role, place it last in menus, and preserve context after cancel.

**Load:** Chapters 5, 11, 13, 17, 19.

## 6. Search and Discovery

- Define one explicit scope.
- Put search in one predictable location.
- Update results while typing when feasible.
- Offer suggestions, recent searches, and useful corrections.
- Add tokens, filters, or scope only when the result set warrants them.
- Rank relevant results first.
- Open the exact result and reconstruct a natural return path.
- Provide filtered-empty recovery and privacy controls for history.

**Load:** Chapters 7, 9, 10, 15, 19.

## 7. iPhone-to-iPad Adaptive Workspace

- Preserve product destinations while changing presentation.
- Compact: tabs, NavigationStack, sheets, staged detail.
- Wide: sidebar-adaptable tabs, NavigationSplitView, inspector/popover.
- Collapse tertiary utility before navigation and content.
- Support resizable windows, pointer, keyboard, drag and drop, and multiple windows only where work benefits.
- Test thirds, halves, quadrants, portrait, landscape, and large text.

**Load:** Chapters 2, 3, 9, 13, 14, 17.

## 8. Glanceable System Extension

Choose:

- Widget for persistent summary or simple recurring action.
- Live Activity for one bounded changing event.
- Notification for a timely event that matters outside the app.
- Control for a focused action/state.
- App Shortcut for a common task by voice, search, or automation.

Define freshness, expiry, locked-state privacy, denied state, and exact deep link before visual design.

**Load:** Chapters 7, 9, 15, 19.

## 9. Media Detail and Playback

- Use system player behavior.
- Preserve aspect ratio, captions, position, output routing, and interruption state.
- Keep inline playback until full screen materially improves content.
- Make controls revealable and exit familiar.
- Use Picture in Picture for eligible passive continuity.
- Keep buffering, paused, failed, and complete states distinct.

**Load:** Chapters 7, 8, 13, 18, 19.

## 10. Trustworthy Subscription or Purchase Page

- Show current entitlement and one context-relevant primary action.
- State price, period, renewal, trial, and consequences before commitment.
- Keep restore and management discoverable.
- Avoid false urgency, preselected expensive options, and hidden cancellation.
- Prevent duplicate purchase and preserve pending state.
- Use StoreKit/system purchase behavior.

**Load:** Chapters 1, 5, 7, 11, 13, 16, 19, 20.

## Pattern Selection Rule

Select the smallest pattern that covers the primary job. Combine patterns only when the page genuinely contains both workflows. If three or more patterns compete in one screen, the feature probably needs stronger task separation or navigation.
