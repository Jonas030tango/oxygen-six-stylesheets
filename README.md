# Oxygen Six Stylesheets

A WordPress plugin that adds named CSS stylesheets to Oxygen Builder. You write and manage the stylesheets in the WordPress admin. The builder preview and the frontend load them.

Oxygen has no way to name or edit its stylesheets from the WordPress admin. This plugin adds that.

## Download

The installable ZIP files are in the [`versions`](versions) folder. The [changelog](CHANGELOG.md) lists the changes in each version.

| Version | File |
|---|---|
| 0.3.13 | [oxygen-six-stylesheets-0.3.13.zip](versions/oxygen-six-stylesheets-0.3.13.zip) |
| 0.3.12 | [oxygen-six-stylesheets-0.3.12.zip](versions/oxygen-six-stylesheets-0.3.12.zip) |
| 0.3.11 | [oxygen-six-stylesheets-0.3.11.zip](versions/oxygen-six-stylesheets-0.3.11.zip) |
| 0.3.10 | [oxygen-six-stylesheets-0.3.10.zip](versions/oxygen-six-stylesheets-0.3.10.zip) |
| 0.3.9 | [oxygen-six-stylesheets-0.3.9.zip](versions/oxygen-six-stylesheets-0.3.9.zip) |
| 0.3.8 | [oxygen-six-stylesheets-0.3.8.zip](versions/oxygen-six-stylesheets-0.3.8.zip) |
| 0.3.7 | [oxygen-six-stylesheets-0.3.7.zip](versions/oxygen-six-stylesheets-0.3.7.zip) |
| 0.3.6 | [oxygen-six-stylesheets-0.3.6.zip](versions/oxygen-six-stylesheets-0.3.6.zip) |
| 0.3.5 | [oxygen-six-stylesheets-0.3.5.zip](versions/oxygen-six-stylesheets-0.3.5.zip) |
| 0.3.4 | [oxygen-six-stylesheets-0.3.4.zip](versions/oxygen-six-stylesheets-0.3.4.zip) |
| 0.3.3 | [oxygen-six-stylesheets-0.3.3.zip](versions/oxygen-six-stylesheets-0.3.3.zip) |
| 0.3.2 | [oxygen-six-stylesheets-0.3.2.zip](versions/oxygen-six-stylesheets-0.3.2.zip) |
| 0.3.1 | [oxygen-six-stylesheets-0.3.1.zip](versions/oxygen-six-stylesheets-0.3.1.zip) |

## Requirements

- WordPress 6.0 or later
- PHP 7.4 or later
- Oxygen 6 or Oxygen 4.x (classic). Oxygen is optional; see [Without Oxygen](#without-oxygen).

## Installation

1. Download the ZIP file of the version you want.
2. In WordPress, go to **Plugins → Add New Plugin → Upload Plugin**.
3. Select the ZIP file, then click **Install Now**.
4. Click **Activate**.

The plugin adds the menu **O6 Stylesheets** to the WordPress admin.

## Features

### Stylesheets

- Each stylesheet has a name and a CSS body.
- The CSS editor has syntax highlighting (the WordPress code editor).
- WordPress revisions record each change to the CSS. You can compare and restore old versions.

### Active and inactive

- A published stylesheet is active. The site loads it.
- A draft stylesheet is inactive. The site does not load it.
- The list shows the status, the priority and the CSS size of each stylesheet.
- The bulk actions **Activate** and **Deactivate** change the status of many stylesheets at once.

### Priority

- Each stylesheet has a priority. The default is 10.
- A lower number loads earlier. When two rules conflict, the stylesheet that loads later wins.
- You can change the priority in the stylesheet settings or with **Quick Edit**.

### Categories

- Categories organize the stylesheets. The plugin creates the category "Uncategorized".
- Categories have no effect on the output.

### Import and export

- **O6 Stylesheets → Import / Export** exports all stylesheets to one JSON file.
- The file contains the CSS, the status, the priority and the categories.
- An import skips each stylesheet that has the same name as an existing one.
- The maximum size of an import file is 2 MB.

### Checks

The editor shows a warning when the CSS has:

- unbalanced braces `{ }` or parentheses `( )`
- an empty rule (a selector with no properties)
- a `url()` that points to an external server

## How the CSS loads

| Setup | Method |
|---|---|
| Oxygen 6 | The plugin adds the CSS to the style output of Oxygen. The frontend and the builder preview show it. |
| Oxygen 4.x (classic) | The plugin adds a `<style>` element late in `wp_head`, after the CSS of Oxygen. The frontend and the builder preview show it. The builder interface does not get it. |
| Without Oxygen | The plugin adds a `<style>` element in `wp_head`. |

### Without Oxygen

The plugin also works without Oxygen, as a stylesheet manager for any theme. The admin shows a notice about this.

## Security

- Only administrators can create, edit and delete stylesheets.
- Only administrators can manage categories and use import and export.
- The plugin removes these patterns from the CSS when you save it:
  - HTML tags
  - `@import` rules
  - `expression()`, `behavior:` and `-moz-binding:`
  - `javascript:` URLs

## Uninstall

When you delete the plugin in WordPress, it deletes all its data: the stylesheets, the categories, the settings and the permissions it added.

Export your stylesheets before you delete the plugin.

## License

Copyright (C) 2026 Jonas Karanlik Zadow

This program is free software. You can redistribute it and/or modify it under the terms of the GNU General Public License, version 2 or (at your option) any later version. See [LICENSE](LICENSE).

This program comes WITHOUT ANY WARRANTY.

Oxygen is a product of its own vendor. This plugin is not affiliated with Oxygen or its vendor.
