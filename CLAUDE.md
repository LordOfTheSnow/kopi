# CLAUDE.md

Guidance for Claude Code when working in the **kopi** theme repo itself.

## Sass / Dart Sass

`layouts/_partials/head.html` compiles `css/main.scss` via `toCSS` with no
options. With Hugo `0.170.0`+, LibSass is gone and Hugo uses Dart Sass, which
it finds as the standalone `sass` binary on `PATH` (e.g. the `dart-sass`
package on Arch/CachyOS). No Node.js/npm (`sass-embedded`) is needed.

The SCSS uses the module system (`@use`), not the deprecated `@import`:

- `assets/css/main.scss` pulls in each partial with `@use "partials/<name>"`.
- Partials that need the `md` mixin or `$breakpoint-md` must start with
  `@use "variables" as *;` (members are not shared implicitly as with
  `@import`). Currently: `_base`, `_components`, `_widgets`.

Do not reintroduce `@import`; Dart Sass warns on it and will remove it in 3.0.
