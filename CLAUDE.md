# CLAUDE.md

Guidance for Claude Code when working in the **kopi** theme repo itself.

## Known issues

### LibSass deprecation warning

`layouts/_partials/head.html` compiles `css/main.scss` via `toCSS` with no
options, which uses the LibSass transpiler. Hugo v0.153.0 deprecated LibSass
in favor of Dart Sass and now emits a build warning:

```
WARN  deprecated: css.Sass: libsass was deprecated in Hugo v0.153.0 and will
be removed in a future release. Use dartsass instead.
```

Switching to Dart Sass (`toCSS (dict "transpiler" "dartsass")`) requires the
`sass-embedded` npm package to be present wherever the site is built (see
Hugo docs: https://gohugo.io/functions/css/sass/#dart-sass) — i.e. it pulls
in a Node.js/npm dependency for what is otherwise a Node-free static site
build. The site owner wants to avoid adding a Node.js toolchain just for
this, so the warning is being left in place for now.

Revisit once Hugo removes LibSass support (forcing the move) or if a
Node-free way to invoke Dart Sass becomes available in Hugo.
