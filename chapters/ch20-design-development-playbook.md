# Chapter 20: iOS Page Design-to-Development Playbook

## Core Idea

Turn a feature request into a production-ready iOS page by resolving product intent, information hierarchy, navigation, states, adaptation, accessibility, privacy, and component semantics before visual polish. Then implement the same decisions as a small SwiftUI state model and semantic view hierarchy.

This playbook is the default operating procedure for using this skill on future iOS page work.

## Frameworks Introduced

### The HIG Page Contract

Every page proposal should define:

1. **Purpose:** Person, job, and smallest successful outcome.
2. **Entry and exit:** How people arrive, leave, cancel, and return.
3. **Hierarchy:** Primary content, primary action, secondary content, tertiary actions.
4. **Structure:** Tab, stack, split view, sheet, popover, alert, or window.
5. **Components:** System-first mapping for every interaction.
6. **States:** Initial, loading, content, empty, refresh, error, denied, offline, success.
7. **Adaptation:** Compact/wide, portrait/landscape, Dynamic Type, keyboard, RTL.
8. **Trust:** Accessibility, privacy, permissions, destructive recovery.
9. **Feedback:** Immediate response, progress, completion, failure, undo.
10. **Verification:** Scenarios and acceptance checks on real configurations.

### Design confidence levels

Label important recommendations:

- **HIG rule:** Directly grounded in Apple guidance or standard component semantics.
- **Product inference:** Best choice based on the described job and hierarchy.
- **Open decision:** Requires product data, user research, policy, or content not yet supplied.

This prevents a design preference from masquerading as a platform requirement.

## Key Concepts

### Resolve semantics before styling

The navigation container, presentation type, action role, control semantics, and state model determine whether a page behaves like iOS. Color, radius, blur, imagery, and motion refine that structure after it is sound.

### Design one contract across disciplines

Product intent, page anatomy, component choice, state behavior, accessibility, privacy, copy, implementation, and tests should describe the same decisions. A mockup that omits failure and a view model that invents new states are two incomplete versions of the product.

### Make adaptation explicit

Do not leave iPad, compact windows, Dynamic Type, localization, keyboard, pointer, and denied permissions to implementation improvisation. Define what remains, reflows, collapses, or becomes another presentation.

### Separate platform rule from product judgment

Apple guidance establishes familiar behavior and constraints, but it rarely decides the product’s primary task, business priority, or content model. Mark each recommendation by confidence so the team knows what to validate with Apple guidance and what to validate with users or product evidence.

## Mental Models

### Page as stateful contract

A page is the agreement among intent, visible hierarchy, available actions, system environment, data state, and recovery. If any part changes, review the whole contract rather than patching the screenshot.

### Semantics → behavior → appearance

Choose what an element means, then how it behaves across inputs and states, then how it looks. Reversing this order often produces custom controls that resemble iOS but fail under accessibility, keyboard, loading, or error conditions.

### One source of truth

Navigation, presentation, progress, button availability, and feedback should derive from explicit product state. This keeps the visual design, SwiftUI implementation, and automated tests aligned.

## Anti-patterns

- Starting from a gallery screenshot or card style before identifying the task.
- Treating every stakeholder request as equally prominent.
- Using a sheet to avoid deciding navigation hierarchy.
- Creating custom controls because system components appear insufficiently branded.
- Designing only the successful content state.
- Adding separate phone and tablet screens with no shared information model.
- Writing several loading/error booleans that can form impossible states.
- Declaring a design “HIG-compliant” without testing Dynamic Type, assistive input, denial, failure, and interruption.
- Presenting personal preference as an Apple requirement.
- Producing SwiftUI code that does not preserve the page’s action hierarchy and recovery contract.

## Phase 1: Frame the Product Decision

### Write the one-sentence job

Use:

> When [context], the person needs to [task] so they can [outcome].

Then define the smallest success that the page itself can deliver. If the sentence contains several unrelated outcomes, split the feature or choose a clear primary path.

### Identify trust constraints

List:

- Sensitive data involved.
- Permissions and the exact moment each becomes necessary.
- Financial, health, safety, or irreversible consequences.
- Content that must not appear in notifications, widgets, screenshots, or locked surfaces.
- Recovery requirements and data-retention expectations.

### Decide what can wait

Move account creation, profile completion, advanced preferences, optional permissions, education, cross-sell, and secondary analytics out of the main path unless they are genuinely required for success.

## Phase 2: Build the Information and Action Hierarchy

Classify every proposed element:

| Class | Question | Typical treatment |
| --- | --- | --- |
| Primary content | What must be understood or changed now? | Main page region |
| Primary action | What advances/completes the task? | One prominent Button or standard placement |
| Secondary content | What helps the current decision? | Supporting region, section, disclosure |
| Secondary action | What is useful but not dominant? | Secondary button or toolbar |
| Tertiary action | What is infrequent/contextual? | Menu or context menu |
| Destructive action | What removes or irreversibly changes? | Destructive role, undo or confirmation |

