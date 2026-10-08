# Application Surface

Android applications should keep platform entrypoints small and make
application-owned components responsible for durable state and business rules.

## Entry Points

Prefer a single-activity app unless a project-specific requirement justifies
multiple activities.

Activities, services, receivers, and providers should coordinate with
application-owned components instead of owning durable data or business rules
directly.

The Android manifest is a compatibility surface. Changes to exported
components, permissions, intent filters, backup behavior, package visibility, or
minimum SDK should be deliberate and reviewed.

## Architecture

Use clear UI and data layers. Add a domain layer when shared or complex
business rules would otherwise leak into UI or storage code.

UI state should be derived from explicit models and exposed through state
holders such as ViewModels. User actions should flow back to the owner of the
relevant state.

Prefer unidirectional data flow for screen state: state flows from state owners
to UI, and events flow from UI back to the owner that can validate and apply
changes.

Each persistent data type should have a single source of truth. The source of
truth owns mutation and exposes immutable state or query results to the rest of
the app.

## UI

Compose UI should keep rendering, state collection, and event dispatch clear.
Composable functions should not own long-lived business state or perform
surprising I/O as part of rendering.

User-visible state should account for loading, empty, error, denied-permission,
and unavailable-platform states where those states can occur.

## Navigation

Use Navigation Compose for in-app navigation in Compose-first applications
unless a project-specific package chooses another navigation approach.

Navigation state and route arguments are compatibility surfaces when they are
used by deep links, notifications, widgets, shortcuts, or other external entry
points.

## Permissions

Request only permissions required for the current user-visible feature set.

Permission prompts should be tied to user intent and should have a clear
fallback or blocked state.

Permissions are part of the public application contract. Adding a permission
should be treated as a meaningful user-facing change.

## Camera

Use CameraX for camera preview and media capture unless a project-specific
requirement cannot be satisfied through CameraX.

Camera behavior must account for Android lifecycle changes, permission denial,
camera unavailability, orientation changes, and process recreation.

## Platform Boundaries

Keep dependencies on Android framework APIs near platform-facing components.
Business rules should be testable without launching Android UI when practical.
