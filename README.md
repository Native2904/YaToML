# YaToML

A Total Commander Lister plugin (WLX) for viewing and editing **YAML** and
**TOML** files as a tree + table grid, instead of raw text.

YAML and TOML are everywhere in modern development: Docker Compose,
Kubernetes manifests, GitHub Actions / GitLab CI workflows, Ansible
playbooks, and Helm charts (YAML), as well as `Cargo.toml` for every Rust
project and `pyproject.toml` for modern Python packaging and tools like
`ruff` and `black` (TOML).

## Features

- **Grid view**: tree on the left (structure), table on the right (Key /
  Type / Value) showing the children of the selected node — click a
  Map/List row to jump into it, double-click a value row (or a row in the
  table) to edit it.
- **Inline editing**: double-click or press F2 on a scalar value (String,
  Integer, Float, Bool, DateTime) to edit it in place. Enter commits,
  Escape cancels.
- **Save (Ctrl+S)**: writes changes back to disk using a *patch* approach
  — only the bytes of the values you actually changed are replaced.
  Comments and formatting elsewhere in the file are preserved untouched.
  - **TOML**: fully supported for all scalar types, including dates/times.
  - **YAML**: supported for single-line plain and quoted scalar values
    (the common case). Multi-line block scalars (`|`, `>`) and values
    inside flow collections (`{...}`/`[...]`) are detected and safely
    rejected with a warning rather than guessed at — the file is never
    corrupted, but those specific values won't be saved yet.
  - A mandatory verification step re-parses the result after every save
    and aborts (writing nothing) if anything doesn't match expectations.
- **Context menu** (right-click, or Shift+F10 / Menu key): expand/collapse
  all in the tree, edit/copy value/copy key in the table, jump from a
  table row to its tree node, and Save.
- **Status bar**: shows the breadcrumb path of the selected node, and an
  "unsaved changes" indicator while an edit is pending.
- **Dark mode**: optional, off by default. Enable via `yatoml.ini` (see
  below) — independent of Total Commander's own color scheme.

## Installation

1. Copy `yatoml.wlx64` (64-bit) and/or `yatoml.wlx` (32-bit) to a folder
   of your choice.
2. In Total Commander: Configuration → Options → Plugins → Lister
   plugins → Configure → Add, and point it at the `.wlx64`/`.wlx` file.
   Assign it to extensions `yaml`, `yml`, `toml` (or let Total Commander's
   automatic detection handle it).
3. Optional: place `yatoml.ini` in the same folder as the plugin DLL to
   enable dark mode (see below).

## Dark mode

Not connected to Total Commander's own theme. Create or edit
`yatoml.ini` next to the plugin DLL:

```ini
[Settings]
DarkMode=1
```

`DarkMode=0` (or no file at all) keeps the normal light appearance. The
setting is re-read every time a file is opened — no restart needed, just
close and reopen the Lister window (or open the next file).

## Known limitations

- YAML: multi-line block scalars and flow-style values can be viewed but
  not saved yet (see above) — a clear warning is shown, nothing is
  corrupted.
- No plain-text view yet (planned as a second tab alongside the grid).
- YAML anchors/aliases are resolved transparently on load (shown as their
  final value); the alias relationship itself is not shown or editable.

## License

MIT.
