# Chapter 9: Navigation Architecture and Search

## Core Idea

Navigation helps people answer three questions: Where am I? What can I reach from here? How do I return? Choose a navigation structure that mirrors the information architecture, remains stable as content changes, and adapts from compact to wide layouts without changing the product’s meaning.

Search is navigation by intent. Give it a clear scope, a predictable location, and useful results before adding advanced filtering.

## Frameworks Introduced

### Navigation levels

- **Top-level destinations:** Independent areas of the app, commonly represented by a tab bar or adaptable sidebar.
- **Hierarchy:** Parent-to-child movement through content, commonly represented by a navigation stack or split view.
- **Peer navigation:** Movement among ordered items at the same level, sometimes represented by paging and a page control.
- **Contextual movement:** Links and actions that open the exact related object, search result, notification destination, or deep link.

### Search scope

- **Global search** crosses the app’s primary content collection.
- **Local search** filters or searches within the current collection or context.
- **Dedicated discovery search** can be a top-level destination when browsing, suggestions, and search are a central product experience.

## Key Concepts

### Keep top-level destinations stable

Use a tab bar for top-level navigation, not for commands. Keep tabs visible and enabled; when a section contains no content, show an informative empty state instead of removing the tab. A changing tab set makes the app’s map unstable.

Use a small number of concise, usually single-word labels and familiar filled SF Symbols. Avoid relying on a More overflow destination because it hides the architecture. Badges belong only on information important enough to revisit, and they must remain current.

On iPad, top-level tabs can adapt into sidebar presentation. If customization is useful, start with a focused default set—typically no more than about five primary destinations—so the initial structure stays legible.

### Use a sidebar for depth and context

A sidebar is useful for deeper, secondary navigation and can preserve scope while content changes. Keep hierarchy shallow; if it grows beyond roughly two levels, transition to a split-view detail rather than nesting disclosure indefinitely.

Let people hide or customize a sidebar when that supports their work, but do not hide it by default without a strong content reason. Use familiar symbols and labels. On iPhone, a tab bar is generally the first choice for top-level destinations; a deep hierarchy can live inside one tab.

### Preserve navigation identity

Each destination needs a clear title and a predictable back path. Do not put the app name in every navigation title. Keep titles concise—source guidance suggests roughly 15 characters where possible—and use large titles when they improve orientation, not simply as decoration.

Deep links, notifications, widgets, and search results should open the exact relevant destination while reconstructing enough hierarchy for a natural return path.

### Put search where its importance is visible

Prefer one obvious global search location. Choose placement by task:

- **Bottom placement** when search is a priority and reachability matters.
- **Top placement** when bottom content or a bottom toolbar is more important.
- **Inline placement** when search filters one local collection.
- **Dedicated tab** when discovery and search form a major product destination.

On iPad, avoid automatically focusing a search field if the software keyboard would unnecessarily cover content.

### Make search useful during entry

When feasible, update results as the person types. Offer relevant suggestions, recent searches, corrections, and likely scopes. Rank strong results first. Use tokens for common structured attributes and filters or a scope bar only when they materially improve a large result set.

Start broad unless the local context clearly establishes a narrower scope. Always show the active scope. If search history is retained, make its use clear and provide a way to clear it.

### Use page controls only for ordered peers

A page control indicates position in a short, ordered set at the same hierarchy level. It does not replace navigation for a hierarchy or arbitrary collection. When there are more than roughly ten pages, use a grid, list, thumbnail strip, or another scalable mechanism.

## Mental Models

### Destination or action

If selecting an item changes where the person is in the app, it may be navigation. If it changes data or performs a command, it is an action and belongs in a button, menu, or toolbar—not a tab.

### Stable map, flexible presentation

The destination set and labels remain stable while the presentation adapts:

- Compact: tab bar plus navigation stacks.
- Wide: sidebar-adaptable tabs or split navigation.
- Very narrow: stage hierarchy without deleting destinations.

### Scope before syntax

Before designing tokens, filters, or query language, make sure a person knows what is being searched. A sophisticated search field with ambiguous scope is still poor navigation.

## Anti-patterns

- Using tab items for Add, Search command, Play, or another action.
- Hiding or disabling an empty tab.
- More than the interface can show, with key destinations buried under More.
- Replacing navigation labels with unfamiliar icons.
- Deeply nested sidebars with several disclosure levels.
- A search field on every screen with overlapping scopes.
- Automatically opening the iPad software keyboard on page load.
- Filtering silently without showing active scope or filters.
- Search results that open a generic home screen instead of the matched item.
- Page dots for an unbounded feed.

## Implementation Bridge

- Use NavigationStack for compact hierarchical flow and NavigationSplitView for wide hierarchy.
- Use TabView for stable top-level destinations and its sidebar-adaptable style when the architecture should transform on iPad.
- Use searchable, search scopes, suggestions, tokens, and programmatic focus according to the search model.
- Model navigation state explicitly so deep links can reconstruct a valid path.
- Keep tab identity stable across authentication and empty-content states.
- Expose keyboard shortcuts for search and major destinations on iPad where appropriate.

## Decision Table

| Need | Preferred structure |
| --- | --- |
| 3–5 independent app sections | Tab bar |
| Top-level sections that should become a sidebar | Sidebar-adaptable tabs |
| Parent-child drill-down | Navigation stack |
| Persistent hierarchy plus detail | Navigation split view |
| Temporary local filtering | Inline search |
| Discovery is a primary product job | Dedicated Search destination |
| Short ordered peer set | Paging plus page control |
| More than about 10 peers | List, grid, or thumbnails |

## Worked Example: Marketplace

The draft has tabs for Home, Categories, Search, Cart, Add Listing, Messages, Orders, and Profile. Search also appears in three different headers.

Reconstruct it:

1. Keep a stable, focused top level such as Home, Browse, Sell, Inbox, and Profile; if Sell is an action rather than a destination, move it to a prominent button instead.
2. Put cart access in the relevant toolbar with a meaningful badge rather than adding another top-level destination.
3. Make Browse the dedicated discovery/search destination and expose category scope clearly.
4. Use one search model with suggestions, recent searches, filters, and exact-result deep links.
5. On iPad, let destinations adapt to a sidebar and show category hierarchy plus results in a split view.
6. If Orders are account content, place them predictably under Profile while allowing notifications and deep links to open a specific order.

## Key Takeaways

- Match top-level, hierarchy, peer, and contextual navigation to different structures.
- Keep destinations stable; adapt presentation rather than rewriting the map.
- Use tabs for destinations and controls for actions.
- Give search one clear location, explicit scope, and exact result routing.
- Preserve a natural back path for every entry point.

## Connects To

- Chapter 2: Platform Strategy
- Chapter 10: Lists, Collections, and Charts
- Chapter 11: Buttons, Menus, Toolbars, and Actions
- Chapter 15: System Experiences

## Source Focus

Navigation and search; Tab bars; Sidebars; Navigation bars; Search fields; Page controls; Split views; Toolbars; Spotlight.
