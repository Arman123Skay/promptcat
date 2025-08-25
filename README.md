# PromptCat — Zero-Dependency Prompt Manager in One HTML File

[![Download Release](https://img.shields.io/badge/Release-Download%20Now-brightgreen?logo=github&labelColor=2b2f33)](https://github.com/Arman123Skay/promptcat/releases)

![Header cat image](https://images.unsplash.com/photo-1518791841217-8f162f1e1131?auto=format&fit=crop&w=1400&q=80)

A single-file prompt manager, catalog, and library. Everything stays in your browser. Meow. 😼

Table of contents
- About
- Features
- Why a single file
- Topics and tags
- Download and run
- First run walkthrough
- UI tour
- Prompt model and fields
- Prompt templating and variables
- Search, filter, and tags
- Import and export
- Local storage internals
- Backups and migration
- Examples and curated prompts
- Keyboard shortcuts
- Accessibility and browser support
- Privacy and offline use
- Integration ideas
- Development and file structure
- Contributing
- Tests and QA
- Roadmap
- License and credits
- Where to get releases

About
PromptCat stores your prompts in the browser. It runs as a single HTML file. The app needs no servers. It needs no build tools. It needs no libraries. The UI runs in modern browsers. You can open it from disk or a local web server. The whole app fits in one file with HTML, CSS, and JavaScript embedded. You own your prompts. They never leave your browser unless you export them.

Features
- Single-file app: open and run a single HTML file.
- Zero dependencies: no frameworks, no package install.
- Local-only storage: data lives in your browser localStorage or IndexedDB.
- Rich prompt entries: title, body, tags, model, metadata fields.
- Templates: variables and placeholders for quick reuse.
- Catalog view: browse prompts by category, tag, or popularity.
- Quick search: keyword search across titles and body text.
- Filters: model, tag, date, and custom fields.
- Inline editing: edit prompts fast without a separate screen.
- Import/export: JSON and CSV support for backup and sharing.
- Versioned releases: download the single HTML file from Releases.
- Keyboard shortcuts: speed up common tasks.
- Lightweight CSS theme with dark mode.
- Offline-first: works without network access.
- Small footprint: size stays low to keep load fast.

Why a single file
A single HTML file simplifies deployment. You can store that file in a folder, keep it in a thumb drive, or host it on a static site. You can open it by double-clicking the file in any modern browser. No install step. No dependency chain. The single file also makes audits easy. You can read the full source in a text editor in seconds.

Topics and tags
This repository aligns with these topics:
- 0-dependencies
- css
- html
- javascript
- llm
- offline
- prompt
- prompt-catalog
- prompt-library
- prompt-manager
- prompt-toolkit
- prompting
- prompts

Download and run
Download the release file and open it in your browser. Go to https://github.com/Arman123Skay/promptcat/releases and download the HTML asset. After download, open the file with Chrome, Firefox, Edge, or Safari. The file runs locally and stores data in your browser storage. The release page contains the latest builds and any signed or archived versions.

First run walkthrough
1. Open the downloaded HTML file in your browser.
2. The app shows a welcome card and a prompt list.
3. Click Create to add your first prompt.
4. Give the prompt a short title and a body.
5. Add tags like marketing, code, or roleplay.
6. Save the prompt. The app stores it locally.
7. Search the prompt list by typing in the search box.
8. Export your data to create a backup file.

UI tour
The UI focuses on speed and clarity. The layout has three main areas:
- Left: folder and tag navigation. Use it to narrow prompts.
- Center: prompt list. See title, tags, and short body snippets.
- Right: editor pane. View and edit the selected prompt.
The top bar holds search, import, and export actions. The bottom bar shows storage stats and quick help.

Prompt model and fields
Each prompt entry uses a compact model. The model stores these fields:
- id: a UUID string.
- title: short text.
- body: prompt text with variables.
- tags: array of strings for categorization.
- model: optional string to tag a target LLM.
- private: boolean to mark local-only prompts.
- createdAt: ISO timestamp.
- updatedAt: ISO timestamp.
- usageCount: integer to track runs.
- lastUsedAt: ISO timestamp for last run.
- meta: an object for custom key-value pairs.

You can use all fields to filter, sort, and export.

Prompt templating and variables
PromptCat supports placeholders and simple templating. Use double braces for variables. For example:
- Hello, my name is {{name}}.
You can define default values inside the editor. Use the variable panel to set values at run time. The app replaces variables before you copy the prompt to your clipboard.

Variable rules
- Variable syntax uses double braces without spaces around the name.
- Names accept letters, numbers, hyphen, and underscore.
- The app performs exact replacement of the token.
- You can set runtime values or defaults inside the prompt entry.

Advanced example
Say you store a template:
- Title: Product Launch Email
- Body: "Write a concise email to announce {{product}} launching on {{date}}. Focus on benefits and 2 CTAs."

At run time, set product to "ProdX" and date to "2025-09-01". The app generates the final prompt ready to send to an LLM or to copy.

Search, filter, and tags
Search runs across title and body text. The UI accepts multiple term queries. Use a minus sign to exclude terms. Example:
- query: design -logo
This returns entries with design but not logo.

Filters
- Tag filter: click a tag to show only items with that tag.
- Model filter: limit to prompts for a specific model name.
- Date range: select created or updated range.
- Starred: filter to starred or high-usage prompts.

Tagging best practices
- Keep tag names short and consistent.
- Use plural or singular form consistently.
- Use a prefix for workflow tags, like wf-review or wf-draft.
- Use topical tags for subject matter, like marketing or python.

Import and export
PromptCat supports two main formats: JSON and CSV. The app uses a compact JSON schema for complete backups and a flat CSV for simple lists.

Export
- Full export creates a JSON file with all prompt objects and metadata.
- CSV export produces rows with title, tags, model, and body text.
You can export manually from the UI. The app creates a download file named promptcat-backup-YYYYMMDD.json.

Import
- Import JSON to restore a full backup.
- Import CSV for large lists. The CSV import maps columns to title, tags, model, and body.
- Conflict handling: the app prompts to merge or skip prompts with matching titles.
- Import merges tags and normalizes case.

Local storage internals
PromptCat stores data with a layered approach:
- Primary store: localStorage for fast reads and simple writes.
- Secondary store: IndexedDB for larger datasets and structured queries.
- Backup file: JSON export for safe offline copies.
The app detects storage availability and picks the best store. If localStorage is full, it falls back to IndexedDB. The app stores prompts as objects keyed by id to allow fast update and delete operations.

Why both localStorage and IndexedDB
- localStorage offers simple APIs and fast reads for small data sets.
- IndexedDB handles large data and avoids quota issues on some browsers.
Using both gives speed and scale while keeping code small.

Backups and migration
You should export backups regularly. The app shows a storage usage indicator in the footer. The indicator tells how many prompts you have and a rough size estimate in KB. Use export when you reach a size you want to preserve.

Migration tips
- From other prompt managers: export to CSV or JSON and then import into PromptCat.
- From a text file: transform prompts into CSV with columns: title, tags, body.
- Keep a master backup in cloud storage if you need cross-device sync.

Examples and curated prompts
Below are example prompts and patterns you can add.

1) Code review prompt
Title: JavaScript Code Review
Body: "You are a senior JS engineer. Review the following code for bugs, style, and performance. Provide a short summary and a bullet list of fixes. Code: {{code}}"

Tags: code, review, javascript

2) Email rewrite prompt
Title: Friendly Professional Email
Body: "Rewrite the text below to be friendly, professional, and concise. Keep it one paragraph. Text: {{text}}"

Tags: writing, email, copy

3) Interview prep prompt
Title: Behavioral Interview Prep
Body: "You are an interviewer. Give me 5 behavioral questions for the role of {{role}} and explain what a strong answer looks like for each."

