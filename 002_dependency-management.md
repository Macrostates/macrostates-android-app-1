# Dependency Management

Android applications should keep runtime dependencies explicit and
well-maintained.

## Tooling

Use Gradle as the normal local interface for dependency resolution, builds,
tests, linting, and packaging.

Use the Gradle wrapper once the Android project is scaffolded. Wrapper files are
part of the build interface and should be committed.

Use Kotlin for application code.

Use Jetpack Compose for new UI unless a project-specific package requires a
different UI toolkit.

Use Android Jetpack libraries when they solve common platform work, including
lifecycle-aware state, camera integration, persistence, background work,
navigation, and security integration.

## Default Stack

Use these defaults for new Android applications unless a project-specific
package deliberately chooses otherwise:

- Kotlin for application code.
- Jetpack Compose for UI.
- Android Studio as the primary IDE.
- Gradle with Kotlin DSL for builds.
- Coroutines and Flow for asynchronous work and reactive state.
- ViewModel with unidirectional data flow for screen state.
- Navigation Compose for in-app navigation.
- Room when structured local persistence is needed.
- DataStore for settings and preferences.
- WorkManager for reliable deferrable background jobs.

These defaults are starting points, not mandatory dependencies for every app.
Do not add Room, DataStore, WorkManager, or Navigation Compose unless the
application has a real need for the capability they provide.

## Version Catalogs

Prefer a Gradle version catalog at `gradle/libs.versions.toml` when dependency
volume is large enough that centralized version management improves clarity.

Small applications may keep dependencies in module build files until a version
catalog would reduce meaningful duplication.

## Runtime Dependencies

Runtime dependencies should be declared in the relevant Gradle module.

Do not add a runtime dependency unless it is required by supported application
behavior. Prefer Android platform APIs and Jetpack libraries over custom
implementations for established Android concerns.

Dependencies that affect persisted formats, cryptography, export formats,
camera behavior, billing, analytics, crash reporting, networking, or user data
handling are compatibility or policy choices. Capture them in implementation
decision records when they are selected.

## Development Dependencies

Development-only tools such as test frameworks, linters, static analyzers, and
coverage tools should be separated from runtime dependencies by Gradle
configuration and module scope.

## Lockfiles

Android app repositories may commit Gradle dependency lockfiles when
reproducible builds matter for the project. If lockfiles are used, document the
normal update command and review expectations.
