# Changelog

Each linked version number opens the installable ZIP file of that version. Versions before 0.3.1 have no ZIP file.

## [0.3.14](versions/oxygen-six-stylesheets-0.3.14.zip) – 2026-10-04

### Added

- Visitors get the stylesheets as one cached CSS file instead of inline CSS. The browser keeps the file, so the next pages load less CSS. The setting "Cached file" is in O6 Stylesheets → Settings and is on by default. Users who can edit stylesheets still get the inline CSS with the stylesheet names.
- If the plugin cannot build or use the file, all visitors get the inline CSS as before. Examples are a stylesheet with `@namespace` or a relative URL such as `../a.png`. A stylesheet whose last rule does not end with `}`, for example only `@layer a, b;`, also blocks the file. The server can also fail to write or send the file. The Settings page shows the reason.
- With WPML or Polylang and one domain per language, each domain gets its own file if a URL in the CSS starts with one `/`.
- A page cache that keeps a page longer than 7 days can link a deleted file. The file can also be missing on a site with more than one web server and no shared uploads. A CSS optimizer that combines CSS or loads it later can change how the stylesheets apply. Clear the page cache in the first case. In the other cases, turn off "Cached file".

### Changed

- With a persistent object cache, a change to other content, for example a product, no longer clears the stylesheets from that cache. Shops and other sites with many changes read the stylesheets from the database less often.
- The plugin sorts the stylesheets in PHP instead of in the database. The order stays the same. Without a persistent object cache, the stylesheets load faster when they are large.
- On Oxygen 6, the builder interface no longer reads the stylesheets, so it uses less memory. The builder preview still shows them.

## [0.3.13](versions/oxygen-six-stylesheets-0.3.13.zip) – 2026-09-28

### Changed

- On Oxygen 6, the plugin loads the stylesheets only on frontend requests. REST, admin, cron and login requests now use less memory.
- The plugin adds its admin UI hooks only on admin requests.
- The check for stylesheets with unchecked CSS no longer runs a database query on each admin page. It runs after a plugin update until no such stylesheet is left.
- WordPress keeps at most 10 revisions of a stylesheet. When a save creates a new revision, WordPress deletes the oldest revisions above 10. Your own `WP_POST_REVISIONS` limit or revisions filter stays in effect.

## [0.3.12](versions/oxygen-six-stylesheets-0.3.12.zip) – 2026-09-28

### Fixed

- The warnings about braces and parentheses ignore braces and parentheses in comments, strings and `url()`. A comment without `*/` and a string without its closing quote end as in the browser.
- If the CSS is too large or too complex to check, a warning says so.
- The Security Notice about external URLs also shows for `@import "https://…"`, for a URL with CSS escapes such as `\2f\2f`, and for `url(http:host/x)`. It no longer shows for a URL in a comment or for the SVG namespace `http://www.w3.org/2000/svg` in a data URI.
- When you delete the plugin, it removes all its data. This includes stylesheets in the trash, the stylesheet categories, and the plugin capabilities on every role and user. Capabilities of other plugins stay.
- After an activation with WP-CLI, the first load of the Stylesheets screen no longer shows "Sorry, you are not allowed to edit posts in this post type."

## [0.3.11](versions/oxygen-six-stylesheets-0.3.11.zip) – 2026-09-27

### Security

- The CSS filter also removes keywords that use CSS escapes or comments, for example `@\69mport` or `behavior/**/:`. The markers are `[removed]`, `[removed]:`, `[removed](` and `@o6s-removed-import`. A marker no longer hides the rules after it.
- If the CSS check cannot finish, for example on a very large input, the plugin does not save the CSS. A notice says so, and the previous CSS stays. The import skips such an entry.
- After the update, the plugin checks the CSS of all stylesheets once. A stylesheet whose CSS fails the check is no longer used on the site. The editor shows its CSS and a notice until you correct and save it.
- The import removes HTML tags from stylesheet titles for all users.
- A stylesheet can no longer be private or have a password. Quick Edit and Bulk Edit no longer offer these options, and the update changes existing private stylesheets to drafts.

### Fixed

