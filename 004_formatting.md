# Formatting

Android applications should use automated formatting for Kotlin, Gradle, and
XML files where practical.

## Kotlin

Use a project-configured Kotlin formatter, such as ktfmt or Spotless with a
Kotlin formatter backend.

Formatting rules should be deterministic and runnable from the command line.

## Gradle And XML

Gradle build files and Android XML resources should follow consistent, boring
formatting.

Generated files should not be manually reformatted unless the generator expects
that workflow.

## Style

Prefer consistency over local personal style. Formatting should remove review
noise rather than become a source of debate.

