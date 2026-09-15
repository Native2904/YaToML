# Changelog

## 1.0.0 — 2026-09-15

First public release.

### Features
- Grid view (tree + table) for YAML and TOML files
- Inline editing of scalar values (String, Integer, Float, Bool, DateTime)
- Save (Ctrl+S), patch-based: only changed values are rewritten, comments
  and formatting elsewhere are preserved
  - TOML: fully supported for all scalar types
  - YAML: supported for single-line plain/quoted values; multi-line block
    scalars and flow-style values are safely detected and rejected with a
    warning instead of being saved incorrectly
  - Mandatory verification after every save; aborts (writes nothing) if
    the result doesn't match what was expected
- Context menu (tree: expand/collapse all; table: edit/copy value/copy
  key, jump to tree node; both: Save)
- Status bar with breadcrumb path and unsaved-changes indicator
- Dark mode via `yatoml.ini` (independent of Total Commander's own theme),
  with configurable colors
- Four-language interface: German, English, Russian, Ukrainian, via
  `language_<code>.ini`, selected in `yatoml.ini`
- Escape closes the Lister window (cancels an in-progress edit first, if
  any)

### Known limitations
- YAML: multi-line block scalars (`|`, `>`) and flow-style values
  (`{...}`/`[...]`) can be viewed but not yet saved
- No plain-text tab yet (planned)
- YAML anchors/aliases are resolved transparently on load; the alias
  relationship itself is not shown or editable
