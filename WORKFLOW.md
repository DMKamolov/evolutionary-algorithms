# My workflow: computational tools ↔ GitHub

The assignment asks for two connected workflows. This page documents how each one works for me, with evidence.

## 1. Claude + VS Code + GitHub

Used for: writing notes, building the playground notebook, and working on my portfolio site.

**Setup**
1. Clone this repository in VS Code: Command Palette → **Git: Clone** → paste the repo URL.
2. Install the **Claude Code** extension: Extensions view (`Cmd+Shift+X` / `Ctrl+Shift+X`) → search "Claude Code" → Install. It needs VS Code 1.98+ and a Claude account ([setup docs](https://code.claude.com/docs/en/vscode-extension)).
3. Open the Claude Code panel from the sidebar and work on files in the repo. Claude proposes edits as diffs that I review before accepting.
4. Commit and push from VS Code's **Source Control** panel.

**How I use it**
<!-- Describe a real session, e.g. "I asked Claude to …, it proposed …, I changed … before committing." -->
_add_

**Evidence**
<!-- A screenshot of VS Code with the Claude Code panel open on this repo, and links to 1–2 commits made this way. -->
_add_

## 2. Gemini + Colab + GitHub

Used for: running and experimenting with notebooks in Colab.

**Setup**
1. **GitHub → Colab:** in Colab, **File → Open notebook → GitHub**, paste this repo's URL, and pick a notebook.
2. **Gemini in Colab:** use the Gemini button in Colab to explain a cell, debug an error, or draft code.
3. **Colab → GitHub:** **File → Save a copy in GitHub**, choose this repo and the notebook's path, and write a commit message.

**How I use it**
<!-- Describe a real session, e.g. "I asked Gemini why my bisection loop never ended; it pointed out …" -->
_add_

**Evidence**
<!-- A screenshot of Gemini in Colab on one of these notebooks, and a link to a commit made with "Save a copy in GitHub". -->
_add_

## Where each tool fits

| Task | Tool | Why |
|---|---|---|
| Running notebooks, quick experiments | Colab + Gemini | Nothing to install; Gemini sits next to the code |
| Multi-file edits, notes, the site | VS Code + Claude Code | Works across the whole repo, shows diffs before changing anything |
| Version history, sharing | GitHub | One place that the portfolio links to |