Remove duplicate headings, repeated metadata, decorative cards, and actions that do not serve the current job.

### Choose navigation before layout

- Independent top-level destination → TabView.
- Compact hierarchy → NavigationStack.
- Persistent hierarchy in wide space → NavigationSplitView.
- Short distinct task → sheet.
- Small temporary controls in wide space → popover.
- Critical actionable interruption → alert.
- Choices after an initiated action → confirmation dialog.
- Independent durable document/task → window.

Do not solve a hierarchy problem with visual styling.

## Phase 3: Map to System Components

Use this system-first mapping:

| Intent | SwiftUI starting point |
| --- | --- |
| Hierarchical navigation | NavigationStack / NavigationLink |
| Wide hierarchy | NavigationSplitView |
| Top-level destinations | TabView |
| Repeated text rows | List / Section |
| Structured settings/data entry | Form |
| Immediate command | Button |
| Several secondary commands | Menu |
| Binary setting | Toggle |
| Small related mode set | Picker with segmented style |
| Ordered choice | Picker |
| Continuous range | Slider |
| Increment | Stepper |
| Short text | TextField / SecureField |
| Long text | TextEditor |
| Search | searchable plus scope/suggestions as needed |
| Short focused task | sheet |
| Risk-choice clarification | confirmationDialog |
| Critical interruption | alert |
| Progress | ProgressView |
| Empty/unavailable content | ContentUnavailableView or custom semantic equivalent |
| Share | ShareLink |
| Chart | Swift Charts |

Create a custom component only when:

1. No standard component serves the semantics.
2. The product benefit outweighs familiarity and accessibility cost.
3. Press, focus, disabled, selected, loading, keyboard, pointer, RTL, Dynamic Type, and accessibility states are specified.

## Phase 4: Define the State Model

Do this before writing view code.

Example:

    enum PageState {
        case initial
        case loading
        case content(Model, freshness: Freshness)
        case empty(EmptyReason)
        case permissionDenied
        case offline(cached: Model?)
        case failure(Recovery)
    }

Model a mutation separately:

    enum SubmissionState {
        case idle
        case validating
        case submitting
        case succeeded
        case failed(message: String, canRetry: Bool)
    }

Avoid several booleans that allow impossible states. Keep existing content available during refresh. Preserve drafts independently of remote success. Give retryable mutations stable identity.

For each state, specify:

- Visible content.
- Primary action and whether it is safe.
- Navigation and dismissal behavior.
- Feedback location.
- Accessibility announcement.
- Recovery or retry.
- What persists after backgrounding.

## Phase 5: Specify Adaptive Layout

### Compact mode

- Protect content and one primary action.
- Stage hierarchy.
- Keep frequent controls reachable.
- Move tertiary actions to toolbar overflow.
- Use sheets for temporary tasks.

### Wide mode

- Preserve useful navigation or comparison context.
- Add sidebar, detail, or inspector only when it improves the task.
- Use popovers for small temporary controls.
- Support resizable windows and mixed input.

### Compression order

1. Reflow inline groups.
2. Reduce secondary spacing.
3. Move tertiary actions to overflow.
4. Collapse inspector or supplementary regions.
5. Stage hierarchy.
6. Never shrink touch targets or essential type.

### Required adaptation checks

- Small iPhone portrait and landscape.
- Regular and compact iPad windows.
- Largest Dynamic Type and Bold Text.
- Long localization and right-to-left.
- Light/Dark and increased contrast.
- Software and hardware keyboard.
- Touch, pointer, and keyboard focus.
- Offline, permission denied, and interrupted work.

## Phase 6: Write the Content Contract

For every page, supply final or structurally accurate copy for:

- Navigation title.
- Section and field labels.
- Primary and secondary actions.
- Empty state and next step.
- Permission usage description.
- Validation and error recovery.
- Destructive confirmation.
- Progress and completion.
- Accessibility labels for symbol-only controls.

Use verbs for actions, persistent labels for fields, and specific recovery. Avoid “Submit,” “Yes,” “No,” “Oops,” “Error,” or “Something went wrong” when an outcome can be named.

## Phase 7: Define Feedback and Recovery

For each action:

1. Show immediate press or selection feedback.
2. Prevent accidental duplicate execution.
3. Show local progress if work takes time.
4. Preserve current content and draft.
5. End in a persistent success or failure state.
6. Offer undo for common reversible actions.
7. Confirm only rare irreversible consequences.

Use haptics and symbol motion only when they reinforce meaning. Adapt for Reduce Motion. Do not send a notification for a result already visible in the foreground.

## Phase 8: Implement a Semantic SwiftUI Skeleton