Tags: hr, interview

4) Feature spec prompt
Title: Feature Spec Draft
Body: "Draft a short feature spec for {{feature}} with purpose, goals, success metrics, and a basic user flow."

Tags: product, spec, planning

Curated collections idea
- Onboarding: prompts to onboard new team members.
- Growth: marketing and ad copy prompts.
- Ops: incident postmortem templates.
- Code: snippets and review scaffolds.

Keyboard shortcuts
The app includes a short list of shortcuts for power users. You can view and edit these shortcuts in settings.

Default shortcuts
- N: create a new prompt.
- F: focus search.
- E: edit selected prompt.
- D: delete selected prompt.
- S: star or unstar selected prompt.
- Ctrl/Cmd + K: quick command palette.
- Esc: close modals.

Accessibility and browser support
PromptCat uses semantic HTML and ARIA roles where needed. It aims to work in modern, desktop browsers:
- Chrome latest
- Firefox latest
- Edge latest
- Safari latest
Mobile browsers work but the UI targets desktop layout for efficiency. The CSS uses a responsive grid and switches to single-column on narrow screens.

Privacy and offline use
The app stores data locally. It uses no external analytics, no remote calls, and no third-party trackers. The app works offline after the file loads. You can use the app in an air-gapped environment. If you export or share a backup file, you control where it goes.

Integration ideas
PromptCat focuses on prompt management. It does not ship integrations by default. You can connect it to other tools in multiple ways:
- Copy and paste prompts into your LLM UI or API client.
- Use a browser extension to inject the selected prompt into a web-based LLM input box.
- Write a small local script to read exported JSON and post prompts to an LLM endpoint.

Example extension workflow
1. Select a prompt in PromptCat.
2. Click Copy to Clipboard.
3. Paste the prompt into any web tool or API form.
You can automate these steps with a minimal browser extension or a local helper script.

Development and file structure
The repo stores the core HTML file and optional build artifacts. The single-file app uses small inline modules for maintainability.

Typical repo layout
- promptcat.html — main single-file app (deliverable).
- assets/ — optional images, icons, and license files.
- docs/ — user docs and schema reference.
- tests/ — simple test scripts for data model and import/export.
- CONTRIBUTING.md — contribution guide.
- LICENSE — MIT license.

The single file contains:
- Embedded CSS: lightweight styles and dark mode variables.
- Embedded JS: modular code with minimal helpers for DOM, storage, and templating.
- HTML markup: accessible structure and semantic elements.

