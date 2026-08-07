# Chapter 2: iOS and iPadOS Platform Strategy

## Core Idea

An Apple-platform app should preserve its product identity while feeling intentionally made for the device in use. iPhone and iPad share many components, but they create different physical, spatial, and multitasking conditions. Responsive resizing alone is not enough; hierarchy, control placement, density, input, and workflow need to adapt.

## Frameworks Introduced

### iPhone context

- A medium-size, high-resolution display viewed at close range.
- Often held in one or two hands and used in portrait, sometimes landscape.
- Primarily Multi-Touch, with keyboard, voice, and accessibility inputs also possible.
- Used in both very short checks and sustained sessions.

### iPad context

- A large, high-resolution display used handheld, on a stand, or at a greater viewing distance.
- Resizable windows, multitasking, external displays, and multiple app windows.
- Touch, keyboard, pointer, Apple Pencil, voice, and combinations of inputs.
- Rich inter-app workflows such as drag and drop.

## Key Concepts

### Design one product, not one frozen canvas

Define stable product concepts—content model, action hierarchy, terminology, and state—then select platform-appropriate presentation. The same task may use a pushed detail on iPhone and a persistent secondary column on iPad.

### iPhone: prioritize and stage

Screen space and one-handed reach make hierarchy decisive:

- Keep essential content and the current task prominent.
- Reveal secondary information with a small, predictable interaction.
- Place frequent controls where they are comfortably reachable, often near the middle or bottom.
- Preserve familiar gestures such as swipe to go back and contextual row actions.
- Support portrait and landscape when the task benefits; do not treat landscape as a scaled portrait screenshot.
- Adapt to Dynamic Type, Dark Mode, safe areas, the Dynamic Island, and Display Zoom.

### iPad: expose context without filling space

The larger canvas is an opportunity for context and parallelism, not inflated padding:

- Prefer sidebars, split views, inspectors, popovers, and resizable panes when they reduce navigation.
- Keep content central and controls available without crowding it.
- Preserve the full hierarchy across window sizes as long as it remains usable.
- Collapse tertiary content and inspectors before collapsing primary navigation.
- Test half, third, quadrant, portrait, landscape, Stage Manager, external-display, and keyboard scenarios.
- Support multiple windows when separate documents or tasks benefit from independent context.

### Input methods can coexist

Do not design “touch mode” and “keyboard mode” as mutually exclusive. A person may point with Apple Pencil, type with a hardware keyboard, scroll with a trackpad, and invoke an accessibility command in one session.

Provide:

- Adequate touch targets.
- Pointer feedback for interactive regions.
- Keyboard traversal and shortcuts for important commands.
- Standard gestures plus discoverable alternatives.
- Hover-only enhancement, never hover-only access.
- Consistent focus and selection state across input changes.

### Viewing distance changes density

Controls that are comfortable under a finger at close range can feel oversized when an iPad sits on a desk. Conversely, a dense desktop-style layout can become difficult when used by touch. Choose density from expected viewing distance, precision, and task—not device class alone.

## Mental Models

### Preserve, reveal, collapse

For every region, assign one behavior:

- **Preserve:** essential content and the primary action.
- **Reveal:** useful secondary context through a sheet, inspector, disclosure, or popover.
- **Collapse:** tertiary controls into an overflow menu or later step.

Make these decisions before coding breakpoints.

### Content, navigation, utility

Classify each area of an iPad layout:

- **Navigation** establishes location and scope.
- **Content** is the object or task people came for.
- **Utility** modifies or inspects content.

When width decreases, protect content first, then preserve enough navigation to maintain orientation; utility typically collapses first.

### Capability, not device-name branching

Prefer environment-driven decisions such as available width, size class, input availability, scene configuration, and content needs. A compact iPad window can resemble iPhone constraints; a large iPhone in landscape does not automatically need an iPad hierarchy.

## Anti-patterns

- Scaling an iPhone page proportionally to fill iPad.
- Centering a narrow phone column on iPad while ignoring useful context.
- Showing every control permanently because space exists.
- Hiding the iPad sidebar by default without a task reason.
- Detecting “iPad” and assuming a fixed full-screen size.
- Supporting pointer hover while leaving keyboard focus invisible.
- Requiring a gesture with no visible or accessible alternative.
- Using separate feature sets that make the same product concept behave inconsistently across Apple devices.

## Implementation Bridge

Use SwiftUI’s environment and containers as policy mechanisms:

- **NavigationStack** for staged navigation.
- **NavigationSplitView** for sidebar/content/detail hierarchies.
- **TabView** with the sidebar-adaptable style when top-level tabs should become sidebar navigation at larger widths.
- Scene APIs for multiple windows when independent work contexts are valuable.
- Focus, keyboard shortcut, hover, drag-and-drop, and accessibility modifiers to make inputs complementary.
- Auto Layout, size classes, and trait collections when implementing in UIKit.

Avoid branching on screen pixel dimensions. Build representative previews and UI tests for compact and regular widths, large Dynamic Type, long localized text, and both orientations.

## Decision Table

| Product need | Compact presentation | Wide presentation |
| --- | --- | --- |
| Top-level destinations | Tab bar | Tab bar or sidebar-adaptable tabs |
| Deep hierarchy | Navigation stack | Sidebar or split view |
| Supplementary settings | Sheet | Inspector, popover, or side panel |
| Compare related items | Staged detail or paging | Adjacent columns when comparison benefits |
| Complex editing | Full-screen or large sheet | Dedicated window or content-plus-inspector |
| Independent documents | One active flow | Multiple windows when context should persist |

## Worked Example: A Reading App

The product has Library, Discover, and Profile destinations; a book list; a reader; and typography controls.

On iPhone:

- Use a tab bar for the three top-level destinations.
- Push from Library into the reader.
- Present typography controls in a sheet sized to the task.
- Keep the reading surface edge-to-edge and place frequent reader controls within reach.

On iPad:

- Let the top-level tab structure adapt to a sidebar.
- Use a split view so library selection and book detail can remain visible when space permits.
- Open the reader as the content focus; expose typography as a popover or inspector in wide layouts.
- Support keyboard page commands, pointer feedback, Pencil selection where relevant, drag-and-drop imports, and multiple book windows only if simultaneous reading is a real workflow.

When the iPad window becomes compact, the hierarchy stages naturally instead of squeezing three columns.

## Key Takeaways

- Preserve product concepts while adapting presentation to physical context.
- Prioritize and stage on iPhone; expose useful context and parallelism on iPad.
- Design for resizable windows and mixed inputs, not fixed device screenshots.
- Collapse utility before content and preserve orientation through every size.
- Choose structure from capability and task, not only device name.

## Connects To

- Chapter 3: Layout and Adaptivity
- Chapter 9: Navigation and Search
- Chapter 13: Modality and Presentation
- Chapter 14: Inputs and Interactions

## Source Focus

Designing for iOS; Designing for iPadOS; Layout; Multitasking; Windows; Navigation and search; Sidebars; Tab bars.
