---
name: mrite
description: Solve mathematical modeling contests with the Mrite template: read problems and data including 解题要求/, build Python or MATLAB models per user requirement, generate charts and tables, write LaTeX paper, compile PDF.
metadata:
  allowBash: true
---

# Mrite 数学建模自动求解模板

## 全自动模式

本模板设计为全自动无人值守运行。遇到决策点自行判断并继续，不做 `ask` 类操作。

**但需特别注意以下关键步骤不可跳过：**

## 项目结构

```
竞赛模板/
├── SKILL.md / CLAUDE.md
├── 题目/                  ← 赛题文件
├── 数据/                  ← 附件数据
├── 解题要求/              ← 额外要求（必须枚举全部文件，不只看README）
├── 求解/                  ← AI自动生成
│   ├── 求解计划.md
│   ├── 预处理数据.csv
│   ├── 问题一/
│   │   ├── 问题一_<描述>.py/.m
│   │   ├── 图片/
│   │   └── 结果/
│   ├── 问题二/ ...
│   └── 问题N/
└── 论文/                  ← AI自动生成
    ├── 论文.tex
    ├── format.cls
    ├── fonts/
    └── 0~10章 .tex
```

**文件命名**：代码、图、CSV、tex文件一律中文。图存 `求解/问题X/图片/`，论文通过 `../../求解/问题X/图片/xxx.png` 引用。论文目录只放tex+cls+fonts。

---

## 一、执行流程

### 重要修复：解题要求目录读取规则
**每次解题必须枚举 `解题要求/` 目录下所有文件并逐个读取，不可只读README.md就跳过。README仅说明目录用途，不代表没有其他要求文件。**

### Step 0：读取输入
1. 读 `题目/`（PDF用PyPDF2，DOCX用python-docx）
2. **读 `解题要求/` — 枚举目录下所有文件，逐个读取内容。若为docx则全文解析。写入求解计划.md的"外部要求"部分**
3. 读 `数据/` 下所有数据文件，全量读取
4. 自动识别问题数量N

### Step 1：求解计划
写 `求解/求解计划.md`

### Step 2：逐题求解
每题一个 `.py` 或 `.m` 文件（根据解题要求选择语言），放在 `求解/问题<序号>/`。先算后画。

### Step 3：论文写作
按模板写tex。附录放解题代码（非附件说明）。

### Step 4：编译
```bash
cd 论文
xelatex -interaction=nonstopmode 论文.tex
xelatex -interaction=nonstopmode 论文.tex
grep -c 'Error' 论文.log  # 必须为0
```

### Step 5（自动）：排版优化
Overfull/Underfull → 修复 → 重编译 → 直到干净。

---

## 二、论文规范

### 通用规则
- 正文一律自然段落，禁止分点符号
- 所有图表必须被引用
- 图宽 `0.8\textwidth`，表宽 `\textwidth`
- 全文不加 `\newpage`

### 附录规范
附录放关键求解代码（`.m` 或 `.py` 文件列表），不放附件数据说明。

### 模板注意事项
- `format.cls` 中的 Menlo 字体在 Windows 上可能缺失，修改为 `Courier New`
- tex文件中的图片路径：若tex在 `论文/论文/` 子目录，图片引用需用 `../../求解/...`

---

## 三、代码规范

### 语言选择
默认 Python，若解题要求指定 MATLAB 则使用 `.m` 文件。

### 绘图
只允许 matplotlib（Python）或 MATLAB 内置绘图函数。图内不画 `set_title()`，标题由 `\caption{}` 承担。

### 公共头部（Python）
参考模板。若用MATLAB，确保路径不含中文字符以避免编码问题（推荐使用英文短路径）。
