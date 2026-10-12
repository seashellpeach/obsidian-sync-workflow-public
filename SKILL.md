---
name: obsidian-sync-workflow
description: Help a user choose their own source folder and a destination folder inside their Obsidian Vault, then configure or run one-way file sync with user-confirmed contents and timing. Use for first-time setup, preference changes, or requested syncs. For routine syncs, follow an existing project manifest and its configured workflow.
metadata:
  short-description: Set up a personal Obsidian sync workflow
---

# Obsidian Sync Workflow

Help each user define and operate their own Obsidian sync workflow. The Skill contains only the reusable workflow and helper; each person chooses their own source folder, Obsidian Vault, destination folder, sync contents, and timing. Never assume their project is inside the Skill folder or reuse another person's local paths or preferences.

The bundled helper supports an explicit-file, one-way mirror from a local source folder to a folder inside an Obsidian Vault. It is not a background watcher. Standalone delivered files can use the same helper when they are saved in a user-approved source folder and explicitly added to its manifest.

## Start with the user's saved choices

At project entry, look for `obsidian_sync_preferences.md` and `obsidian_sync_manifest.json` in the current project or source workspace. Read applicable project instructions first. If a valid preference file and manifest already exist, honor them; do not ask the user to reconfirm unchanged choices. Run the manifest's read-only `check` before performing configured synchronization.

If settings are missing, incomplete, invalid, or the user asks to change them, read:

- [Setup questions and preference rules](references/setup-and-policies.md)
- [Manifest format and helper limits](references/manifest-format.md)

On a first setup, help the user identify both sides in everyday language: “which project folder should I read from?” and “where inside Obsidian should its copies appear?” The source folder can live anywhere on the user's computer; it is not part of this Skill. First check the current task's workspace and paths the user has already supplied. If the current workspace is a plausible source, show its name and path and ask whether to use it, unless the user has already said so. If they want another folder, ask them to select or identify that folder. Use an available folder picker when the current environment provides one; otherwise give the shortest operating-system-specific way to copy the folder path. Do not search the whole home directory, removable drives, or unrelated folders to guess.

For the Obsidian side, make a bounded, read-only discovery attempt before asking for a Vault path. Check the selected source workspace and its ancestors for a Vault root (a directory containing `.obsidian/`). If the local Obsidian application exposes a registered/open Vault list through accessible settings or an application interface, read only those registered Vault paths and verify each candidate. Do not scan Vault note contents. Show verified candidate names/paths and how each was found, then ask the user to choose or confirm the Vault. A candidate—even a single candidate—is not permission to write there. If none can be verified, explain in plain language how to locate or select the intended Vault; ask for a path only when the environment offers no usable picker or discovery source. Never guess.

After the Vault is chosen, ask which folder inside it should hold this project's copies. The user can name it in ordinary terms (for example, “Projects / Biology report”); resolve that to a path and show it in the preview. Do not make them invent a manifest or type exact folder syntax when a simple description is enough. They choose the contents, sync trigger, exclusions, and version policy through plain-language choices; path discovery does not decide those settings.

## Guide first-time users in plain language

Do not begin by asking a beginner to define a file allowlist, manifest, or folder taxonomy. After the user confirms the source folder, inspect it read-only: list likely project records and output folders, and read only the small number of project overview, progress, or to-do files needed to understand what the work contains. Use that evidence to suggest exact candidate files; never add them to the allowlist without confirmation. Do not recursively read the whole project, hidden/system/dependency/cache folders, credentials, or unrelated private files.

Explain choices in everyday language and offer a few relevant examples instead of a blank questionnaire. For example, ask whether they want Obsidian to contain (a) finished results, (b) progress notes plus finished results, or (c) only files they request each time. Proactively recommend syncing each approved project result when it is completed and ready to hand off. Offer project milestones or only-when-requested as alternatives. Explain that routine questions, unfinished drafts, and full conversation transcripts are excluded unless the user specifically chooses them. They can answer “not sure—recommend something” or describe their goal naturally. Explain that the original project files can remain the working copy while Obsidian keeps a reading copy, and show simple destination-folder examples such as `Projects/<project>/Deliverables/` or `<project>/<topic>/`. Tailor examples to the current project; do not treat examples as selected settings.

