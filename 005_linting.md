# Linting

Android applications should use linting to catch likely bugs, platform
misconfigurations, and maintainability issues.

## Android Lint

Use Android Lint as the baseline linter for Android framework, manifest,
resource, accessibility, localization, and API usage checks.

Lint should run from the command line and be included in the documented local
verification flow once the project is scaffolded.

## Kotlin Lint

Use a Kotlin linter such as ktlint or Detekt when it materially improves code
quality beyond formatting and Android Lint.

Lint rules should prioritize correctness, readability, import hygiene, and
Android maintainability. Avoid broad rule sets that create noise without
improving the application.

## Suppressions

Suppression comments or baselines should be narrow. When the reason is not
obvious, document why the warning is intentionally accepted.

Lint baselines should not become a place to hide new warnings by default.

