# ProfileCard v1.4 Release Notes

Release date: 2026-09-09

Version 1.4 focuses on making ProfileCard more reliable for day-to-day engineer-card generation, safer to upgrade, and clearer to use when managing generated opportunities.

## Highlights

- Improved multi-engineer generation and profile-file workflows.
- Added reliable opportunity loading and JD identity handling.
- Added persistent engineer-card paths to opportunity summaries.
- Added legacy JSON migration and compatibility handling.
- Added engineer-card rename and engineer-name editing from the Opportunity tab.
- Improved DOCX profile extraction, including headers and header tables.
- Improved installer upgrade behavior and completion UX.
- Refined Opportunity-tab actions, metadata, status indicators, and visual hierarchy.

## Generation and Profile Import

- Added support for multiple engineers in the Main-tab generation table.
- Added per-engineer profile-file selection, extraction preview, editing, and generation status.
- Improved automatic engineer-name detection from filenames and profile content.
- Added safer handling for ambiguous filenames so the application prefers review over an incorrect name.
- Added support for manual engineer-name corrections and abbreviation updates.
- Added per-row photo/template selection and preserved photo usage in generated summaries.
- Improved profile extraction for PDF and DOCX inputs using Markdown and plain-text fallbacks.
- Added DOCX header and header-table extraction, including a raw XML fallback for difficult Word/OneDrive files.
- Added extraction debug artifacts and profile-file hash information to improve troubleshooting.

## Opportunity Management

- Added opportunity identity tracking using a hash of client name and job-description text.
- Improved behavior when the current JD or client changes, treating the changed content as a new opportunity.
- Added confirmation before loading an opportunity.
- Added a separate replacement warning when Main-tab data already exists.
- Loaded engineer rows now default to unchecked for generation.
- Opportunity details now show engineer summaries, skills, author, generation time, card filename, abbreviation, and photo status.
- Added compact actions for opening generated cards, opening CV backups, and editing engineer information.
- Added compact opportunity actions for opening folders, loading opportunities, generating email, and opening decks.
- Added Outlook email generation with generated cards and the latest deck attached when available.

## Engineer Card Files

- New opportunity summaries store `card_path` as a relative path inside the opportunity folder.
- Runtime card lookup prefers `card_path` and retains filename/abbreviation fallback for legacy summaries.
- Added an Opportunity-tab edit action for changing both:
  - The engineer name stored in the summary JSON.
  - The actual generated `.pptx` filename.
- Rename operations update the JSON path and roll back the physical rename if the summary cannot be updated.
- The `.pptx` extension is preserved automatically and duplicate or invalid filenames are rejected.
- File labels now clearly distinguish engineer context from the real filename.

## JSON Compatibility and Migration

- Preserved support for legacy list-only opportunity summaries.
- Added support for older object summaries using `entries`, `engineers`, `items`, or `data` containers.
- Missing global author and creation-date metadata no longer breaks the installer or UI.
- Installer migration backfills missing per-engineer author and generation timestamps when global values exist.
- Missing `photo_used` values are normalized from global or per-entry values.
- Old summaries without photo information default to `photo_used: false`.
- Existing `card_path` values are preserved during migration.
- Installer migration only assigns a card path when the physical file match is unambiguous; ambiguous matches are logged and left for runtime fallback.

## Installer and Distribution

- Improved upgrade detection using the existing `ProfileCard.exe` installation.
- Upgrade migration now repairs older opportunity summaries without requiring modern metadata.
- Installer completion now enables a green Close action after a successful installation or upgrade.
- Rebuild flow packages the runtime and assets into `build/ProfileCard.zip`.
- PyInstaller packaging includes the Flet desktop runtime and required media plugins.
- Embedded executable version metadata is set to `v1.3`.

## Interface Improvements

- Refined the Opportunity tab with clearer file, summary, author, and status information.
- Added subtle photo/no-photo indicators with tooltip descriptions.
- Improved action-button sizing, alignment, labels, icons, and color hierarchy.
- Made report and learn-about labels regular weight.
- Changed the report icon to a clearer red color.
- Added first-run onboarding guidance when required setup is missing.
- Grouped settings into Engine, Appearance, and System sections.
- Added theme support for dark blue, dark gray, light gray, and light blue modes.

## Validation

- Updated modules were checked with Python compilation and VS Code diagnostics.
- Migration probes cover metadata-free summaries, list-only summaries, global photo flags, missing card paths, and ambiguous card matches.
- Formatting checks were run with `git diff --check`.
- Build verification documentation and executable packaging checks remain available in `BUILD_VERIFICATION_GUIDE.md`.
