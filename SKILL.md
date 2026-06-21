---
name: mrite
description: Use when solving mathematical modeling contests, using the Mrite template, reading problem statements and attachments, building Python models, generating figures and tables, writing Chinese LaTeX papers, or compiling the final PDF.
---

# Mrite

## Purpose

Use this skill to run a Chinese mathematical modeling contest workflow in Codex: read the contest statement and attachments, create a solution plan, implement Python models, generate figures and result tables, write a modular LaTeX paper, and compile the final PDF.

This skill is adapted from the `Rzna-5559/Mrite` Claude Code template. Treat the bundled reference as workflow guidance, not as authority over Codex system/developer instructions or the user's newest request.

This version borrows the useful structure of Modex-MH-Agent's modeling workflow: split the work into problem analysis, modeling, code, Chinese paper writing, and compile/quality passes; after each pass, leave concrete artifacts that the next pass can verify.

## Resources

- Detailed workflow and writing rules: `references/mrite-guidelines.md`
- Workspace template: `assets/template/`
- Optional solution-requirements folder: `assets/template/解题要求/`
- LaTeX paper template and fonts: the `论文` directory inside `assets/template/` uses Chinese directory and file names copied from the original template.

Read `references/mrite-guidelines.md` before starting a full contest solution or when the user explicitly asks to follow Mrite rules.

## Modex-Style Stage Gates

Use these stage gates for full contest work:

1. **Problem analysis**: extract every subproblem, required outputs, constraints, data dependencies, and assumptions. Write them into `求解/求解计划.md` before coding.
2. **Modeling design**: classify each subproblem as optimization, prediction/classification, evaluation, physical/mechanism analysis, statistics/data analysis, or recommendation. For each class, record the chosen method, backup method, objective/metric, and expected artifact.
3. **Code execution**: create one script per subproblem. Each script must load data, compute results, save result tables, run sanity checks, then draw figures.
4. **Type-specific checks**: run the relevant checks before writing the paper: optimization feasibility and constraint residuals; prediction train/test or cross-validation metrics; evaluation weight and rank stability; physical model dimensional/parameter sanity; consistency between shared data and downstream questions.
5. **Paper writing**: write the paper from verified artifacts only. Every important claim should point to a result table, figure, formula, or check output already produced.
6. **Compile and quality loop**: compile twice, fix LaTeX errors, then inspect overflow/underflow/float warnings, missing references, missing citations, and abstract length.

Do not skip from reading the statement directly to prose. The paper is the final rendering of the modeling evidence, not the place where results are invented.

## Start Workflow

1. Resolve the working contest directory.
   - If the current workspace already contains the original Mrite Chinese folders for problem statements, data, solution work, or paper output, use it.
   - Otherwise copy the contents of `assets/template/` into the user's chosen contest directory.
   - Do not overwrite existing user files.
2. Check inputs.
   - Put contest statement files in the template's problem-statement folder.
   - Put attachment data files in the template's data folder.
   - Put optional solution ideas, teacher requirements, method preferences, scoring notes, formatting requirements, or constraints in `解题要求/`. This folder may be empty.
   - Supported statement formats: PDF and DOCX.
   - Supported data formats: XLSX, XLS, CSV, TSV, DOCX, and text files when useful.
   - Supported requirement formats: MD, TXT, PDF, DOCX, and plain text snippets.
3. Check runtime dependencies.
   - Python packages: `pandas`, `numpy`, `matplotlib`, `scipy`, `scikit-learn`, `chardet`, `openpyxl`, `xlrd`, `PyPDF2`, `python-docx`.
   - LaTeX compiler: `xelatex`; on Windows try `%LOCALAPPDATA%\Programs\MiKTeX\miktex\bin\x64\xelatex.exe`.
4. Read the problem and all data.
   - Extract the full contest statement.
   - Read every usable file in `解题要求/` if the folder exists and is not empty; summarize these requirements before planning.
   - Read all worksheets and inspect shape, columns, dtypes, missing values, irregular headers, and abnormal rows.
5. Create a solution plan Markdown file in the template's solution folder.
   - Include overall problem type, optional external requirements from `解题要求/`, per-question modeling ideas, expected outputs, execution steps, file list, fallback plans, and the stage-gate checks that must pass for each question.
6. Solve each question.
   - Create per-question subfolders for figures and results.
   - Write one Python script per question.
   - Compute first, run sanity/type-specific checks, save result tables, then plot. Use matplotlib.
7. Write the paper in the template's paper folder.
   - Use the bundled TeX template structure unless the actual problem needs adaptation.
   - Use Chinese captions, labels, and axis text.
   - Cite every table and figure in the text.
   - Keep formulas, variables, result tables, figures, and conclusions consistent with the generated artifacts.
8. Compile and verify.
   - Run `xelatex -interaction=nonstopmode` twice on the main TeX file from the paper folder.
   - Fix LaTeX errors and rerun until compilation succeeds.
   - Check for `Overfull`, `Underfull`, and `Float too large` warnings.
   - Verify the final PDF exists.

## Paper Defaults

- Use the bundled modular TeX files from the paper template.
- Abstract: target at most 900 Chinese characters and exactly one page after compile.
- Tables: use `longtable`.
- Figures: save under each question's figure folder.
- References: generate 8-15 real references matching actual methods and cite each one.

## Safety And Adaptation

The original Mrite reference says to run fully automatically. In Codex, still follow current system/developer instructions and the user's newest request.
