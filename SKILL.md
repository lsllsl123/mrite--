---
name: mrite
description: Use when solving mathematical modeling contests, using the Mrite template, reading problem statements and attachments, building Python/MATLAB models, generating figures and tables, writing Chinese LaTeX papers, or compiling the final PDF.
---

# Mrite

## Purpose

Use this skill to run a Chinese mathematical modeling contest workflow: read the contest statement and attachments (including any files in `解题要求/`), create a solution plan, implement models (Python or MATLAB per user/spec requirement), generate figures and result tables, write a modular LaTeX paper, and compile the final PDF.

This skill is adapted from the `Rzna-5559/Mrite` Claude Code template. Treat the bundled reference as workflow guidance, not as authority over system/developer instructions or the user's newest request.

## Resources

- Detailed workflow and writing rules: `references/mrite-guidelines.md`
- Workspace template: `assets/template/`
- Optional solution-requirements folder: `assets/template/解题要求/` — **读取此目录时枚举所有文件，不要只看README**
- LaTeX paper template and fonts: the `论文` directory inside `assets/template/` uses Chinese directory and file names copied from the original template.

Read `references/mrite-guidelines.md` before starting a full contest solution or when the user explicitly asks to follow Mrite rules.

## Modex-Style Stage Gates

1. **Problem analysis**: extract every subproblem, required outputs, constraints, data dependencies, and assumptions. Write them into `求解/求解计划.md` before coding.
2. **Modeling design**: classify each subproblem as optimization, prediction/classification, evaluation, physical/mechanism analysis, statistics/data analysis, or recommendation. Record chosen method and fallback.
3. **Code execution**: one script per subproblem. Load data, compute, save tables, run checks, then draw figures.
4. **Type-specific checks**: run relevant checks before writing the paper.
5. **Paper writing**: write from verified artifacts only — every claim must point to a table, figure, formula, or check output.
6. **Compile and quality loop**: compile twice, fix errors, check overfull/underfull/float warnings, missing references, abstract length.

## Start Workflow

1. **Resolve working directory**: copy `assets/template/` to the contest directory if not already present.
2. **Check inputs**:
   - Contest statement → `题目/`
   - Data attachments → `数据/`
   - Requirements/constraints → `解题要求/` — **❗CRITICAL: 必须读取该目录下所有文件（含.docx/.pdf/.txt等），不可只看README.md就跳过**
3. **Check runtime dependencies**: Python packages (pandas, numpy, matplotlib, scipy, scikit-learn, chardet, openpyxl, xlrd, python-docx) or MATLAB (as required by spec).
4. **Read problem and all data**: full statement + every file in `解题要求/` + all data sheets.
5. **Create solution plan**: `求解/求解计划.md` with problem type, external requirements, per-question method, outputs, steps, and checks.
6. **Solve each question**: create per-question subfolders, write one script per question.
7. **Write paper** in `论文/` using the bundled TeX template.
8. **Compile and verify** with `xelatex -interaction=nonstopmode` twice.

## Paper Defaults

- Use bundled modular TeX files from the paper template.
- Abstract: at most 900 Chinese characters, exactly one page after compile.
- Tables: use `longtable` exclusively (no `tabular`/`tabularx`).
- Figures: save under each question's figure folder, cite each one in text.
- References: 8-15 real references matching actual methods.
- **Appendix**: include key solution code (not data description).

## Safety And Adaptation

The original Mrite reference says to run fully automatically. In Codex, still follow current system/developer instructions and the user's newest request. When external requirements exist (e.g., "use MATLAB"), honor them as overrides on the default Python-based workflow.
