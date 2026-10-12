# Manifest format and helper limits

The bundled `scripts/project_obsidian_sync.py` reads a version 1 JSON manifest. The Skill package holds only reusable instructions and code: each user chooses their source folder and destination folder in their own Vault, then keeps their private manifest and preferences with that source workspace. Use the manifest for explicit files in one or more confirmed source roots. The example below illustrates the fields only; replace every example path and label with the user's confirmed choices.

```json
{
  "version": 1,
  "project_name": "Example Workspace",
  "vault_root": "/absolute/path/to/ObsidianVault",
  "target_root": "/absolute/path/to/ObsidianVault/Chosen/Target",
  "roots": {
    "workspace": "/absolute/path/to/source-workspace"
  },
  "index": {
    "title": "Example Workspace Sync Index",
    "target": "Chosen/Index/Sync Index.md"
  },
  "entries": [
    {
      "root": "workspace",
      "source": "outputs/Example_v1.md",
      "target": "Chosen/Project/Reports/Example_v1.md",
      "label": "Example report v1",
      "category": "Reports"
    }
  ]
}
```

## Field and path rules

- `project_name` is the user-approved workspace name shown in the managed index.
- `vault_root` must identify an existing Obsidian Vault containing `.obsidian/`.
- `target_root` must be inside that Vault. The helper places its sync state file there.
- Each `roots` value identifies an existing source directory. Do not let a source root overlap the Vault target root.
- Each `entries` item names one exact file relative to its selected root and one unique destination path relative to `target_root`. `label` and `category` are user-selected index text, not fixed taxonomies.
- `index.target` is a unique file path relative to `target_root`; `index.title` is the user-selected title. Always configure the index explicitly. Omitting it uses the helper's generic built-in path and title.
- Keep absolute machine-specific paths and the manifest out of distributable Skill packages. If collaborators use different machines, each person needs their own local paths and manifest.
- The helper rejects path traversal and unsafe source/destination overlap. It checks file paths and symlink resolution before copying.

## Preflight and sync behavior

Run:

```bash
python3 "<skill-directory>/scripts/project_obsidian_sync.py" check --manifest "<source-workspace>/obsidian_sync_manifest.json"
python3 "<skill-directory>/scripts/project_obsidian_sync.py" sync --manifest "<source-workspace>/obsidian_sync_manifest.json"
python3 "<skill-directory>/scripts/project_obsidian_sync.py" check --manifest "<source-workspace>/obsidian_sync_manifest.json"
```

The first `check` is read-only. `sync` preflights the full allowlist before copying. The final `check` is also read-only and should report no pending, conflicting, or missing files. Exit code `0` means clean or successful; `1` means pending work; `2` means a conflict or missing source; `3` means a configuration, path, permission, or execution error.

The helper stores SHA-256 state in `.obsidian-sync-state.json` under the target root. If the source and destination match, the entry is unchanged. If a destination differs from the last managed copy, the helper stops with a conflict rather than overwriting it. It never deletes files when an entry is removed from the manifest.

The helper always creates and maintains one generated Markdown index. It mirrors only explicit file entries; it does not watch for file changes, recursively sync folders, implement bidirectional synchronization, or automatically deliver files to another environment. Its `init` command creates a particular maintenance-record and to-do layout, so generic profiles should create their custom manifest from the user-approved choices instead of invoking that default initializer.
