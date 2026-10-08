# Application Versioning

## Scope

These rules apply to applications using this package. Application versions
identify the app, independently of this specification package's own version and
release tags. A specification package release does not release an application.

## Committed Version Source

Each application must have one authoritative, tracked version declaration in
its application repository. The normal location is the application's Gradle
build configuration; a dedicated version file read by Gradle is also valid.
Document the chosen location. Do not maintain competing hand-edited copies.

The application version must use exactly `Major.Minor.Patch`: three non-negative
decimal integers separated by periods, without leading zeroes, prefixes, or
suffixes. For example, `0.1.0`, `1.0.0`, and `2.3.4` are valid. Use `0.1.0` for
a new application's initial development version unless the project specifies
another starting version.

Gradle's application `versionName` and APK filename version must come from that
same declaration. A clean checkout must provide the version without requiring
Git tags, network access, local settings, or manually supplied build parameters.
The version is committed source data; ordinary builds must not bump it or create
commits or tags.

Maintain an Android `versionCode` alongside the semantic version, either as a
tracked positive integer or through a documented deterministic mapping. Every
new application version must have a version code greater than the previous
version's code, within Android's supported range. Rebuilding the same source
version must not increase it. If artifacts share an application ID and require
distinct install ordering, document a version-code scheme that preserves it.

## Automatic Version Bumps

The implementer must assess version impact whenever applying project changes
and update the application version as part of version-affecting work without
waiting for a separate request to bump it. Use the highest applicable impact:

- **Major:** incompatible changes to supported user workflows, persisted data,
  exported formats, or other application compatibility commitments. Increment
  Major and reset Minor and Patch to zero.
- **Minor:** backward-compatible features or newly supported capabilities.
  Increment Minor and reset Patch to zero.
- **Patch:** backward-compatible fixes, security corrections, and changes to
  runtime dependencies, configuration, or packaging that affect the shipped app
  without adding a feature or breaking compatibility. Increment Patch.

Apply the same classification during `0.x.y` development. A version bump does
not authorize the underlying breaking change: obtain any required product or
compatibility decision before implementing it. Once that change is authorized,
the implementer performs its corresponding application version bump, including
a Major bump, automatically. These permissions concern application versions;
specification package versioning remains governed by the meta package.

Documentation-only, specification-only, test-only, or internal maintenance
changes that do not affect the shipped app need no application bump. Record the
classification and reason in the work record, including a no-bump decision.

Use one bump for a coherent change set relative to the previous finalized
application version. Intermediate edits, retries, fixes found during validation,
and repeated builds of that change set do not each receive another bump. If its
scope grows before the release commit and tag are finalized, recalculate using
the highest impact relative to the same previous version. Subsequent changes to
an already tagged application version require a new version; do not reuse or
move its tag.

## Application Release Commits And Tags

Commit each finalized application version and its corresponding implementation
changes in the application's main repository. The version declaration, Android
version code, implementation, and relevant verification evidence must describe
the same change set. Do not include unrelated local work merely to make a release
commit possible.

After relevant checks pass, create an annotated Git tag `v<Major.Minor.Patch>`,
such as `v1.2.3`, on that application release commit. Verify that the tagged
version declaration matches the tag and that the artifact-producing source is
committed. A tag in the specification package's upstream repository cannot
substitute for this application tag. Repositories with multiple independently
versioned applications must document an unambiguous per-application tag prefix.

This package requires automatic local version commits and tags for completed,
validated application change sets. It does not grant permission to switch or
merge branches or push to a remote. Follow the repository's Git authorization
rules for those operations. When publication is authorized, publish the release
commit to the application's primary branch and its corresponding tag together,
atomically where supported. Do not report an unpublished local tag as a remote
release. If validation, integration, or publication is blocked, record the
pending step and keep its status explicit.

Check for an existing tag before creating it. Never move, replace, delete, or
force-push a release tag to accommodate different contents. If the intended tag
already identifies the same verified release commit, treat the operation as
already done. Resolve conflicting tags through a new version.

Creating a commit or tag does not constitute workflow closure confirmation.

## APK Filenames

Every generated application APK, including debug and release outputs, must have
a deterministic filename containing the application identifier or readable
artifact name, exact semantic version, and build variant. For example:

```text
example-1.2.3-debug.apk
example-1.2.3-release.apk
example-1.2.3-demo-release-arm64-v8a.apk
```

Include flavor, split, ABI, or other output qualifiers when needed to prevent
filename collisions. Keep the semantic version itself unchanged; variant
qualifiers belong elsewhere in the filename. Configure the normal build flow
to produce these names automatically, without manual renaming. Keep artifacts
under Gradle build output directories and out of Git unless an explicit artifact
publication policy says otherwise.

## Verification

For version-affecting changes, verify that:

- The selected bump matches the change's highest compatibility impact.
- The committed version uses the required format and the version code increases.
- Built APK metadata matches the authoritative version and version code.
- APK filenames contain the same version and distinguish generated variants and
  splits; exercise the configured naming for debug and release when available.
- The annotated application tag matches the committed version and source.
- After authorized publication, the remote branch contains the release commit
  and the remote tag resolves to it.

Report checks that could not run and why. Specification edits alone do not
require building or releasing an application; record any resulting application
implementation gap separately.
