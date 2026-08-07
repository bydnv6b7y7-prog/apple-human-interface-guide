# Chapter 16: Launch, Onboarding, Accounts, Settings, Help, and Ratings

## Core Idea

The app should reveal value before demanding commitment. Launch with continuity, teach in context, postpone accounts and permissions until their benefits are clear, choose strong defaults, and ask for ratings only after a genuine positive experience.

## Frameworks Introduced

### Value-first lifecycle

1. **Launch:** Restore a useful state immediately.
2. **Orient:** Make the primary value and next action evident.
3. **Teach:** Explain unfamiliar behavior at the moment it becomes relevant.
4. **Commit:** Ask for account, permission, purchase, or setup only when needed.
5. **Support:** Keep settings and help discoverable but out of the main flow.
6. **Reflect:** Ask for a rating after demonstrated engagement at a natural break.

### Teaching hierarchy

Prefer:

1. Familiar interface that needs no explanation.
2. Good defaults and visible affordances.
3. Brief contextual label or empty-state guidance.
4. A TipKit tip near the relevant feature.
5. A short optional onboarding flow only for prerequisites or a truly novel model.

## Key Concepts

### Launch directly into the experience

Launch quickly and restore the previous meaningful state. The launch screen is a visual bridge while the app initializes; make it closely resemble the first frame, with minimal static structure. Do not use it as a timed splash, advertisement, tutorial, or branding screen, and avoid text that can become stale or need localization.

Load cached or placeholder content when remote data is unavailable and show a nonintrusive state. Do not greet every launch with an alert.

### Keep onboarding short and optional

Let people learn by doing. Postpone nonessential profile completion, theme selection, feature tours, subscription pitches, and permissions. If a prerequisite must be explained, use a small number of focused pages with a clear skip or exit unless completion is truly required for the app’s core function.

Use context-specific tips for unfamiliar or newly available actions. A tip should describe one action or benefit, appear only to eligible people, and recur at a respectful cadence. Source guidance suggests one or two sentences for tips, short tooltips around 60–75 characters, and avoiding more frequent display than roughly once per 24 hours.

Do not explain standard platform behavior such as how to tap a tab or use a Back button.

### Delay account creation

Allow browsing, trial, local work, or other meaningful use without signing in when the product permits. Ask for an account when sync, collaboration, purchase restoration, or protected personal content makes its value clear.

Use passkeys, Sign in with Apple, password AutoFill, and system authentication. Name the biometric actually available rather than using a generic or wrong brand. Do not add a redundant in-app biometric opt-in screen when system authorization already communicates the choice.

Make account deletion discoverable and explain what will be removed, retained for legal reasons, or still processing. Show a clear completion or pending status and preserve a safe Cancel path before irreversible deletion.

### Ask for permissions in context

Trigger the request when someone initiates the feature. Explain the direct value, not organizational need. If access is denied, keep the app useful where possible and show a route to Settings only when the person tries the affected feature again.

Do not bundle permission requests into onboarding merely to improve acceptance metrics.

### Make settings earn their existence

Choose strong defaults that work for most people and honor system settings such as appearance, text size, notifications, locale, accessibility, and privacy.

Place:

- Frequent contextual choices near the content they affect.
- Infrequent app-wide preferences in a Settings area.
- Device- or permission-level options in system Settings, with an appropriate deep link when needed.

Avoid a settings page that exposes implementation flags or asks people to configure the product before they can understand it.

### Offer help at the point of uncertainty

Help should be task-specific and searchable where the product warrants it. Use examples, concise steps, and links to deeper support. Make recovery available near errors. Do not use help text to compensate for unclear labels or unconventional standard actions.

### Request ratings after value

Use the system rating prompt after sustained engagement, completion, or another positive natural break—not at launch, during onboarding, after an error, or while the person is busy. Do not ask a preliminary “Do you like the app?” question to route only positive users to the system prompt.

The system controls whether the prompt appears and limits display; the source notes up to three displays within a 365-day period. Treat every request opportunity as scarce.

## Mental Models

### Time to first value

Measure from launch to the first meaningful outcome, not to account creation or tutorial completion. Remove or postpone each step that does not make that outcome safer or more understandable.

### Teach on contact

Explain a feature when the person can see or use it. Context gives the explanation meaning and lets the person act immediately.

### Default, context, settings

For every preference ask:

1. Can a strong default remove the choice?
2. Does the choice belong beside the content it affects?
3. Only then, does it deserve a durable Settings entry?

## Anti-patterns

- Timed logo splash or launch-screen advertising.
- Blocking first use behind a carousel of feature descriptions.
- Requesting notifications, tracking, location, photos, and contacts during onboarding.
- Mandatory sign-in before a person can understand the product.
- Custom password or biometric flow that imitates system UI.
- Hidden or ambiguous account deletion.
- Settings for system appearance, text size, or behaviors the platform already controls.
- Tips that appear repeatedly, cover content, or promote upgrades.
- Rating prompt at launch, after failure, or before meaningful engagement.
- Custom rating pre-screen that suppresses negative feedback.

## Implementation Bridge

- Keep launch work minimal, restore scene/navigation state, and render useful cached content early.
- Use TipKit eligibility and rules for contextual education.
- Use AuthenticationServices, passkeys, Sign in with Apple, AutoFill, LocalAuthentication, and secure storage.
- Model permission states including not determined, denied, restricted, limited, and authorized; design every path.
- Use openSettingsURL only in a context where the person understands what to change.
- Use StoreKit’s system review-request API and never assume it will display.
- Persist drafts and onboarding completion without making version changes force the entire tour again.

## Reference Table

| Moment | Preferred response |
| --- | --- |
| First launch | Useful content or smallest core task |
| New unfamiliar feature | Contextual TipKit tip |
| Permission needed | Request at feature use |
| Sync/collaboration needed | Explain benefit, then authenticate |
| Frequent local option | Put near affected content |
| Rare global preference | Settings area |
| Recoverable confusion | Inline help near task |
| Positive natural break | System rating request |

## Worked Example: Personal Budget App

The first run shows five tutorial pages, requires account creation, asks for notifications and contacts, requests a rating, and then opens an empty dashboard.

Reconstruct it:

1. Open to a focused “Add your first account or transaction” task with sample context.
2. Let a person try local budgeting before sign-in; request an account when enabling sync or sharing.
3. Ask for notifications only when creating a reminder. Do not request contacts until sharing is chosen.
4. Use a contextual tip the first time category rules become relevant rather than teaching them in advance.
5. Choose sensible currency and date defaults from locale while keeping them editable in Settings.
6. Show an actionable empty state and restore the last-used account on later launches.
7. Request a rating after several completed weekly reviews, at the end of one—not during setup.

## Key Takeaways

- Launch into useful continuity and minimize time to first value.
- Teach on contact; use onboarding only for real prerequisites.
- Delay accounts, permissions, purchases, and ratings until their value is visible.
- Prefer strong defaults and contextual controls over large settings screens.
- Use system authentication, tips, permission, and rating experiences.

## Connects To

- Chapter 1: Design Principles and Product Intent
- Chapter 7: Accessibility, Privacy, and Localization
- Chapter 13: Modality and Presentation
- Chapter 15: System Experiences

## Source Focus

Launching; Onboarding; Managing accounts; Settings; Offering help; Ratings and reviews; Privacy; Feedback; Alerts.
