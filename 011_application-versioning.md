# Application Versioning

## Scope And Ownership

Process 5 owns repository-wide specification and implementation baselines,
development identities, change records, integration preparation, release
preparation, and the separation between finalization and publication. Finalized
baselines use `specs-MAJOR.MINOR.PATCH` and `imp-MAJOR.MINOR.PATCH`. Meta owns
reusable specification package versions and their independent package releases.

This document specializes application version metadata for Android. An Android
application has its own identity, `versionName`, and `versionCode`; these are not
additional Macrostates baselines. Several applications may share a repository's
baselines while retaining separate application versions and release histories.

An application may define or override its versioning, release cadence, review,
tagging, and publication strategy in project-specific specifications according to
composition authority. The selected repository policy still governs shared
branch integration. No external changeset product, hosting platform, automatic
store upload, or publication after every merge is required by this package.

## Default And Independent Application Versions

Without an explicit application versioning policy, the stable `versionName` is
the numeric part of the finalized implementation baseline selected for the app:
`imp-6.4.8` gives `6.4.8`. It has no `imp-` prefix or development suffix.

A project-specific policy may choose an independent `versionName`, such as
`7.3.25`, while recording the exact `imp-*` and `specs-*` baselines that produced
that release. It need not share their Major.Minor. Define the policy's version
scheme, authoritative declaration, assignment mechanism, required checks, and
release authorization when choosing this override.

A new repository baseline does not automatically release an Android app or
advance its Android counter. An unchanged published app retains its original
version, counter, and baseline provenance. A later app release using the default
policy adopts the numeric version of its selected finalized implementation.

## Committed Metadata And Provenance

Maintain one authoritative tracked source for each app's release metadata. The
Process deliverables document is the conventional source:
`.macrostates/implementation/deliverables.yaml`. For example:

```yaml
schema_version: 1
deliverables:
  android-app:
    strategy: implementation
    specification: specs-6.4.2
    implementation: imp-6.4.8
    release_date: "2026-09-21"
    source:
      tag: android-app/v6.4.8
    android:
      version_code: 68
```

For an independent application version, its entry additionally declares
`strategy: independent`, `version: "7.3.25"`, and the project's `version_scheme`.
These are hypothetical identities and values, not a required starting version.
Process defines the document schema and release records. A project may choose
another authoritative source through an explicit policy, provided the build and
release records preserve the same identities without competing editable values.

For every finalized app release, record its application identity, exact
application version, version code, application release date, selected
specification and implementation baselines, and source commit. The two
Macrostates references must describe the same implemented contract; the
application's own version does not need matching Major.Minor. Do not compare an
unchanged app's historical provenance against newer repository baselines as if
it were a new app release.

The Process-owned `.macrostates/implementation/release.yaml` identifies the
repository implementation baseline. It is not, by itself, the version/date/code
declaration for every application in a monorepo. An application release date may
differ from the date its implementation baseline was finalized.

## Android Version Code

`android.version_code` must be a tracked integer from 1 through 2,100,000,000.
Allocate a higher code when preparing a new app release that must supersede the
previous release for the same application ID and distribution lineage. Reusing a
version name does not permit reusing a code for changed published artifacts.
Rebuilding the same finalized release or finalizing an unrelated repository
baseline must not increment the counter.

When outputs share an application ID and need distinct installation ordering,
document a deterministic variant scheme based on this counter. It must remain
in range and preserve update ordering across the supported output and release
channels. Independently released application IDs maintain independent counters.

## Build Integration

Gradle must read and validate the app's authoritative metadata, deriving:

- `versionName` from the declared independent version or selected implementation
  baseline under the default policy.
- `versionCode` from the tracked Android counter or documented variant mapping.
- The app's exposed release date from its application release declaration.
- Artifact filename versions from the same application version source.

Reject missing, malformed, contradictory, or ambiguous metadata with a useful
build error. Validate baseline syntax, the applicable contract relation, the real
calendar date, the declared application version policy, and the integer/range.
Do not keep competing hand-edited versions, dates, or counters in Gradle,
properties, resources, or CI. Generate build metadata when runtime features need
the version or date.

A clean release checkout or source archive must provide the app metadata needed
for its build without Git, network access, machine-local settings, or manually
supplied version parameters. Ordinary builds must not update declarations,
dates, counters, commits, or tags.

Development source must be distinguishable from a finalized application release.
Process development identities such as
`imp-6.4.8-branch.feature-x.gabc123` identify repository work; they are not stable
application release versions. A project may expose an appropriate development
`versionName` or generated development marker under its application policy, but
must preserve the selected baseline and work identity and must not claim that
changed development source is the unchanged stable release. Source archives
without Git use captured build metadata or report unavailable source identity
honestly; they must not invent a commit or silently infer finalization.

## Preparation, Integration, And Release

Feature branches record specification and implementation impacts through Process
change records. They do not allocate official Macrostates versions or
automatically increment Android counters for each coherent edit. Incorporating
upstream changes updates the validation target and computed development identity,
while preserving the work's recorded starting baselines.

Follow Process and Repository for development-branch synchronization, integration
preparation, closed-workflow gates, review, and stale-target handling. Release
preparation finalizes repository baselines separately from app release
preparation. App policy decides when and how an Android candidate receives its
version name, counter, date, and release records.

For an authorized Android release, verify that the app declaration, built
metadata, version counter, source snapshot, exact Macrostates baselines, and
verification evidence describe the same candidate. Follow the project's tag and
publication policy; `imp-*` and `specs-*` identify repository baselines rather
than automatically serving as app-release tags. Use unambiguous application
namespaces where several deliverables have their own tags.

Never move or reuse published identities for changed source. Distinguish
prepared, locally tagged, remotely tagged, and distributed states. Verify the
relevant remote identities when publication is authorized. Store or other
distribution upload is a separately authorized operation. A release or
publication does not implicitly close a workflow.

## APK Filenames

Every generated application APK, including debug and release outputs, must have
a deterministic filename containing the application identifier or readable
artifact name, exact application version, and build variant. For example:

```text
example-7.3.25-debug.apk
example-7.3.25-release.apk
example-7.3.25-demo-release-arm64-v8a.apk
```

Include flavor, split, ABI, application ID, or other qualifiers when needed to
prevent collisions. Use the application's version even when it differs from
the repository's implementation version. Keep variant qualifiers and any
filesystem-safe development identity separate from the stable version value.
Configure the normal build flow to produce these names without manual renaming.
Keep artifacts under Gradle build output directories and out of Git unless an
explicit publication policy requires otherwise.

## Verification

For version-affecting application or build changes, verify that:

- The selected default or override follows the effective application policy.
- The declaration and exact baseline provenance are accurate.
- The Android counter preserves installation ordering for this application ID.
- Gradle consumes one authoritative metadata source.
- Built APK version name/code and exposed release date match the app declaration.
- APK filenames use that application version and distinguish variants/splits;
  exercise debug and release naming when available.
- Rebuilds leave declarations, counters, dates, and Git state unchanged.
- Integration preparation and readiness satisfy Process's workflow and evidence
  gates against the current target.

For an authorized app release, additionally verify the application's release
identity, referenced finalized baselines, exact source snapshot, and authorized
publication. Report checks that could not run and why. Specification edits alone
do not require building or releasing an app. Record any pending declaration or
build migration explicitly before claiming readiness under this package.
