# Apple HIG Glossary

Use Apple’s terms precisely. Component names describe behavior, not merely appearance.

| Term | Practical meaning |
| --- | --- |
| Accessibility | Designing the complete experience for varied vision, hearing, mobility, speech, and cognitive needs, including assistive technologies and settings. |
| Action sheet / confirmation dialog | A modal set of choices that clarifies an action someone already initiated, often including a destructive or cancel path. |
| Agency | The principle that people should understand, control, and recover from their actions. |
| Alert | A critical, immediately actionable interruption with a title, optional message, and concise actions. |
| App Intent | A focused unit of app capability exposed to system surfaces such as Shortcuts, widgets, controls, and Siri. |
| App Shortcut | A common App Intent made available with brief natural phrases and system discovery. |
| Badge | A current unread or unresolved count/status attached to an app or destination; never the only status cue. |
| Compact / regular | Environment traits describing available layout space; they are more useful than assuming a fixed device canvas. |
| Content layer | The information, media, documents, or task people came to use. |
| Control layer | Navigation and controls acting on content, often rendered with system-managed materials. |
| Context menu | Secondary shortcuts related to a selected object; never the only route to an important action. |
| Control | A focused system-surface action or state, or generically an interactive component such as a Button or Toggle. |
| Craft | The principle of deliberate quality across visuals, words, motion, state, accessibility, and maintenance. |
| Dark Mode | A system appearance that semantic colors, assets, contrast, and materials adapt to; not mechanical inversion. |
| Detent | A supported sheet height, such as medium or large, used only when the content works at that height. |
| Direct manipulation | Interaction in which content visibly follows touch, pointer, Pencil, or drag with immediate feedback. |
| Dynamic Type | The system text-scaling behavior driven by semantic text styles and a person’s preferred size. |
| Empty state | A purposeful state explaining absent content and, when appropriate, the next meaningful action. |
| Familiarity | The principle of building on platform conventions and knowledge people already possess. |
| Flexibility | The principle of adapting across people, contexts, window sizes, orientations, inputs, and platforms. |
| Full Keyboard Access | System accessibility that lets people navigate and operate an interface entirely with a hardware keyboard. |
| Haptic | Tactile feedback that reinforces selection, success, warning, error, or a physical interaction. |
| Hierarchy | The ordered importance and relationship of content, navigation, and actions. |
| Inspector | Supplementary controls or attributes that affect selected content while preserving the main context. |
| Live Activity | A glanceable, frequently updated system surface for one bounded event with a clear start and end. |
| Liquid Glass | Apple’s current system-managed visual treatment that helps distinguish adaptable controls from content; use system behavior rather than painted imitation. |
| Material | An adaptive system surface that combines translucency and visual separation according to content and accessibility settings. |
| Modality | A dedicated mode that blocks interaction with the parent context until dismissal. |
| NavigationSplitView | SwiftUI structure for sidebar/content/detail hierarchy that adapts as space changes. |
| NavigationStack | SwiftUI structure for staged hierarchical navigation. |
| Permission usage description | A brief, specific explanation of how a protected capability supports the feature requesting it. |
| Popover | A transient anchored view for a small amount of related information or functionality, generally used in wide layouts. |
| Primary action | The one action most likely to advance or complete the current task; destructive is a separate role. |
| Progressive disclosure | Revealing detail or advanced capability only when it becomes relevant. |
| Purpose | The principle of creating genuine value around a clear product intent. |
| Responsibility | The principle of acting in people’s interest through privacy, safety, transparency, and data minimization. |
| Right to left (RTL) | A logical reading and navigation direction requiring layout adaptation while preserving non-directional and physical meaning. |
| Safe area | The region where essential content and controls remain clear of system-covered or difficult display areas. |
| Semantic color | A color chosen by role—label, background, tint, destructive—so it adapts to appearance and accessibility. |
| SF Symbols | Apple’s adaptable symbol library with weight, scale, rendering, variable color, and animation behavior. |
| Sheet | A modal presentation for a short, distinct task that preserves a relationship to the parent context. |
| Simplicity | The principle of clarity and directness through hierarchy, wording, defaults, and disclosure; it does not mean emptiness. |
| Spotlight | System search that can surface indexed app content and deep-link to the exact item. |
| Tab bar | Persistent top-level destination navigation; it does not contain commands. |
| TipKit | Apple framework for eligible, contextual education near a feature. |
| Toolbar | A standard control region for frequent context-relevant actions, with secondary commands in overflow. |
| Voice Control | Accessibility input that targets clearly named semantic controls through spoken commands. |
| VoiceOver | Screen reader that navigates the accessibility tree and announces element name, role, value, state, and actions. |
| Widget | Persistent glanceable system content with one clear purpose, lightweight interaction, and exact deep links. |
| Window | An independent, durable task or document context that can resize and coexist with other work. |

## Commonly Confused Terms

| Do not confuse | Distinction |
| --- | --- |
| Tab bar vs segmented control | Tabs change top-level destination; segments switch a few closely related modes or views. |
| Button vs Toggle | A button performs an action; a toggle represents persistent binary state. |
| Pull-down menu vs pop-up selection | A pull-down menu issues commands; pop-up/picker selection shows one current value. |
| Alert vs action sheet | An alert interrupts for critical information; an action sheet offers choices related to an initiated action. |
| Sheet vs navigation | A sheet isolates a short task; navigation moves within the app’s information hierarchy. |
| Popover vs sheet | A popover is small, anchored, and wide-layout-oriented; a sheet adapts better to compact space and longer tasks. |
| Widget vs Live Activity | A widget offers persistent periodic value; a Live Activity tracks one bounded, frequently changing event. |
| Empty vs error | Empty can be a valid content state; error means expected content or action could not complete. |
| Primary vs destructive | Primary describes task priority; destructive describes consequence. A destructive action should rarely be primary. |
