# Testing

Android applications should test behavior at the cheapest level that gives
useful confidence.

## Unit Tests

Unit tests should cover platform-independent business rules, models,
repositories with fake data sources, reducers, serializers, validation, and
edge cases that users or persisted data depend on.

Unit tests should live under module `src/test/`.

## Integration Tests

Integration tests should cover boundaries between application code and local
storage, databases, files, background work, dependency injection, or other
non-trivial adapters.

Use focused integration tests rather than relying only on end-to-end UI tests
for behavior that can be verified without a device.

## Instrumentation Tests

Instrumentation tests should cover Android framework behavior that cannot be
verified reliably on the host JVM.

Instrumentation tests should live under module `src/androidTest/`.

## UI Tests

UI tests should cover critical user workflows, permission states, navigation,
and important Compose state rendering where regressions would be costly.

Do not make every visual detail an end-to-end test. Prefer stable semantic
assertions and targeted screenshot tests only when visual regressions matter.

For input workflows, verify with a visible software keyboard that the primary
action remains on screen, unobstructed, and tappable without scrolling to find
it or hiding the keyboard. Exercise focus changes, validation/error states,
keyboard show/hide, and constrained layouts such as landscape or enlarged text.
Checking only the keyboard-hidden layout or invoking semantic click actions
without checking actual visible bounds does not establish keyboard safety.

## Compatibility Tests

Persisted formats, exported artifacts, manifest contracts, and documented
workflows should have regression tests or documented manual checks where
practical.

## Verification Commands

Once scaffolded, the repository should document commands for:

- Building a debug artifact.
- Running unit tests.
- Running instrumentation tests when they exist.
- Running Android Lint.
- Running formatting or lint checks configured by the project.

