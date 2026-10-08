# Project Layout

Android applications should use the standard Gradle Android project layout.

## Directory Structure

A single-application repository should normally use this shape:

```text
settings.gradle.kts
build.gradle.kts
gradle/
gradlew
gradlew.bat
app/
  build.gradle.kts
  src/
    main/
      AndroidManifest.xml
      kotlin/
      res/
    test/
      kotlin/
    androidTest/
      kotlin/
```

Use Kotlin DSL for Gradle build files unless a project-specific package chooses
Groovy deliberately.

The root project owns shared build configuration. The `app` module owns the
Android application artifact.

## Modules

Start with one `app` module unless a project-specific requirement or meaningful
implementation boundary justifies additional modules.

Additional modules should have clear ownership, such as:

- `:core:model` for platform-independent models.
- `:core:data` for repositories and local data sources.
- `:core:domain` for reusable business rules.
- `:feature:<name>` for large independently owned feature areas.

Do not split modules merely to imitate a large app. Module boundaries should
reduce coupling, improve testability, or make ownership clearer.

## Source Organization

Application code should be organized by responsibility and stable boundary.
Avoid placing all behavior directly in an `Activity`, Compose screen, or
platform callback.

Prefer packages that make architectural ownership visible, such as:

```text
ui/
data/
domain/
platform/
```

Project-specific naming may differ, but the chosen layout should make UI,
business behavior, persistence, and Android integration boundaries easy to
recognize.

## Generated And Local Files

Generated build outputs belong under module `build/` directories and must not
be committed.

Local SDK paths and machine-specific settings belong in local files such as
`local.properties` and must not be committed.

