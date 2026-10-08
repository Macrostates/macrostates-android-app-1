# Static Analysis

Android applications should use static checks where they improve confidence in
behavior, API compatibility, and release quality.

## Kotlin And Compiler Checks

Treat Kotlin compiler warnings as signals to inspect. Projects may promote
warnings to errors when the team can sustain that posture without blocking
ordinary work on noisy third-party or generated code.

Prefer explicit nullability, sealed state models, and typed boundaries for
application states that users or persisted data depend on.

## API And Compatibility Checks

If the repository exposes reusable modules, libraries, plugins, or public APIs
for other applications, document the compatibility surface and add API checks
when practical.

For app-only repositories, the main compatibility surfaces are persisted data,
exported files, manifest behavior, permissions, deep links, widgets, shortcuts,
and user-visible workflows.

## Security-Sensitive Checks

Projects with privacy, cryptography, authentication, network, payment, or
personal-data behavior should identify security-sensitive code paths and define
additional verification expectations in a project-specific package or
implementation decision record.

