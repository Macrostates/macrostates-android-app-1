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
- Application version storage, automatic semantic version bumps, release tags,
  and versioned APK filenames.
- README, developer documentation, and example expectations.

Project-specific product behavior, privacy policy, security model, branding,
distribution channel policy, release cadence, and user workflows belong in a
project-local package.

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
