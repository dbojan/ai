
2026-10-04-22-24-03

rules for ai editing, and ask for editing.


## Working Rules General
- If you are going to do gui testing using Xvfb, ask for permission first, and warn user it might take a lot of tokens, like 50% of 5 hour limit.
- Always read the whole uploaded source file, and spec.md, so you do not reimplement already implemented functions, and mess up existing ones. When files are uploaded, read/verify the full uploaded file before making claims about its contents; do not rely only on truncated previews/snippets. If the full file cannot be read, say so explicitly.
- At the start of substantive work, state briefly whether the current model/effort is sufficient or whether a stronger model is warranted (see Verification and model selection). If you do not know which model is running, ask me after you finish reading this document.
- Don't display unnecessary text, I am trying to conserve tokens
- Before spending noticeable time thinking, checking assumptions, reviewing context, or running code inspection, say briefly what is about to be done. If it continues, give short progress updates rather than staying silent. Don't display fake working text ("Crystalizing", etc.); if unable to, display in short what you are currently doing, e.g. "Thinking", "Reading file filename".

- This project folder is not necessarily a Git worktree; do not assume `git diff/status` works.
- User experience is the top priority. Warn before any change likely to make startup, playback, visual behavior worse, and explain the tradeoff.
- Follow direct implementation orders exactly. Do not reinterpret them, and do not substitute a different approach or broaden/narrow a behavior without asking first. Ask before changing the requested approach.
- Do not modify features I asked for without asking me firsts.
- Do not add features I did not asked for without asking me first.
- Warn before adding dependencies and wait for explicit confirmation.
- When proposing a change, first identify the smallest function or module that can implement it, if it makes sense. Do not expand the scope unless the user asks.
- Before writing new code, identify existing code that already performs a similar task. Prefer extending or reusing it over creating parallel implementations.
- When you believe a refactor is better than the requested implementation, explain it first. Do not perform it unless explicitly approved.
- If the requested change appears to require edits in more than three files, stop and explain why before making any changes.

- Do not run compile/build checks and do not ask the user to compile or test, not even after every change; the user compiles/tests manually and provides logs if needed. Do not repeatedly state "I did not compile" after each change.

- After context compaction/resume, reread this file before making edits or proposing implementation changes. Announce every context compaction/resume clearly, and say whether you have read rules.md and spec.md if they exist. Notify the user when context has changed, such as after compaction/resume, before continuing substantive analysis or edits.

- When recommending edits to a document/source file, state exactly which document/file to read, what text to search for, and what to replace it with. Prefer precise search/replace instructions over vague descriptions.

- Do not revert user or generated changes without explicit instruction.

- Do not guess what is inside files, function names, or variable names, or location of those. Look up in the files. If youndo not have files, ask for files
- Avoid broad rewrites unless logs show a specific cause.
- Write name of the patch first, and short summary of what is to be done in plain english, and which files will be modified.
- Before and during modifying files, clearly identify which files will be modified, and any new files, backup files, or folders that will be created.

- Do not make code changes without explicit confirmation from the user. Do not change code until approved with word 'codenow'. Do not use same timestamp and previous codenow approval, for new edits or fixes, after new messages from user, without explicit written permision, in the form of codenow. Even if it is for small fix like compiler error, or an import statement.
- After changes are done, show a summary what was done.

- Do not update specification file (usually spec.md) unless the user asks.
- On adding changes to recent section of the spec.md, mention which files were edited.

- Treat the patched version of source files as the current state of the project — pulling from what's in outputs, not from what happens to still be sitting in the uploads folder



## File Editing

* Ask user if he wants to manually edit files. If he says yes, when describing manual file edits, always specify:
  * which file to open
  * what text to search for (the complete block of text to search for, or a single line. Do not ask user to select text at speciefied line, and then stop before some othere specified line.)
  * what text to replace it with (complete replacement text)
  * take into account indent in front of text, so search block can be searched for at once, using multiline matching, and user does not have to remove indent to find text block

* If user asks to check newly modified file he uploaded, or asks 'like this?' , just compare it with the previously updated file. Anounce what you are doing. If you are missing previous file, say so.
* When an edit target could occur more than once, provide a complete search block that is unique in the current file. Before approving the user’s edit, re-read the uploaded resulting file and verify that each intended replacement landed in the correct function and that no similar block was changed by mistake.
* When reviewing a manually edited file, report only verified findings from the uploaded current file. Do not assume that an earlier instruction was applied correctly.
  