- The edit screen hides the Visibility row of the Publish box. Before, the rule that hides it had no effect.
- The Security Notice about external URLs also shows for `url(//host)` and for external strings in `image-set()`.
- The CSS filter no longer changes `scroll-behavior`, `overscroll-behavior` or selectors such as `.behavior:hover`.
- The "CSS not saved" notice and the list of stylesheets with unchecked CSS show only to users who can edit these stylesheets.

## [0.3.10](versions/oxygen-six-stylesheets-0.3.10.zip) – 2026-09-27

### Changed

- The frontend loads all published stylesheets with one database query. With a persistent object cache, for example Redis, one cache entry holds the result.
- Query filters and post meta filters of other plugins, for example `pre_get_posts`, `posts_where` or `get_post_metadata`, no longer change the stylesheets on the frontend.
- The import notice counts duplicate titles and invalid entries separately. When nothing is imported, the notice is a warning.
- The import accepts only a `.json` file. The browser rejects an empty file field, another file type and a file larger than 2 MB before the upload.
- A failed import shows a notice with the reason, for example an expired form, a JSON syntax error or a file without the "items" list.

### Fixed

- The Import / Export page no longer has two buttons with the same `id="submit"`.
- The import notice uses the singular form for one stylesheet: "1 stylesheet imported".
- A reload of the import result page no longer sends the file again.
- The notices of the stylesheet screens say "stylesheet" instead of "post".

## [0.3.9](versions/oxygen-six-stylesheets-0.3.9.zip) – 2026-09-27

### Added

- On activation, the plugin checks the character set of the database tables. On `utf8mb3` tables, a warning tells you that stylesheets cannot contain emoji or other 4-byte characters.

## [0.3.8](versions/oxygen-six-stylesheets-0.3.8.zip) – 2026-09-26

### Fixed

- Revisions keep the CSS unchanged for users without the `unfiltered_html` permission, for example site admins on a multisite. Before, WordPress changed `a > b` to `a &gt; b` in the revision, and a restore broke the CSS. Revisions from older versions can still contain `&gt;`: check the CSS after you restore one of them.
- The import finds an existing stylesheet or category only by its exact name. Before, "Färben" counted as a duplicate of "Farben", and "Größe" of "Grösse".
- The import reuses an existing category at any level of the category tree.
- The import keeps a category named `0`.
- The CSS filter replaces a run of `<` before a tag in one step, so a second save gives the same CSS.

## [0.3.7](versions/oxygen-six-stylesheets-0.3.7.zip) – 2026-09-26

### Fixed

- A save keeps the backslashes in the CSS, for example `content: "\201C"` or `.md\:flex`. Older versions deleted them on each save, also in the revisions. CSS saved with an older version does not get its backslashes back: add them again.
- A revision restore keeps the backslashes in the CSS.
- The import keeps the backslashes in the CSS, the stylesheet titles and the category names.
- The import finds an existing stylesheet by its exact title and skips it. Before, a title with a backslash, two spaces, `<` or `%` was imported again.
- The import accepts the title `0`.

## [0.3.6](versions/oxygen-six-stylesheets-0.3.6.zip) – 2026-09-26

### Security

- The page source shows the stylesheet names only to users who can edit stylesheets. Other users see the post ID in the CSS comments.
- Without Oxygen 6, the id of each `<style>` element contains the post ID, not the stylesheet name.

## [0.3.5](versions/oxygen-six-stylesheets-0.3.5.zip) – 2026-09-26

### Fixed

- Stylesheet categories have no public pages. The site has no archive for a category, and the Tag Cloud widget does not show the categories.

## [0.3.4](versions/oxygen-six-stylesheets-0.3.4.zip) – 2026-09-26

### Fixed

- The bulk actions **Activate** and **Deactivate** skip stylesheets that already have the new status, so a draft keeps its date. They also skip stylesheets in the trash.
- The bulk action notice counts only the stylesheets that changed.
- The bulk action notice does not show again when you reload the list.

### Security

- The bulk action **Activate** needs the permission to publish stylesheets.
- The import needs the permission to edit stylesheets. A user who cannot publish stylesheets imports them as drafts.

## [0.3.3](versions/oxygen-six-stylesheets-0.3.3.zip) – 2026-09-26

