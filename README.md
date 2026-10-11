# QM handbook for mipt students (v 2.0)
Quantum mechanics has never been an easy subject to learn. When i was a student i used to struggle with finding a good handbook or lectures for solving problems and understanding new approaches. Thus, after several years of teaching students, I decided to create an "easy to read" handbook, which is supposed to help bachelor's students to develop a new mathematical approach and applied it to the new physics. Surely, it should also help them to pass QM exams :)

If you find a mistake, feel free to create merge request with necessary corrections.

## Read it

- **Current edition** — [part 1](https://mvanza.github.io/QM-handbook-for-mipt/QM1.pdf) and [part 2](https://mvanza.github.io/QM-handbook-for-mipt/QM2.pdf), rebuilt whenever an edition is tagged.
- **[Released editions](https://github.com/MVanza/QM-handbook-for-mipt/releases)** — the latest one is always at [`releases/latest/download/QM1.pdf`](https://github.com/MVanza/QM-handbook-for-mipt/releases/latest/download/QM1.pdf) and [`.../QM2.pdf`](https://github.com/MVanza/QM-handbook-for-mipt/releases/latest/download/QM2.pdf).

The PDF is no longer committed to this repository — it is built by CI from the
sources in `QM1-latex/`. Pull requests get a build too: open the `build` check
and download the `QM1-pdf` artifact to preview the change.

## Formatting

The `.tex` sources follow one style, so that diffs stay small and readable:

- UTF-8, LF line endings, 2-space indentation, no trailing whitespace —
  [`.editorconfig`](.editorconfig) sets this in most editors (VS Code needs the
  EditorConfig extension), and [`.gitattributes`](.gitattributes) keeps line
  endings LF in git on every platform.
- Prose is wrapped at 80 columns. Display math is only re-indented: break long
  equations by hand, at `=` or `+`.
- `&` columns in `align*`, matrices and tables stay as you wrote them.

The wrapping and indentation are done by
[latexindent](https://github.com/cmhughes/latexindent.pl), which comes with TeX
Live and MiKTeX, using the rules in [`.latexindent.yaml`](.latexindent.yaml). It
only ever changes whitespace, so the PDF stays the same. Run it from the
repository root:

```bash
# Linux, macOS, Git Bash
latexindent -s -m -wd "-l=.latexindent.yaml" "-c=.latexindent-cruft/" QM*-latex/*.tex QM*-latex/*/*.tex
```

```powershell
# Windows PowerShell
latexindent -s -m -wd "-l=.latexindent.yaml" "-c=.latexindent-cruft/" (Get-ChildItem -Recurse -Filter *.tex QM*-latex).FullName
```

- To format only some files, list them instead of the whole set.
- To check without changing anything, replace `-s -m -wd` with `-k -m`: it exits
  with 1 if any file would change.
- Keep the quotes around `-l=…` and `-c=…`: Windows PowerShell splits such
  arguments at the dot otherwise.
- Backups of changed files and the log go to `.latexindent-cruft/`, which git
  ignores.

**Windows with MiKTeX.** latexindent is a Perl program and MiKTeX does not
include Perl: install [Strawberry Perl](https://strawberryperl.com/). Git Bash
puts Git's own Perl first on `PATH`, and that one lacks latexindent's modules —
run latexindent from PowerShell, or add `export PATH="/c/Strawberry/perl/bin:$PATH"`
to `~/.bashrc`.
