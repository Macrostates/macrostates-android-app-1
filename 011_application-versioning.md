# Application Versioning

## Scope

Applications using this package follow Process's contract-based versioning policy.
Process owns the composition/implementation relationship, classification, required
release declaration, primary-branch alignment, development workflows and release
boundaries. Meta owns individual specification package versions and package tags.
This document owns only the Android integration of those rules.

Application versions are numeric `MAJOR.MINOR.REVISION`, with no prefix or suffix.
Composition versions use `spec-MAJOR.MINOR.REVISION`; specification package versions
remain independent. A package release does not release the application. This
contract-based policy replaces the former Android-owned semantic bump policy and
its automatic tag for every completed change set.

## Committed Version Source

Use the Process-owned `.macrostates/implementation/release.yaml` in the
application's repository as the single authoritative tracked declaration. Add
the required Android extension:

```yaml
version: "6.4.8"
specification: "spec-6.4.2"
release_date: "2026-09-21"
android:
  version_code: 68
```

These are hypothetical values, not a required starting version. Follow Process
for the common fields and first-baseline/adoption rules. `android.version_code`
must be a tracked integer from 1 through 2,100,000,000. Every new finalized
application version must have a higher code than the previous application's
version; rebuilding the same version or changing only specification revision
must not increase it. If artifacts share an application ID and need distinct
install ordering, document a deterministic variant scheme based on this counter
that remains in range and preserves update ordering.

Gradle must read and validate this declaration, deriving:

- `versionName` and the APK filename version from `version`.
- `versionCode` from `android.version_code` (or the documented variant mapping).
- The app's exposed release date from `release_date`.

Validate the common version syntax and matching Major.Minor of `version` and
`specification`, the real calendar date, and the Android integer/range. Reject
missing, malformed or ambiguous declarations with a useful build error. Do not
keep competing hand-edited constants in Gradle, properties, resources or CI.
Expose version/date information through generated build metadata when the app
uses it in Settings, file metadata or other features.

A clean checkout must provide all release metadata without Git, network access,
local settings, or manually supplied parameters. Ordinary builds must not modify
versions, dates, counters, commits or tags. Primary-branch and release checks
compare against the composition under Process; a development build may target an
older implemented contract while its branch specs describe documented pending
work. The build's declaration must still describe its implemented baseline honestly.

## Automatic Version Bumps

Apply Process's automatic classification and version-update rules for every
coherent change set. The implementer updates the Android counter and release date
alongside any required implementation version bump. Keep the revision independent
from the composition's revision; no Android rule may independently choose a
conflicting Major.Minor or infer it from a package version.

Implementation-only fixes, dependency/configuration changes or rewrites preserving
the effective contract use an implementation revision. Contract changes use the
shared Major/Minor determined by Process. Specification-only editorial work and
non-shipped documentation/test maintenance do not force an application release.
Record the classification and checks in the workflow. Repeated builds and
intermediate corrections within one uncommitted change set do not bump again.

## Application Release Commits And Tags

Follow Process for commit alignment, release readiness, annotated application and
composition tags, and publication. Normal versioned commits do not automatically
create release tags. Builds never create either. Repository rules still govern
Git operation authorization, and creating a merge request does not authorize its
merge or remote release publication.

For an authorized application release, verify that its committed declaration,
Android counter, release date, implementation, specification baseline and relevant
verification evidence describe the same candidate. Use Process's implementation
release tag convention, normally `vMAJOR.MINOR.REVISION`, in the app repository.
Keep package releases in their own source repository and namespace. Never move or
reuse a published tag for changed source. Confirm the remote commit/tag identities
when publication is authorized, and distinguish pending/local from published state.
Release tagging and workflow closure remain separate.

## APK Filenames

Every generated application APK, including debug and release outputs, must have
a deterministic filename containing the application identifier or readable
artifact name, exact implementation version, and build variant. For example:

```text
example-1.2.3-debug.apk
example-1.2.3-release.apk
example-1.2.3-demo-release-arm64-v8a.apk
```

Include flavor, split, ABI, or other output qualifiers when needed to prevent
filename collisions. Keep the implementation version itself unchanged; variant
qualifiers belong elsewhere in the filename. Configure the normal build flow
to produce these names automatically, without manual renaming. Keep artifacts
under Gradle build output directories and out of Git unless an explicit artifact
publication policy says otherwise.

## Verification

For version-affecting implementation or build changes, verify that:

- The selected classification follows Process and the baseline reference is accurate.
- The declaration validates and its Android counter preserves installation ordering.
- Gradle consumes the declaration without competing hand-edited metadata.
- Built APK version name/code and exposed release date match the declaration.
- APK filenames contain the same version and distinguish variants/splits; exercise
  configured naming for debug and release when available.
- Rebuilds do not mutate the declaration, counter, date or Git state.
- Primary-branch integration passes Process's alignment and readiness checks.

For an authorized release, additionally verify the annotated application tag,
referenced composition tag, source snapshot and any authorized remote publication.
Report checks that could not run and why. Specification edits alone do not require
building or releasing an application. Record an unimplemented declaration/build
migration explicitly and follow Process's adoption procedure before claiming or
committing the first aligned primary-branch baseline.
