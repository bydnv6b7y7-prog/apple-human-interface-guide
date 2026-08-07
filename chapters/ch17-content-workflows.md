# Chapter 17: Files, Sharing, Drag and Drop, Search, Undo, and Multitasking

## Core Idea

Content workflows should cooperate with the system and with other apps. Use platform file, sharing, search, drag-and-drop, collaboration, and undo behaviors so people can move work across contexts without learning app-specific transfer rituals or fearing data loss.

## Frameworks Introduced

### Content lifecycle

1. **Create or import.**
2. **Find and open.**
3. **Edit with autosave and undo.**
4. **Move, duplicate, or organize.**
5. **Share or collaborate.**
6. **Resume across windows, apps, and interruptions.**

### Transfer fidelity

When exporting or dragging, offer representations from highest to lowest useful fidelity:

- Native editable object.
- Standard structured document or rich representation.
- Image, text, URL, or other broadly compatible representation.

The destination can choose the best format it supports.

## Key Concepts

### Cooperate with Files

Use system open, import, export, and document-picker experiences. Use familiar New, Open, and Add labels and show file types or constraints only when they matter.

Autosave continuously where practical so people do not manage a fragile explicit Save cycle. Preserve document identity, recent locations, and conflict state. Use Quick Look for standard preview rather than rebuilding a viewer.

If the app needs a custom browser for domain content, keep Files integration available and follow familiar navigation, selection, naming, sorting, and location behavior.

### Share through the system

Use the system Share experience or ShareLink. Provide the actual content, a useful preview, and only relevant app-specific activities. Do not duplicate copy, print, save, AirDrop, Messages, or other system actions.

Label custom activities with concise verbs. Sharing permissions should be easy to compare and summarized in plain language. After collaboration begins, provide a familiar collaboration entry point and show current participants or access without exposing sensitive details unnecessarily.

### Support drag and drop where content has a destination

Drag and drop should work within the app and across apps when the content model allows it. Keep an alternative button or menu path.

Expected semantics:

- Within the same container, dragging commonly moves.
- Across containers or apps, dragging commonly copies.
- Multiple selected items can travel together.
- Source selection remains understandable.
- Valid destinations highlight before drop.
- Insertion position or replacement consequence is visible.
- A failed drop returns or explains itself.
- Long asynchronous imports show progress and can recover.

Support several representations so a rich destination can receive editable content while a simple destination can receive text or an image.

### Make search part of the content lifecycle

Index content that people expect to retrieve through app search and Spotlight. Open the exact object and reconstruct a valid navigation path. Keep search history and indexed metadata privacy-aware, remove stale items, and support useful filters only after scope and ranking are strong.

### Make undo predictable

Support multiple undo and redo for editing and organizational changes where feasible. Use standard gestures, menus, and keyboard commands and describe the result with clear labels such as “Undo Move Card.”

Do not redefine system undo gestures. Keep the model deterministic: undo reverses the last relevant operation in the active context, restores selection when possible, and does not silently discard unrelated later work.

For common deletions, undo is often better than an alert. For irreversible or externally committed operations, use proportionate confirmation.

### Survive multitasking and interruption

When the app becomes inactive:

- Pause attention-dependent media, games, and animation.
- Finish or safely suspend user-initiated background work.
- Persist drafts, navigation, selection, and scroll context.
- Avoid notifications for state the person will see immediately on return.
- Resume without making people reconstruct the task.

Support resizable iPad windows, drag and drop between apps, multiple documents where valuable, and Picture in Picture for qualifying media.

## Mental Models

### Ownership and destination

For each content operation, define:

- Who owns the canonical object?
- Is the operation move, copy, link, or export?
- What survives if the app closes?
- What format and permissions reach the destination?
- Can the operation be undone?

### No dead-end content

A person should be able to locate, preview, move, share, and recover their work using familiar system paths. Proprietary storage should not make ordinary content feel trapped.

### Resume contract

Record the minimum state required to return naturally: document, selection, edit draft, navigation path, window, and in-flight operation. Do not persist sensitive transient data unnecessarily.

## Anti-patterns

- A custom file browser as the only way to reach documents.
- Explicit Save required after every minor edit.
- Rebuilt sharing grid that omits system destinations.
- Sharing a screenshot when an editable representation exists.
- Drag and drop with no visible destination or non-drag alternative.
- A drop silently turning move into copy or replacing content.
- One-level undo that loses selection and context.
- Alerting before every undoable deletion.
- Returning from multitasking to the home screen instead of the active task.
- Notifications announcing completion while the same result is foreground and visible.

## Implementation Bridge

- Use documentGroup, fileImporter, fileExporter, fileMover, Quick Look, or corresponding UIKit document APIs.
- Use Transferable, ShareLink, draggable, dropDestination, item providers, and multiple representations.
- Use UndoManager and standard Undo/Redo command exposure.
- Use Core Spotlight for durable searchable content and route results through the navigation model.
- Persist scene-specific state for independent windows and use background task APIs only for legitimate user work.
- Test cancellation, duplicates, naming conflicts, offline state, external file changes, large imports, app termination, and cross-app transfer.

## Decision Table

| Need | System-first approach |
| --- | --- |
| Open/import document | File importer or document picker |
| Save/export copy | File exporter |
| Preview standard file | Quick Look |
| Share content | ShareLink/system activity view |
| Move rich content | Drag and drop with Transferable representations |
| Reverse edit | UndoManager and standard commands |
| Find app content | In-app search plus Core Spotlight |
| Resume parallel documents | Scene/window state |

## Worked Example: Whiteboard App

The app stores boards only in a private gallery, exports screenshots, requires drag for arranging objects, and loses the current board when backgrounded.

Reconstruct it:

1. Autosave boards and restore the active board, selection, zoom, and edit history appropriately.
2. Support file import/export in a native editable format plus PDF and image representations.
3. Use the system share view and provide a meaningful preview.
4. Support drag and drop for images, text, URLs, and native board objects, with explicit Add/Import alternatives.
5. Highlight valid canvas regions and show progress for large imports.
6. Add labeled Undo/Redo, keyboard commands, and reversible delete.
7. Index board titles and permitted metadata in Spotlight and deep-link to the exact board.
8. On iPad, allow separate board windows only when simultaneous reference or editing is valuable.

## Key Takeaways

- Use system file, sharing, preview, search, and transfer experiences.
- Autosave work and provide predictable multi-step undo.
- Support rich drag-and-drop representations plus visible alternatives.
- Define move/copy/export semantics before implementation.
- Restore the exact work context after interruption and across windows.

## Connects To

- Chapter 9: Navigation and Search
- Chapter 14: Inputs and Interactions
- Chapter 15: System Experiences
- Chapter 18: Media and Full-Screen Experiences

## Source Focus

File management; Collaboration and sharing; Drag and drop; Undo and redo; Multitasking; Searching; Spotlight; Activity views; Quick Look.