Start with data and semantics, not card styling:

    struct FeaturePage: View {
        @State private var model = FeatureModel()

        var body: some View {
            NavigationStack {
                content
                    .navigationTitle("Page Title")
                    .toolbar { pageActions }
            }
        }

        @ViewBuilder
        private var content: some View {
            switch model.state {
            case .initial, .loading:
                ProgressView()
            case .content(let content, _):
                ContentView(content: content)
            case .empty(let reason):
                EmptyStateView(reason: reason)
            case .permissionDenied:
                PermissionStateView()
            case .offline(let cached):
                OfflineStateView(cached: cached)
            case .failure(let recovery):
                FailureStateView(recovery: recovery)
            }
        }
    }

Then add:

- Semantic colors and system text styles.
- Safe-area and adaptive container behavior.
- Focus and keyboard commands.
- Accessibility name, value, order, and actions.
- Loading, disabled, and destructive roles.
- Previews for every state and environment.

Avoid creating a generic Card component before the content relationships prove that a container is needed.

## Phase 9: Review Gates

### Gate A — Product

- The person and job are explicit.
- One smallest success is visible.
- Nonessential setup is postponed.
- Primary and destructive actions are not confused.

### Gate B — HIG structure

- Navigation matches the information architecture.
- Standard components are used where semantics fit.
- Presentation is no more interruptive than necessary.
- Content and control layers remain distinct.

### Gate C — Inclusive trust

- Dynamic Type does not truncate essential meaning.
- VoiceOver, Voice Control, keyboard, and pointer paths work.
- Color, sound, motion, and gestures are not single channels.
- Permissions are minimal and requested in context.
- Sensitive content is protected on system surfaces.
- RTL and localization reflow are defined.

### Gate D — State and recovery

- Every reachable state has a design.
- Refresh preserves useful content.
- Errors state what happened and what to do next.
- Drafts survive interruptions.
- Retry is safe and undo is available where appropriate.

### Gate E — Craft

- Alignment and spacing express hierarchy.
- Copy is concise and consistent.
- Motion explains cause or continuity.
- The page works in Dark Mode and accessibility settings.
- Real-device interaction feels immediate.

## Required Output Format for Future Page Requests

When this skill guides a page design or implementation, respond in this order:

1. **Recommendation** — The proposed page in one paragraph.
2. **Product rationale** — Job, smallest success, and deferred elements.
3. **Page anatomy** — Ordered regions and action priority.
4. **Interaction flow** — Entry, main path, cancel, completion, recovery.
5. **Component map** — Intent → Apple component → SwiftUI API.
6. **State matrix** — Loading, content, empty, error, denied, offline, success.
7. **Adaptive behavior** — iPhone, iPad window sizes, Dynamic Type, RTL, inputs.
8. **Accessibility and privacy** — Concrete requirements.
9. **Implementation** — State model and production-oriented SwiftUI structure when requested.
10. **Acceptance checks** — Testable outcomes.

Keep the recommendation decisive. Ask a question only when a missing product decision would materially change navigation, data collection, destructive behavior, or business outcome. Otherwise state the assumption and proceed.

## Worked Example: Subscription Management Page

Requirement: “Design a premium membership page with upgrade, plan change, restore, and cancel.”

Apply the contract:

1. **Purpose:** Let a person understand current entitlement and perform the next relevant subscription action.
2. **Hierarchy:** Current plan/status first; benefits and available plan comparison second; one context-specific primary action; Restore and policy links secondary; cancellation clearly labeled but not visually promoted.
3. **Structure:** A normal navigation page, not a launch modal. Use a sheet only for plan comparison or purchase flow if system commerce does not own it.
4. **State:** Not subscribed, active, trial, grace period, expired, family/shared entitlement, loading, offline cached, purchase pending, failure, restored.
5. **Trust:** Show price, billing period, renewal behavior, trial terms, and consequences before commitment. Never use false urgency or hide cancellation.
6. **Components:** List/Form sections, standard Buttons and links, ProgressView during purchase, confirmation only for meaningful destructive consequences, StoreKit system purchase management.
7. **Adaptation:** Stack benefit comparisons at large text; on iPad avoid a narrow phone page floating in unused space—use readable width and supporting detail where useful.
8. **Recovery:** Prevent duplicate purchase, preserve entitlement display, provide specific Retry, and make Restore status persistent.
9. **Acceptance:** VoiceOver reads plan and price correctly; denied network leaves current entitlement visible; interrupted purchase resolves safely; localization does not truncate price terms.

The result is a trustworthy account page, not a generic marketing paywall.

## Key Takeaways

- Use the HIG Page Contract before visual styling or SwiftUI composition.
- Resolve hierarchy, presentation, components, states, adaptation, and trust explicitly.
- Derive the UI from a small state model and preserve content through work and failure.
- Review product, structure, inclusion, recovery, and craft as separate gates.
- Produce decisive recommendations with implementation and testable acceptance criteria.

## Connects To

All chapters. Start here for page design and development, then load the relevant specialist chapters from the topic index.

## Source Focus

Synthesizes Design principles, Designing for iOS, Designing for iPadOS, Foundations, Inputs, Patterns, Components, and System experiences.
