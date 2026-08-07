# Chapter 11: Buttons, Menus, Toolbars, and Actions

## Core Idea

Actions need clear priority, predictable placement, and a control whose behavior matches the choice. Buttons expose immediate actions; menus organize related commands; toolbars keep frequent actions near content; system share and quick-action surfaces extend tasks beyond the page.

## Frameworks Introduced

### Action hierarchy

- **Primary:** The most likely action that advances or completes the current task.
- **Secondary:** Useful alternatives that deserve visible access but less emphasis.
- **Tertiary:** Infrequent or contextual commands suitable for an overflow or context menu.
- **Destructive:** An action that removes data or has difficult-to-reverse consequences; this is a role, not a priority.

### Menu families

- **Pull-down menu:** Commands related to the invoking button.
- **Pop-up button:** A flat set of mutually exclusive values that shows the current selection.
- **Context menu:** Secondary shortcuts for the selected object or region.
- **Edit menu:** Standard text/content editing operations.
- **Action sheet or confirmation dialog:** Choices that clarify an intentional action, especially where consequences need attention.
- **Activity or share view:** System-provided sharing and related activities.

## Key Concepts

### Make buttons easy to hit and predict

On iOS, provide a hit region of at least 44 by 44 points. A custom button needs a visible press state, focus behavior where relevant, disabled behavior, and an accessibility role.

Label a button with a concise verb or result. Use a familiar symbol without text only when the meaning is clear in context. If the button begins work, update it to communicate progress—for example, “Checkout” can become “Checking out…”—and prevent accidental duplicate submissions without making the page appear broken.

### Limit visual competition

Most pages need only one or two visually prominent buttons. Distinguish priority through standard style, tint, and placement rather than making several oversized calls to action. Never style a destructive command as the page’s primary invitation.

Disabled controls should be used when the prerequisite is evident and nearby. If the person cannot understand why an action is unavailable, explain the condition or keep the action available and validate at the appropriate moment.

### Build deliberate toolbars

Put frequent, context-relevant actions in the toolbar and move secondary commands to overflow. Source guidance recommends a restrained structure—roughly no more than three logical groups—and at most one prominent trailing action.

Use standard components and SF Symbols. Keep titles concise and avoid putting the app name in the navigation title. Do not add custom backgrounds, borders, or per-item colors that compete with the system control layer.

Toolbar contents should change only when context genuinely changes, and important commands should not jump unpredictably between visible and overflow positions.

### Keep menus short and ordered

Write menu items as verbs or verb phrases. Put high-priority commands first, group related items, and place destructive commands last with the destructive role. Use an ellipsis when the command opens another interface to gather information before completion.

Keep submenu depth to one level. If a submenu grows beyond roughly five items or represents navigation, reconsider the structure.

### Do not hide primary actions in menus

A pull-down menu becomes worthwhile when a control has several related commands, commonly three or more. It is not a good home for the only route to a primary task. A generic More button reduces discoverability; use it for truly secondary commands and preserve specific visible actions where frequency or consequence warrants.

### Use context menus as accelerators

A context menu is a shortcut, not the sole access path. Every command should also be available through the main interface or another discoverable route. Show only commands relevant to the selected object, use at most one submenu level, and put destructive actions last.

Do not attach both a context menu and an edit menu to the same item when their behaviors would conflict.

### Use the system share experience

Invoke the system activity/share view with the standard Share symbol. Provide relevant content and app-specific activities without duplicating system actions. Label custom activities with concise verbs.

### Keep Home Screen quick actions focused

Offer up to four predictable, high-value tasks people may want before opening the app. Use concise labels and familiar symbols. Quick actions should deep-link to the exact task, not merely launch the home page.

## Mental Models

### Frequency × consequence

- High frequency, ordinary consequence: visible button or toolbar item.
- Low frequency, ordinary consequence: menu.
- High consequence: explicit label and proportionate confirmation or undo.
- Object-specific shortcut: context menu plus a discoverable main route.

### Choice or command

A pop-up button chooses a persistent value. A pull-down menu issues commands. A segmented control changes a closely related state or view. An action sheet clarifies an initiated action. Choosing the wrong model makes people unsure whether something will happen immediately.

### One visual winner

Blur the page mentally. One action should remain the obvious next step. If three colorful buttons demand equal attention, the product has not resolved priority.

## Anti-patterns

- Several equal filled buttons on one page.
- Red, prominent styling for routine deletion.
- Symbol-only buttons with unfamiliar or ambiguous meaning.
- Touch targets equal to the visible glyph.
- A toolbar crowded with separators and many isolated groups.
- Primary actions hidden behind More.
- Long menus with multi-level submenus.
- Context menus as the only way to edit, share, or delete.
- A pull-down menu used for a mutually exclusive setting without showing the current value.
- Rebuilding the Share sheet or duplicating its system actions.

## Implementation Bridge

- Use Button roles and standard button styles before custom gesture handlers.
- Use ToolbarItem placements and ToolbarItemGroup to express semantic placement.
- Use Menu and Picker according to command-versus-selection semantics.
- Use contextMenu only as an accelerator; expose equivalent row, toolbar, or detail actions.
- Use ShareLink or the system activity controller for sharing.
- Update labels, disabled state, and progress from the same action state to prevent duplicate execution.
- Add keyboard shortcuts to important commands on iPad and make menu terminology match visible buttons.

## Decision Table

| Need | Control |
| --- | --- |
| One immediate action | Button |
| Frequent action on current content | Toolbar button |
| Several related commands | Pull-down Menu |
| One value from a flat set | Picker/pop-up presentation |
| Secondary object shortcuts | Context menu |
| Clarify an intentional risky action | Action sheet/confirmation dialog |
| Share content | System share view |
| Start a predictable task from Home Screen | Quick action |

## Worked Example: Document Editor

The draft shows Save, Export, Share, Rename, Duplicate, Move, Archive, and Delete as equally styled buttons above the document.

Reconstruct it:

1. If editing autosaves, remove Save and show a quiet persistent save state.
2. Keep Share visible because it is frequent and recognizable.
3. Put Rename, Duplicate, Move, Export, and Archive in a clearly labeled overflow menu, ordered by frequency.
4. Put Delete last with a destructive role and use undo or proportionate confirmation according to reversibility.
5. Add relevant context-menu shortcuts to the document list, but keep every command accessible in the document interface.
6. On iPad, provide familiar keyboard shortcuts and keep command names identical across menu, toolbar, and shortcuts.

## Key Takeaways

- Resolve action priority before choosing style or placement.
- Keep one visual winner and make destructive role distinct from primary priority.
- Use the menu type that matches command, selection, context, or confirmation.
- Treat context menus as shortcuts and More as secondary space.
- Prefer system toolbars, sharing, symbols, and keyboard command behavior.

## Connects To

- Chapter 9: Navigation and Search
- Chapter 12: Forms and Data Entry
- Chapter 13: Modality and Presentation
- Chapter 14: Inputs and Interactions

## Source Focus

Buttons; Toolbars; Menus; Pull-down buttons; Pop-up buttons; Context menus; Edit menus; Action sheets; Activity views; Home Screen quick actions.
