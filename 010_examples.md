# Examples

Android app repositories may include examples when they help contributors or
downstream users understand supported extension points, integration patterns, or
reusable modules.

## Location

Runnable examples should live under a top-level `./examples/` directory or in a
clearly named sample module such as `:sample`.

Examples should not live inside production source sets unless they are part of
the shipped app.

## Scope

Examples should be small, focused, and runnable from a clean checkout when
their declared dependencies are available.

Examples should use mock, synthetic, or public data. They must not include real
private user data, credentials, signing keys, production endpoints, or
environment-specific local paths.

## Verification

Important examples should have lightweight build or smoke verification when
practical.

Example verification should not require private external services, secrets, or
large local datasets.

