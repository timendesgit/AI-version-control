# ProfileCard 2.0 Release Notes

Release date: 2026-09-25

Version 2.0 is a major release. It adds automatic Bench-file matching for engineers, reworks the engineer-entry and CV-import workflow, expands opportunity history and email generation, and ships a dedicated Windows installer with upgrade migration.

## Highlights
- UI improvements.
- Added Bench matching: engineers are automatically matched against a company Bench Excel export, with an editable engineer-profile popup for Grade, NCR, and Availability month, plus read-only Site/Manager/Availability-date info and a strong-skills chip list.
- Reworked engineer entry: single-file "Add profile file" action, a redesigned bulk-import dialog with detection-source badges and per-row scan control, and smarter filename/CV-content name detection.
- Added a per-engineer "Generate" checkbox with pre-flight validation, and deck regeneration that now merges freshly generated cards with previously existing ones.
- Renamed the no-JD output folder to Engineer Library, with a dedicated visibility toggle and automatic migration of existing data.
- Added "Generate Email" to draft an Outlook email with a candidate table, attached cards/deck, and the user's signature.
- Added a dedicated Windows installer with upgrade detection, a progress/log UI, and automatic migration of older opportunity summaries.
- Added mandatory-update support and inline release-notes highlights in the update dialog.
- Improved DOCX header extraction, the About dialog, and general UI polish across the Main and Opportunities tabs.

## Bench Matching

- Added a Bench service that reads a Bench report Excel export (`.xlsx`, `.xlsm`, or `.xlsb`) from a configured folder, picking the most recently modified matching file and copying it to a temporary snapshot so the live file is never opened directly (aborting the sync if the source changes mid-copy).
- Parses the `AllStatus` sheet with tolerance for header-name variants, reading SWP, Manager, Consultant, Grade, NCR, Site, Status, Opportunities, Invoice Date, IC Date, skills/certifications, languages, and optional GGID, cost, and Availability-month columns.
- Each engineer row now shows a live Bench-match chip (Grade | NCR | Availability month) with searching/matched/unmatched states, matched in the background as engineers are added.
- Matching is accent- and case-insensitive, tries an exact name match first, then a token-based partial match; a separate lower-confidence pass surfaces "other possible matches" when no strict match is found.
- Added a redesigned "Bench profile" popup: avatar with initials, name and GGID header, an editable Grade badge, editable NCR and Availability-month fields, read-only Site/Manager/Availability-date info, and a "Strong skills" chip list parsed from the Bench proficiency data. Editable fields are highlighted with a brand-colored border so it's clear which values can be overridden; the candidate list supports switching the matched record or removing the selection.
- Manual overrides to NCR, Grade, and Availability month are kept for the current session and are included when a card is generated.
- If the Bench data has changed since an opportunity was last saved, a one-time "Bench information updated" prompt asks the user to review the match.
- Added a "Bench report folder" setting with a folder picker and a "Refresh bench data" action; an initial sync now runs automatically on startup when a folder is configured.
- Generated cards and opportunity summaries now store the matched Bench record and GGID alongside each engineer entry.

## Engineer Entry and CV Import

- Added a single-file "Add profile file" action: pick one PDF/DOCX and the app detects the engineer's name from the filename or CV content and adds the row with the file already attached.
- Reworked the bulk-import dialog with a wider layout, a file-type badge, a "Detected via" badge (Filename / CV content / Manual / Needs review), and a per-row "Scan" checkbox that controls which rows "Auto-detect names" processes.
- Improved filename-based name detection: handles bracketed name prefixes, "Last, First" formatting, camelCase-glued names, and a wider stopword list, flagging ambiguous filenames as "Needs review" instead of guessing.
- Improved CV-content name detection: now also tries the email address and LinkedIn profile slug before falling back to a more careful header-line heuristic, reducing false positives from role titles or skill tags.
- Added an "Edit engineer name" action per row to rename an already-added engineer, with a live abbreviation preview and duplicate-name protection.

## Generation and Decks

- Added a per-engineer "Generate" checkbox so engineers can be included or excluded from a specific run without removing them from the table; rows loaded from a saved opportunity start unchecked.
- Added pre-flight validation before generating: blocks the run with the list of affected names if a checked engineer has no valid profile file, and warns before a deck is generated without some unchecked engineers' cards.
- Deck generation now merges newly generated cards with cards that already exist in the opportunity folder, so rebuilding a deck correctly includes unchanged engineers.
- Added "Clear" and "Restore loaded opportunity" actions on the Main tab.
- Editing the Job Description or Client Name after loading a saved opportunity is now detected as a new opportunity, with all engineers auto-selected for regeneration and an explanatory prompt.

## Opportunity Management

- Renamed the output folder used for CV-only generations (no Job Description) from `NoJobDescription` to `Engineer_Library`, migrating any existing folder automatically.
- Added a "Show Engineer Library" toggle to the Opportunities filter panel; it's hidden by default and, when shown, is marked as a library rather than a client opportunity (loading, email, and deck generation are disabled for it).
- Engineer cards are now matched to their opportunity-summary entry using an explicit stored path, with the previous filename-based matching kept as a fallback for older summaries.
- Added a "Rename engineer card" action that renames both the displayed engineer name and the generated file together, rolling back on failure.
- Opportunity details now show, per engineer, the file name, abbreviation, photo status, and author/generation-time, with clearer "Open card", "Open CV", and "Edit" actions.
- Simplified "Load opportunity" to a single confirmation that loads everything, rather than choosing which pieces to load.

## Outlook Email Generation

- Added "Generate Email" per opportunity: builds an Outlook draft with a candidate table (name, profile, role, grade, rate, availability, and key skills, where that data is available), attaches the latest card for each engineer plus the newest deck, and embeds the user's default Outlook signature when one is configured.

## Installer and Distribution

- Added a standalone Windows installer (`InstallProfileCard.exe`) with a destination-folder picker, fresh-install/upgrade detection, a progress bar, and an activity log written alongside the installer.
- On upgrade, the installer migrates older `_opportunity_summary.json` files, backfilling author, generation time, photo-used, and card-path information where it's missing.
- The distribution ZIP now includes the installer next to the app runtime folder, avoiding self-extracting executables that some endpoint security tools flag.
- Packaging now includes the dependencies needed for Bench-file reading and Outlook email generation.

## Update Checking

- The update dialog now shows the Highlights section from the new version's release notes inline, with a "See release notes" link to the full notes.
- Added support for mandatory updates: when a release is marked mandatory, the "Later" option is removed and the app closes automatically after the download page opens.

## Interface and Other Improvements

- Improved DOCX profile extraction to include header text and header tables, with a raw-XML fallback for locked or hard-to-open Word/OneDrive files.
- The About dialog now shows an embedded author photo, and feedback/support links now point to separate Teams channels.
- Restyled the engineer-entry controls, the Main-tab action tiles, and the report/learn-about labels for clearer visual hierarchy.

## Validation

- Updated modules were checked with Python compilation and manual verification of the Bench-matching, import, and installer-migration flows.
- Formatting was checked with `git diff --check`.
