# Android app specification package

This package describes reusable conventions for Android applications. It
defines the project shape, build posture, app architecture, quality gates,
packaging expectations, documentation expectations, and example placement
needed by Android apps.

## Macrostates

This package is part of Macrostates, a project for composing reusable
specification packages into specs-driven development projects.

## Scope

- Android project layout and module boundaries.
- Gradle, Kotlin, Android Gradle Plugin, and dependency posture.
- Application architecture and Android platform surface ownership.
- Formatting, linting, and static analysis expectations.
- Unit, integration, instrumentation, and UI test expectations.
- Debug, release, signing, and packaged artifact expectations.
- Android integration of Process's contract-based versioning and authoritative
  release declaration: version name/code, release date and versioned APK filenames.
- README, developer documentation, and example expectations.

Project-specific product behavior, privacy policy, security model, branding,
distribution channel policy, release cadence, and user workflows belong in a
project-local package.

## Macrostates artifacts

Follow the selected Meta package's project layout: numbered specification
packages and the project entrypoint are tracked under `.macrostates/specs/`.
Implementation documentation, decisions, workflows and release declarations,
when required by project rules, live under `.macrostates/implementation/`.
Application source, tests, build configuration and runtime configuration retain
their language/tool locations outside `.macrostates/`. This package does not
make the Macrostates CLI mandatory or change the scope of a subproject.

## Reading order

1. [Project Layout](001_project-layout.md)
2. [Dependency Management](002_dependency-management.md)
3. [Application Surface](003_application-surface.md)
4. [Formatting](004_formatting.md)
5. [Linting](005_linting.md)
6. [Static Analysis](006_static-analysis.md)
7. [Testing](007_testing.md)
8. [Packaging](008_packaging.md)
9. [Documentation](009_documentation.md)
10. [Examples](010_examples.md)
11. [Application Versioning](011_application-versioning.md)

## License

This specification package, including its documentation, metadata, and bundled
resources, is licensed under the [MIT License](LICENSE).

Copyright (c) 2026 Lucas Lopez.

## AI assistance

This project was developed with AI assistance.