### Fixed

- The frontend loads the active stylesheets in priority order. Before, they loaded in the order in which you created them.
- A stylesheet without a priority value sorts as 10.
- The export keeps a priority of 0. Before, it wrote 10.

## [0.3.2](versions/oxygen-six-stylesheets-0.3.2.zip) – 2026-09-26

### Changed

- The plugin information shows the correct author name and links.

## [0.3.1](versions/oxygen-six-stylesheets-0.3.1.zip) – 2026-05-22

### Security

- A stylesheet name with `</style>` cannot end the `<style>` element and run a script. The plugin removes `<` and `>` from the name in the CSS comments. Versions 0.2.0 to 0.3.0 have this flaw.
- **Quick Edit** cannot change the CSS.
- The plugin rejects a CSS value that is not text.

## 0.3.0 – 2026-05-22

### Added

- Support for Oxygen 4.x (classic). The plugin finds out which Oxygen version is active.
- On Oxygen 4.x, the plugin loads your CSS after the CSS of Oxygen, so your CSS can override it. The builder preview also shows your CSS. The builder interface does not get it.

### Changed

- The notice about a missing Oxygen shows only when neither Oxygen 6 nor Oxygen 4.x is active.

### Known issues

- In the Oxygen 4.x builder preview, the Oxygen stylesheets override your CSS.

## 0.2.0 – 2026-03-25

### Changed

- The post status replaces the **Active** checkbox. A published stylesheet is active. A draft stylesheet is inactive.
- When you update to 0.2.0, the plugin moves each inactive stylesheet to draft.
- The **Publish** box does not show the **Visibility** option.
- The import still reads the `active` field of older export files.
- The **Active** column is not sortable.
- The plugin creates the category "Uncategorized".

### Fixed

- When you sort the list by priority, the list also shows stylesheets that have no priority value.

### Security

- When you save, the plugin removes `@import` rules from the CSS.
- When you save, the plugin removes all HTML tags from the CSS. It also removes `expression(`, `-moz-binding:`, `behavior:` and `javascript:` when they contain spaces.
- On output, the plugin removes all HTML tags from the CSS.
- When you restore a revision, the plugin cleans the CSS in the same way.
- A stylesheet name with `*/` cannot end the CSS comment.

## 0.1.15 – 2026-03-19

### Fixed

- The plugin writes its permissions to the database only when the version changes. Before, it wrote them on each admin page.
- **Last modified by** shows the last editor. Before, it showed the author.
- The frontend also loads stylesheets that have no priority value.
- The import accepts only the status Published, Draft or Pending.
- The maximum size of an import file is 2 MB.
- The uninstall also deletes the permissions of the plugin.

## 0.1.10 – 2026-03-19

### Added

- The list shows the CSS size and a status dot for each stylesheet.
- **Quick Edit** for the active setting and the priority.
- The bulk actions **Activate** and **Deactivate**.
- The page **Import / Export**. It exports all stylesheets to one JSON file, with the CSS, the status, the priority and the categories. The import skips stylesheets that already exist and creates missing categories.
- The editor shows a warning for unbalanced braces, unbalanced parentheses and empty rules.

## 0.1.5 – 2026-03-19

### Security

- Only administrators can create, edit and delete stylesheets and manage categories.
- When you save, the plugin removes these patterns from the CSS: script tags, `</style`, `expression()`, `-moz-binding`, `behavior:` and `javascript:`.
- On output, the plugin removes `</style` from the CSS.
- The editor shows a warning when a `url()` points to an external server.

### Added

- Revisions for the CSS. You can compare and restore old versions.
- **Last modified by** in the stylesheet settings.

## 0.1.0 – 2026-03-19

### Added

- Named stylesheets with a CSS editor that has syntax highlighting.
- Categories for the stylesheets.
- An active or inactive setting for each stylesheet.
- A priority for each stylesheet. A lower number loads earlier. The default is 10.
- Oxygen 6 shows the CSS on the frontend and in the builder preview.
- Without Oxygen, the plugin adds the CSS to the page head.
- The list has the sortable columns **Active** and **Priority**.
- The uninstall deletes the stylesheets.
