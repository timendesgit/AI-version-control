# ProfileCard 3.0 Release Notes

Release date: 2026-10-07

ProfileCard 3.0 brings together the major improvements planned for 2.0 with the latest updates to Bench data, profile imports, and the Windows application. This release makes it easier to prepare engineer profiles, review Bench information, build complete opportunity decks, and distribute the application.

## Highlights

- Browse synchronized Bench data in a searchable, sortable table and add selected engineers directly to the generation list.
- Combine filters across Bench fields, including SWP, grade, status, site, resource manager, availability date, NCR, engineer name, and GGID.
- Import one profile file or a whole folder, with safer name detection and clearer review controls.
- Generate cards for selected engineers, validate missing profile files before generation, and rebuild decks with existing cards included.
- Manage opportunities more completely, including loading and restoring work, renaming engineer cards, and drafting Outlook emails with cards and decks attached.
- Use the dedicated Windows installer and distribution ZIP for fresh installations and upgrades.
- Improved DOCX profile extraction, including a fallback that keeps exported Word profiles readable in the packaged Windows application.

## Bench Data

- ProfileCard can read a configured Bench report from `.xlsx`, `.xlsm`, or `.xlsb` files. The report is read from a temporary snapshot so the source workbook is not modified.
- Engineer rows are matched with Bench records automatically. Possible alternatives can be reviewed, and Grade, NCR, and Availability month can be adjusted for the current session.
- The new **Bench data** browser presents records in a sortable table with engineer, GGID, SWP, resource manager, grade, NCR, availability date, site, and status.
- Search, multi-select filters, and availability-date presets help narrow the list. Filters can be combined, for example, to show one SWP and several grades at once.
- Select one or more records to add engineers directly to the generation table. Full Bench information, including skills, certifications, and languages, is available in the detail panel.
- Template placeholder rows and values are excluded from the browser.

## Engineer Entry and Profile Import

- Add an engineer manually, select a single PDF/DOCX profile, or import multiple profiles from a folder.
- Single-file and folder imports can detect names from filenames and profile content. Ambiguous names are flagged for review instead of being silently guessed.
- Folder import includes detection-source indicators, per-profile name editing, selective content scanning, and controls for choosing which files to import.
- Engineer names can be corrected in the generation table, with abbreviation preview and duplicate-name protection.
- Extracted profile content can be reviewed and edited before generation. PDF and DOCX extraction use text and Markdown processing with fallbacks for difficult files.

## Generation and Decks

- Select which engineers to include in a generation run without removing other engineers from the table.
- Pre-flight checks block generation when a selected engineer has no valid profile file and warn when a deck may omit engineers without existing cards.
- Deck creation includes both newly generated cards and eligible existing cards, so rebuilding a deck does not require regenerating every engineer.
- Changing the client name or job description after loading an opportunity is recognized as a new opportunity, with an option to restore the previously loaded details.
- Choose whether to use the standard or BigPhoto template for each engineer.

## Opportunities and Email

- The Engineer Library organizes card generations created without a job description, with a separate visibility control in the Opportunities view.
- Opportunity details show engineer summaries, card filenames, abbreviations, photo status, author, and generation time, with clearer actions for opening and editing files.
- Engineer cards can be renamed from the Opportunities view; the displayed name, summary, and generated file are kept in sync.
- Generate an Outlook draft with a candidate summary table and the latest engineer cards and deck attached when available. The user's Outlook signature is included when configured.
- Existing opportunity summaries remain compatible, and the installer can migrate older summary metadata during upgrades.

## Installation and Updates

- The Windows distribution includes a dedicated installer with destination selection, fresh-install and upgrade detection, progress feedback, and upgrade migration.
- The distribution ZIP packages the application runtime, required desktop dependencies, assets, and installer together.
- Update notifications can show release highlights in the app. Releases can also be marked mandatory.

## Interface and Reliability

- Main-tab entry actions and the engineer table have been refined for clearer, more compact workflows.
- Opportunity context can be collapsed to keep the generation workspace focused.
- The Bench browser keeps filtering and engineer details inside the same window, avoiding nested-dialog behavior.
- Improved DOCX header extraction and direct Word XML fallback help preserve profile text, including in the packaged application.
- Settings are grouped into Engine, Appearance, and System sections, with dark and light theme options and first-run setup guidance.

## Validation

- The Bench browser was checked against the included Bench report, including combined SWP/grade filters, row selection, detail display, and importing an engineer.
- Python compilation and the project smoke test pass.