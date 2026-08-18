# E-task development guide

This repository contains the Windows-first E-task desktop application.

## Product source of truth

Build only features that belong to the E-task product. Do not turn the app into a generic productivity suite.

Core product model:
- Project → Task only in v1; no deeper nesting.
- Only one task can actively track time at once.
- Main task states: To do, In progress, Completed.
- Start/Resume starts a focus session.
- Stop ends the current session without completing the task; paused/stopped time is not counted.
- Completed records time and completes the task.
- Delete requires confirmation and removes the task's tracked time from aggregates.
- Focus presets: 5 / 10 / 15 minutes plus configurable custom presets.
- The selected duration is a target, never a hard stop. Time continues after the target.
- Longer focus is positive: Start → Focus → Flow → Deep Work. Avoid punishment/red-overdue semantics.
- Show current session time plus accumulated task/project/global time.
- Analytics periods: today, week, month, year, all time; retain historical yearly totals and support comparisons.
- Skill/experience tracking is based on tracked practice hours and is not a professional certification.
- Local-first and offline-first. SQLite is the primary source of truth.
- Closing the main window should leave the app running in the Windows tray when appropriate.
- Timer calculations must be timestamp-based rather than persisted once per second.
- MCP/AI integration should eventually support read/analyze/create/edit/reorder/complete/delete. Meaningful or destructive changes require an explicit confirmation flow; low-risk metadata edits may be allowed without confirmation.

## Navigation and visual direction

Main sections:
- Home
- Projects
- Analytics
- Skills
- Settings

Use a horizontal, rounded, icon-first top navigation. Do not add Calendar, Notes, Goals, Meetings, generic Reports, or an Integrations page unless explicitly added to the product spec later.

The UI is a dashboard-first personal productivity control center:
- strong Current Task hero card
- varied card sizes
- large, glanceable numbers
- progress bars, gauges and compact charts where useful
- solid rounded cards; no glassmorphism
- light and dark themes
- dark theme should be near-black/graphite with a selective accent
- current preferred accent family: curated yellow palette
- Current Task should emphasize the immediate action and progress, not deadline pressure
- primary timer visual: circular gauge plus secondary linear stage indicator
- dashboard cards should eventually be rearrangeable/hideable
- app should support compact and expanded layouts

## Engineering direction

Initial stack:
- Tauri 2
- React
- TypeScript
- Vite
- SQLite via official Tauri SQL plugin

Priorities:
1. Correct timer/session model and data integrity.
2. Fast startup and low background CPU/RAM.
3. Clear component boundaries and typed domain models.
4. Accessible keyboard/mouse interactions.
5. Avoid unnecessary dependencies, animation loops, polling, and background work.
6. Keep data-layer APIs separate from UI components so MCP can use the same application services later.

## Coding rules

- TypeScript strict mode.
- Prefer small typed modules over large components.
- Domain types and application services must not depend on React.
- UI may use mock/demo data until the persistence layer is wired, but clearly isolate mocks.
- Never fake persistence: once SQLite is connected, all writes should go through the repository/service layer.
- Add migrations rather than modifying existing database schemas in place.
- Keep all timer math testable as pure functions where possible.
