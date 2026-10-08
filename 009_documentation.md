# Documentation

Android app documentation should help a developer build, run, test, and reason
about the application safely.

## README

The repository README should include:

- what the app does;
- current project status;
- supported development toolchain once scaffolded;
- setup steps;
- common build, test, lint, and packaging commands;
- `implementation/release.yaml` as the application version/date/counter source,
  its exact specification baseline, the Process-owned automatic bump policy,
  the separate commit/release-tag procedure, and versioned APK location or naming
  pattern; document any pending adoption accurately until the build consumes it;
- important privacy, security, network, storage, or permission constraints;
- license status.

The README should link to authoritative specifications rather than duplicating
large specification sections.

## Implementation Documentation

Implementation documentation should describe the current app structure, known
gaps, verification commands, meaningful architecture decisions, and any current
deviations from the specifications.

When implementation chooses a materially significant Android dependency,
architecture, persisted format, signing approach, or distribution behavior,
record the decision in an implementation decision record.

## Generated Documentation

Generated documentation and reports should not be committed unless a
project-specific workflow requires them.
