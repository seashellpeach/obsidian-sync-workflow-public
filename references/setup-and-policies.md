# Setup questions and preference rules

Use this reference when a project has no complete, confirmed Obsidian sync profile or when the user asks to change one. Each person chooses their own project/source folder and destination inside their own Obsidian Vault; neither folder has to be inside the Skill. Guide beginners in short, ordinary-language steps. Do not ask them to fill in technical fields or infer their choices from examples.

## Choices to confirm

Do not make a beginner invent technical settings. Ask one or two simple questions at a time, using the current project and available Vault information to reduce what they must figure out.

1. **Which folder has the project files?** If the current task already has a clear project workspace, show its name and path and ask whether to use it; if the user has already said “this project,” that confirms it. If they want another folder, ask them to select or identify it. Use an available folder picker when one exists. Otherwise, give a brief Finder, Explorer, or file-manager instruction to copy the folder path; ask them to paste a path only when selection/discovery is unavailable. Do not scan the whole home directory, removable drives, or unrelated folders. After the source is confirmed, inspect it read-only. Use filenames and a small number of relevant overview, progress, or to-do files to identify likely sync candidates. Do not recursively read its full contents or inspect hidden/system/dependency/cache folders, credentials, or unrelated private files.
2. **Which Obsidian Vault should receive the copies?** Check the confirmed source workspace and its ancestors for a directory containing `.obsidian/`; if accessible, check only registered/open Vault paths exposed by the local Obsidian application. Verify every candidate; do not search the whole home directory or read Vault note contents. Show verified candidate names/paths and how they were found, then ask which one to use. If no candidate is verified, help the user locate or select the Vault in plain language and request a path only if no picker or discovery source is available. A detected Vault is never automatic permission to write there.
3. **Which folder inside that Vault should hold the copies?** Let the user describe it naturally (for example, “Projects / Biology report”). Translate that into a concrete destination path; show it in the complete preview. If they are unsure, suggest a folder based on the project and show a simple example. The helper always creates a generated index page, so include its proposed location and title in the preview; never choose a generic default without showing the user.
4. **What should be copied there?** Based on the confirmed source folder's read-only inventory, suggest exact project progress files, selected outputs, or complete delivered text saved as Markdown. Offer everyday-language choices such as finished results only, progress notes plus results, or only items the user asks to copy each time. Explain likely exclusions in plain language (for example, drafts, temporary files, or discussion notes). The bundled helper mirrors explicitly selected files; it does not recursively copy every file in a folder.
5. **When should it sync?** Proactively recommend syncing each approved result for this project when it is complete and ready to hand off. Offer project milestones or only-when-requested as alternatives. Explain that routine questions, unfinished drafts, and full conversation transcripts are excluded unless the user specifically chooses them. Ask what to leave out, such as intermediate files or particular task types. Once confirmed, save the trigger and reuse it at matching work handoffs without asking again; a conversation merely closing is not a trigger.
6. **Which copy is the original, and how should versions work?** Explain that the bundled helper copies one way from the source folder to Obsidian; it cannot keep both sides in sync. Ask whether to keep older versions or maintain one latest copy. A latest-only entry can update its managed destination only if that destination still matches the helper's prior state. Retained versions need distinct filenames and entries; old files are not deleted. If the user wants bidirectional sync, do not configure this helper.
7. **Can this session reach both folders?** Verify that the current execution environment can read the selected source and write to the chosen Vault. Installing the Skill does not grant access to folders the task cannot reach.

Folder discovery is read-only and only identifies candidates. A matching `.obsidian/` directory or a path in Obsidian's registry is not approval to write there. Do not infer the user's file list, destination folder, or sync trigger from discovery results.

When the user is unsure, prepare a short recommended starter profile from the confirmed source folder, discovered files, verified Vault, and their stated goal. Show the source and destination folders, exact files to include, exclusions, sync timing, one-way direction, and version behavior. A recommendation is not active configuration: wait for the user to confirm the complete preview. They may approve it in plain language (“use that plan”) or correct any part without learning the technical field names.

Explain the remaining choices simply:

- **One-way copy:** the project file stays the original; Obsidian receives a reading copy.
- **Keep versions:** older delivered copies stay available, using distinct names.
- **Latest copy only:** one Obsidian destination is updated, but only if nobody edited it outside the helper.
- **Sync timing:** at a completed result, at a project milestone, or only when the user asks.

These are explanations and examples, not automatic selections. The bundled helper still requires the user to approve exact files and the complete source-to-destination preview. The source workspace and Obsidian folder stay wherever the user chose; neither is moved into the Skill.

## Save the confirmed profile

After the user approves the preview, record the choices in a human-readable `obsidian_sync_preferences.md` beside the manifest. Include:

- the confirmed trigger and inclusion/exclusion rules;
- the chosen source-of-truth direction;
- the selected hierarchy and filename/version policy;
- the Vault and target paths, with a note that they are local-machine settings;
- any environment limitations or manual steps the user chose.

Create or edit `obsidian_sync_manifest.json` from the approved source list and folder mapping, following [the manifest format](manifest-format.md). Never overwrite an existing manifest during first-time setup. If one already exists, inspect it and resolve any proposed changes with the user before editing.

Do not add the preference file, manifest, sync state, or generated temporary files to the sync allowlist unless the user explicitly asks for them. Do not copy these machine-specific settings into the shareable Skill package.

## Per-delivery behavior

- Follow the saved trigger and content scope. A later opt-out for the current task takes precedence over the standing trigger.
- Save complete authorized text or the original selected file in the agreed source workspace before syncing. Do not replace complete content with a summary.
- Add a newly delivered file to the manifest only when the saved scope authorizes that type of output. Preserve earlier entries for versioned history.
- If the destination name already exists and is not a previously managed identical or unchanged destination, stop and show the conflict. Do not rename, move, or overwrite either copy without the user's decision.
- If the task cannot access the Vault, mark the item pending. Do not substitute an unapproved upload or claim that an export has synchronized.
