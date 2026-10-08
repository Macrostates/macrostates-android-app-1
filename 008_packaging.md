# Packaging

Android applications should produce ordinary Android artifacts through Gradle.

## Application Metadata

The app module should define package namespace, application ID, minimum SDK,
target SDK, version code, version name, and signing configuration deliberately.

Application ID is a public identity. Changing it creates a different installed
app from Android's perspective and should be treated as a major product and
release decision.

Application versions follow [Application Versioning](011_application-versioning.md).
That document defines the committed version source, automatic version bumps,
Android version codes, application release commits and tags, and APK names.

## Build Variants

Use standard `debug` and `release` build types unless a project-specific
package defines additional distribution or environment needs.

Debug builds may include developer conveniences that are absent from release
builds. Release builds should avoid debug-only logging, inspection endpoints,
test-only permissions, and development signing material.

## Signing

Do not commit private signing keys or production keystore passwords.

Commit safe signing configuration defaults only. Local or CI signing secrets
should come from secure local files, environment variables, or the chosen CI
secret mechanism.

## Artifacts

Debug APKs, release APKs, Android App Bundles, mapping files, generated
manifests, reports, and build outputs should not be committed unless an
explicit release workflow requires it.

Build artifacts should be generated under Gradle build output directories.

Every generated application APK filename must include the application version
and identify its build variant, as defined in
[Application Versioning](011_application-versioning.md).

## Distribution

Distribution channel requirements belong in the project-specific package when
they affect behavior, signing, metadata, privacy declarations, store listing
content, or release cadence.

If a project publishes outside an app store, document installation, update, and
signature verification expectations.