Contributing
The project welcomes contributions. Use the issue tracker to report bugs or suggest features. Follow these steps to contribute code:
1. Fork the repository.
2. Make your changes in a branch.
3. Create a PR describing what you changed and why.
4. Include a small test or instructions to reproduce.
Keep changes focused and small. If you add a new feature, include UI tests or screenshots.

Guidelines
- Keep code small and dependency free.
- Prefer simple DOM APIs over heavy helpers.
- Use clear variable names.
- Add comments for complex logic.
- Keep styles modular and theme-friendly.

Tests and QA
Basic QA includes:
- Load the HTML file in a fresh browser profile.
- Create prompts with varied lengths and special characters.
- Export and re-import a backup and validate all fields.
- Test variable replacement with nested or repeated placeholders.
- Test storage behavior with large data sets.

Roadmap
Planned items:
- Tag groups and nested folders.
- Prompt rating and feedback counters.
- Improved import mapping UI for CSV.
- Optional local network sync across devices on same LAN.
- Built-in examples gallery with categories.
- Enhanced search with regex or fuzzy matching.

Where to get releases
Download the release file and open it in your browser. Visit https://github.com/Arman123Skay/promptcat/releases to find the latest single-file builds and archived releases. Download the HTML asset named promptcat.html or similar and open it with your browser to run the app locally.

License and credits
This project uses the MIT license. The single HTML file contains author credits and license text. It also lists small free icons and images used in the UI. If you contribute an asset, include a short license note and attribution.

Credits and inspiration
PromptCat draws from simple offline-first apps and single-file tools. The UI design aims for clarity and speed. The cat emoji and visual theme add a little personality. Meow. 😼

FAQ
How do I back up my prompts?
- Use Export in the top bar. Export creates a JSON file you can store anywhere.

Can I sync across devices?
- The app does not include cloud sync by default. You can export and import backups to move data between devices. Future roadmap includes optional LAN sync.

What if I lose my backups?
- If you lose local browser storage and you did not export, you may not recover data. Export regularly.

How large can my prompt library be?
- The app scales to thousands of short prompts. Very long prompt bodies may hit localStorage limits on some browsers. IndexedDB fallback handles larger datasets.

How do I report a bug?
- Open an issue on the repo. Include steps to reproduce, browser, and a small sample backup if possible.

How do I extend the templating engine?
- The templating uses simple token replacement with double braces. You can extend it by editing the single file and adding functions to the template processor.

Changelog style
The Release page lists changes by version. Each release includes the single HTML file and a small changelog. Use semantic versioning where possible. The Releases page may include zipped archive files for convenience.

Maintenance tips
- Keep a copy of the HTML file for each stable release you rely on.
- Pin to a release if you want reproducible behavior.
- Use the Releases page to compare versions and read changelogs.

Sample data patterns
A few sample prompt objects look like this in JSON form:
- { "id": "uuid-1", "title": "Short title", "body": "Prompt text {{var}}", "tags": ["tag1","tag2"], "model": "gpt-4", "createdAt": "2025-01-01T00:00:00Z" }
- { "id": "uuid-2", "title": "Another prompt", "body": "Explain {{topic}} in simple terms.", "tags": ["explain"], "usageCount": 5 }

Design notes
- Keep the UI minimal. Show only what users need to act.
- Use color to highlight tags and active filters. Avoid heavy gradients.
- Provide clear affordances for create, edit, delete, and export.
- Make copy and paste easy with one-click copy actions.

Security notes
- The app runs in your browser with local data. It does not send data to external servers.
- If you edit the file and add functionality that contacts external services, review the code for network calls.
- Use exports and imports carefully when sharing with others.

Performance tips
- Keep prompt bodies concise. Large embedded examples increase memory and storage use.
- Use tags and filters to narrow large libraries to a working set.
- Clear old or duplicate prompts to reduce storage size.

Customization
You can customize the UI by editing the CSS section inside the single HTML file. Variables include:
- --bg-color
- --accent-color
- --text-color
- --radius

Change those variables and refresh the file.

Debug and developer mode
A small developer mode shows more logging. Toggle it from the settings menu. Developer mode shows storage events and error traces in a compact console area.

Where to get help
Open an issue on the repository to ask for help, suggest features, or report bugs. Include browser type and a small reproduction case.

Project philosophy
Keep personal data under the user's control. Ship small and stable. Avoid external dependencies. Make the tool useful for daily prompt work without friction.

Screenshots and images
- Main list view: a clean list with tags and quick actions.
- Editor pane: multi-field editor with live variable preview.
- Export dialog: choose JSON or CSV and download.

You can find release builds and assets on the Releases page at https://github.com/Arman123Skay/promptcat/releases

Contact and links
- GitHub issues: open issues on the repo to report bugs or request features.
- Releases: the Releases page holds the single-file builds you can download and run.
- If you need to share a prompt set, export JSON and attach it to an issue for troubleshooting.

Thank you for trying PromptCat. The app aims to be a small, fast way to manage prompts on your terms. Meow. 😼