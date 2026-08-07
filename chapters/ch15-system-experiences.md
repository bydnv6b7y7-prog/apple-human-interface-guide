# Chapter 15: Widgets, Live Activities, Notifications, Controls, and App Shortcuts

## Core Idea

System experiences place selected app value outside the full app. They must be glanceable, privacy-aware, timely, and narrowly scoped. A widget summarizes and deep-links; a Live Activity tracks a bounded event; a notification interrupts only when information matters now; a control or App Shortcut performs a focused action.

## Frameworks Introduced

### Surface-to-job mapping

- **Widget:** Persistent glanceable information and a few lightweight interactions.
- **Live Activity:** Frequently changing status for one bounded event.
- **Notification:** Timely information that matters outside the foreground app.
- **Control:** A focused action or state available in a system control surface.
- **App Shortcut:** A common task invoked through system search, voice, automation, or supported surfaces.
- **Spotlight result/snippet:** Searchable app content or a concise interactive result.

## Key Concepts

### Give every widget one clear purpose

A widget should answer a small, valuable question or support a simple recurring action. It is not a miniature app. Deep-link each meaningful region to the exact app destination.

Offer multiple sizes only when each size provides more useful content or a better job, not scaled padding around the same design. Balance density and legibility. Source guidance suggests standard content margins around 16 points, with about 11 points sometimes appropriate for a tighter visual group; use container-relative shapes instead of hard-coded corner radii.

Keep text readable—generally at least 11 points—and support semantic colors, Light/Dark appearances, and non-color meaning. Use full-color imagery when content demands it, not as generic decoration.

Provide realistic placeholders and previews that preserve privacy. Start widget descriptions with an action verb and explain the value concisely.

### Use Live Activities for bounded live status

A Live Activity has a clear beginning and end and is best for events that update frequently enough to matter at a glance. The source advises keeping an event ideally within about eight hours.

Show only essential, nonsensitive information across Lock Screen, compact, minimal, and expanded presentations. Keep the states visually and semantically coherent. The Lock Screen layout commonly uses about a 14-point margin.

Start the activity when expected or under person control. Update when status meaningfully changes, not continuously for animation. Use alerts only for essential changes and do not duplicate push notifications. End immediately when the event finishes; a useful completion state can remain roughly 15–30 minutes, while the system may retain it on the Lock Screen for up to four hours.

Support one simple interaction where valuable and deep-link to the exact event.

### Send notifications only when they earn interruption

A notification should be timely, useful, and nonduplicative. Do not use notifications to nag about unfinished tasks, repeat information already visible, or report an error to someone currently viewing the app.

When the app is foreground:

- Update visible content.
- Use a subtle in-app state or badge where useful.
- Avoid showing a redundant system banner.

Keep title and body concise. Hide or generalize sensitive previews and provide a meaningful placeholder when previews are disabled. Actions should save time, use clear verbs, and prefer nondestructive choices. Do not add a redundant Open action.

Badges should represent current unread or unresolved information, remain accurate, and never be the only status cue.

### Make controls complete outside the app

A system control should perform a valuable focused action without launching the app whenever possible. Reflect current state, progress, and completion. Use a descriptive SF Symbol and authenticate security-sensitive actions. Redact sensitive state while the device is locked.

Avoid controls that merely act as promotional launchers or require a multistep interface.

### Make App Shortcuts memorable

Choose common, important tasks. Keep the invocation phrase brief and natural, and make it discoverable in the app when relevant. A shortcut should generally perform one focused intent with at most one optional parameter rather than open an ambiguous menu.

Order the most valuable shortcuts first and deep-link to confirmation or relevant content when the result benefits from review.

### Keep Spotlight results useful

Index content people reasonably expect to retrieve. Use clear titles, descriptions, and metadata, and remove stale or private items when appropriate. A snippet should be concise, stay within the system’s limited height—source guidance notes a maximum around 400 points—and offer a descriptive primary action. Deeper detail belongs in the app.

### Preserve system status regions

Keep status-bar content legible and use the system scroll-edge treatment beneath transparent bars. Hide system status only temporarily when full-screen media or immersion gains real value, and preserve a familiar reveal or exit path.

## Mental Models

### Glance, act, continue

Each system surface should let a person:

1. Understand the current meaning at a glance.
2. Take at most one focused action when appropriate.
3. Continue in the exact app context if more work is needed.

### Freshness contract

If a surface displays status, define how it updates, when it expires, what it shows when stale, and how it protects privacy. A stale “live” surface damages trust more than no surface.

### Interruption threshold

Use a notification only when waiting until the next app visit would materially reduce value. Use a Live Activity when the event state matters repeatedly. Use a widget when the information remains useful over time.

## Anti-patterns

- Widget screens packed with navigation and several app-like tasks.
- Same widget composition merely scaled across sizes.
- Using a widget for real-time second-by-second status.
- Live Activity with no defined end.
- Ads, private details, or promotional copy in Live Activities.
- Notifications duplicating foreground errors or Live Activity updates.
- Badge counts that drift out of sync.
- Notification actions labeled Open or Yes.
- A system control that only launches the app.
- Many vague App Shortcuts with unnatural phrases.

## Implementation Bridge

- Use WidgetKit timelines and App Intents for focused widget interaction.
- Use ActivityKit for bounded Live Activities and remote updates where justified.
- Use UserNotifications categories and actions with privacy-aware content.
- Use AppIntent and App Shortcuts for focused system actions.
- Use Core Spotlight for searchable content and remove expired index items.
- Route every entry through one tested deep-link model that reconstructs a valid navigation path.
- Test locked/unlocked, previews hidden, stale data, offline state, denied notifications, all widget sizes, and every Live Activity presentation.

## Decision Table

| Product need | Surface |
| --- | --- |
| Persistent daily summary | Widget |
| Delivery, ride, timer, or match in progress | Live Activity |
| Time-sensitive change outside app | Notification |
| Toggle or focused system action | Control |
| Common task by voice/search/automation | App Shortcut |
| Find specific app content | Spotlight |

## Worked Example: Food Delivery

The concept sends a notification for every status change, mirrors them in a Live Activity, shows the courier’s full name and address on the Lock Screen, and opens the app home screen from every surface.

Reconstruct it:

1. Start one Live Activity after the order is accepted and show the next meaningful status, concise ETA, and privacy-safe identity.
2. Update only on material status change; reserve alerts or notifications for changes needing attention, such as a substitution or arrival.
3. End the activity when delivered and leave a short completion state if useful.
4. Make each surface deep-link to the exact order.
5. Offer a widget for broader recent-order or favorite-ordering value, not second-by-second delivery tracking.
6. Add an App Shortcut such as reordering a favorite with one optional restaurant parameter.
7. Redact address and courier details when locked or previews are hidden.

## Key Takeaways

- Give each system surface one narrow, valuable job.
- Use widgets for persistent glances and Live Activities for bounded live events.
- Notify only when information matters outside the current app context.
- Keep system actions focused, stateful, secure, and deep-linked.
- Define freshness, expiry, denied-state, and privacy behavior before implementation.

## Connects To

- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 9: Navigation and Search
- Chapter 16: Launch, Onboarding, Accounts, Settings, and Help
- Chapter 19: State, Status, and Progress

## Source Focus

Widgets; Live Activities; Notifications; Controls; App Shortcuts; Spotlight; Offering help; Status bars; Snippets.