* Before editing a file, create a backup copy using the format:
  `originalname.ext-YYYY-MM-DD-HH-NN-SS`
* If the required date/time is not known, ask the user for it before generating backup filenames.
* update the timestamp of the file being edited, to the given timestamp YYYY-MM-DD-HH-NN-SS, at the top of the file.
* if there is no timestamp at the top, add it in the format, using appropriate comment for the file format, or programming language:

```
// Project Name - filename.extension
// last modified (utc): 2026-07-20-06-50-00
// instructions: on modify, update string.
```
* First line, first part is project name, then filename.


* After edits are completed, compare the edited file against the backup copy to verify that only the intended changes were made.
* after editing, check new file for bugs and correct logic, but make another backup copy before editing, named: .backup-before-bugs-and-logic-check.timestamp
* after checking for bugs, if there was editing, check if the edits were correct with .backup-before-bugs-and-logic-check.timestamp
* If the comparison is satisfactory, move the backup files to folder:
  `not_needed_after_editing/`
* Do not delete backup files automatically.
* When presenting files, you can just display link to download changed files. You do not have to present backup files.

  ## Verification and model selection

  - After every edit, the implementing model must perform a same-model verification pass:
    * reread the edited regions from the current file;
    * inspect the complete diff against the backup;
    * check references, callers, control flow, error paths, and unchanged behavior;
    * do not run builds, tests, or compile checks unless explicitly requested.
  - A same-model check is sufficient for documentation, comments, formatting, mechanical renames, and small isolated changes with no meaningful behavior, lifecycle, concurrency, persistence, I/O, security, or compatibility impact.
  - For behavior-sensitive changes—such as playback, recording, networking, storage, databases, authentication, concurrency, lifecycle, UI state, migrations, APIs, or multi-file changes—use a separate logic-review pass when practical.
  - The reviewer must inspect the current diff and relevant surrounding code independently, identify regression risks, and not assume the implementation model's reasoning is correct.
  - Use the cheapest available model that is appropriate:
    * use the fast/low-cost model for reading, summaries, documentation, and simple isolated edits;
    * use the balanced coding model for normal implementation and behavior-sensitive reviews;
    * use the strongest model only for broad architecture, difficult concurrency, unclear root causes, security-sensitive work, or high-impact regressions.
  - Do not use a stronger review model automatically for every task. Escalate only when the change could silently regress or when the same-model check cannot establish correctness.
  - If a stronger but more expensive model would materially reduce risk, before substantial work state:
    * the current model and effort;
    * the recommended model and effort;
    * why it would help;
    * that the current model can continue with a higher risk of missed issues.
  - Ask the user whether to continue with the current model or switch before substantial work. Do not ask for an upgrade when the current model is clearly sufficient, and do not silently switch models.
  - If a stronger review finds a possible issue, inspect the current source and diff before changing anything. Do not apply review suggestions blindly.

  - For behavior-sensitive changes, prefer a two-model workflow when the regression risk justifies the extra cost:
    1. Implement with the cheapest suitable model, normally `gpt-5.6-luna` at medium effort.
    2. Perform the required same-model verification first.
    3. If the change has meaningful silent-regression risk, ask the user to switch to `gpt-5.6-terra` at medium effort for a targeted independent review.
    4. The stronger review should inspect only:
       - the current diff;
       - directly affected surrounding code;
       - relevant control flow, error paths, and regression risks.
    5. The reviewer must not redo the entire task analysis unless the diff reveals a broader issue.
  - Suggest stronger model only when the targeted review finds broad architectural, concurrency, lifecycle, or high-impact regression risk.
  - The assistant must not claim that it switched models; the user changes the active model in web or cli interface
  - If the user does not switch models, the implementation model may perform the review, but must state that it is a same-model review.
  - Terra or similar claude model, review is especially appropriate for changes involving playback lifecycle, recording, networking/retries, persistence, concurrency, Media3 behavior, URI/content-provider handling, or changes where a subtle regression would be difficult to detect manually.
  - Luna or similar claude model, same-model verification is normally sufficient for localized changes whose behavior and affected paths are straightforward.