If the user is unsure, propose a short starter plan based on the confirmed source folder, read-only file inventory, and verified Vault candidates. State the exact source folder, chosen Vault and destination folder, files it would include, what it would leave out, when it would sync, how versions would work, and that the sync is one-way. Ask only for the next missing choice or invite a plain-language correction. “Use your recommendation” confirms the proposed plan only after the full preview is visible. Do not create settings, a manifest, an index, or copy files until the user confirms that preview.

Never include a user's settings or absolute paths in this shareable Skill package. Store each confirmed profile and manifest with that user's source workspace, not inside the Skill package or the Obsidian destination.

## Apply the configured trigger

Before archiving a result or syncing project files, compare the current work with the saved trigger and inclusion rules. A direct user request to sync applies to the current requested material. Otherwise, sync only when the configured condition is met. Do not add files to the allowlist just because they appear relevant.

Once a project trigger is confirmed, reuse it at each matching work handoff without asking again. The helper runs when the agent reaches that configured work boundary; a conversation simply closing is not a trigger. It cannot watch every save or run continuously in the background. If a user asks for a trigger the current environment cannot provide, explain the limit and ask which supported work-boundary trigger they want.

## Check access to both folders

Before setup or sync, verify that the current task can actually read the selected source and write to the selected Vault. Installing the Skill or entering a folder name does not by itself grant file access. If either folder is unavailable, explain what this session can and cannot reach, then guide the user to open or select an accessible folder. Do not treat a typed path as proof of access, and do not report a sync that did not happen.

## Configure and run project-file sync

Use `scripts/project_obsidian_sync.py` with Python 3.9 or newer. The helper uses only the Python standard library; no extra Python packages are required. At setup, check whether the current execution environment has a compatible Python runtime. If it does not, tell the user what is missing and leave sync unconfigured until they choose how to proceed; do not install software or claim that a copy succeeded. Create a custom manifest from the user's confirmed choices; do not use the helper's `init` defaults unless the user selected exactly those files and folders. Keep the manifest and preference file in the source workspace, not in the Obsidian destination.

Before the first write to Obsidian:

1. Confirm the selected Vault contains `.obsidian/`, the exact target is inside that Vault, and each source file is within a confirmed source root.
2. Show the user the allowlisted source-to-target entries and generated index path/title. The helper always maintains an index page; if the user does not want one, do not use this helper for that workflow.
3. Run `check` first. A new target may be reported as pending. If the only findings are the expected pending entries and the user has confirmed the initial sync plan, run `sync`, then run `check` again. Stop for any conflict, missing source, path error, or permission error.

For a later configured sync, run both commands:

```bash
python3 "<skill-directory>/scripts/project_obsidian_sync.py" sync --manifest "<source-workspace>/obsidian_sync_manifest.json"
python3 "<skill-directory>/scripts/project_obsidian_sync.py" check --manifest "<source-workspace>/obsidian_sync_manifest.json"
```

Use `python` or `py -3` if that is the available Python command. Read the command result and exit status; command completion alone does not prove a clean sync.

## Preserve boundaries

- Treat the confirmed source folder as canonical and Obsidian as a one-way reading copy. The helper does not support bidirectional sync.
- Sync only files explicitly listed in the manifest. It does not recursively mirror folders, delete destinations, or remove old versions.
- Stop on a missing source, path or permission error, or conflict. Never resolve a conflict by choosing the newer file or overwriting a hand-edited Obsidian copy.
- For version history, use distinct source and destination filenames for each version and keep prior entries. For a latest-only mirror, allow replacement only when the helper confirms the destination still matches its last synchronized state.
- Do not add credentials, private keys, databases, or other sensitive files unless the user specifically approves that exact file and the tool supports it.
- Verify that the current task can access both the source and Vault. If it cannot, leave the item pending and explain the access boundary; installing the Skill does not grant access to folders the task cannot reach.
- Do not read private conversation databases or claim a background connection. Synchronize only the files and complete text the user has authorized for this workflow.

## Report the result accurately

State which configured files were copied or unchanged, whether the final `check` was clean, and any missing files, conflicts, permission failures, or pending items. Report cross-device visibility as unverified unless it was actually checked.
