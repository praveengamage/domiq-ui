# DOMIQ — physical page split

The original single-file prototype has been cut into one standalone `.html`
file per screen. **Open any file directly in a browser** (double-click / `file://`)
and it renders completely on its own. No server, no build step, no fetch, no
partials, no templating, no JS-generated markup.

## Files

```
login.html                     register.html              forgot-password.html
dashboard.html                 new-project.html           project-workspace.html
project-history.html           profile.html
admin-dashboard.html           quotation-review.html      quotation-review-detail.html
users.html                     catalogue.html             analytics.html

css/style.css                  ← all styles (shared)
js/app.js                      ← all behaviour + seed data + logo (shared)
```

Each HTML file contains its own complete markup: the icon `<svg>` sprite, the
sidebar, the topbar, and that screen's content are written into the file
directly. The sidebar/topbar are duplicated across files on purpose — that's
what a physical split means.

## How navigation works

Links still call `go('screen-id')`. In this build `go()` is a 2-line helper in
`app.js` that just points the browser at the matching file
(e.g. `go('u-create')` → `new-project.html`). It is **not** a router — you can
replace any `onclick="go('x')"` with a plain `<a href="x.html">` and delete the
helper if you prefer.

## Shared JS

`app.js` keeps every interaction handler and render function from the original.
On load it fills in only the widgets that exist on the current page (each render
guards on element presence), so the one shared file works for all 14 pages.

## Screen ↔ file map

| Screen id          | File                          |
|--------------------|-------------------------------|
| auth-login         | login.html                    |
| auth-register      | register.html                 |
| auth-forgot        | forgot-password.html          |
| u-dashboard        | dashboard.html                |
| u-create           | new-project.html              |
| u-workspace        | project-workspace.html        |
| u-history          | project-history.html          |
| u-profile          | profile.html                  |
| a-dashboard        | admin-dashboard.html          |
| a-review           | quotation-review.html         |
| a-review-detail    | quotation-review-detail.html  |
| a-users            | users.html                    |
| a-catalogue        | catalogue.html                |
| a-analytics        | analytics.html                |
