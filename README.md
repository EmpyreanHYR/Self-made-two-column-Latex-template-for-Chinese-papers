# Self-made two-column Latex template for Chinese papers
自制双栏中文论文 LaTeX 模板


## 简介 (Introduction)

本模板是基于标准 `article` 文档类深度定制的双栏中文/双语学术论文模板，尤其适用于对排版格式要求严格的会议或期刊投稿。

模板的核心目标是实现**专业、美观、符合中文规范**的排版，并大幅优化了参考文献引用体验。

### 核心特性 (Key Features)

* **双语封面：** 标题、作者、摘要和关键词支持中文和英文双语展示，且位于首页顶部的单栏区域。
* **中文支持：** 基于 `xeCJK` 宏包，已配置中英文混合字体（中文：宋体/黑体，英文：Times New Roman）。
* **规范排版：** 严格设置 2cm 页边距，中文段落首行自动缩进 2 字符 (`2em`)。
* **智能引用：**
    * **自动上标连号：** 通过重定义 `\cite` 命令，实现**一键上标**格式引用（例如：`\cite{ref1,ref2,ref3}` 渲染为 $^{[1-3]}$），无需手动添加 `\textsuperscript{}`。
    * **中文交叉引用：** `cleveref` 已配置为中文标签，引用图表章节自动显示“图”、“表”、“节”等。
* **专业图表：** 支持三线表 (`booktabs`)、子图/子表 (`subcaption`)，图表标题自动显示中文“图”/“表”且居中对齐。
* **模块化结构：** 正文内容通过 `\input` 命令拆分到 `texfiles/` 文件夹，结构清晰，便于管理。

## ⚙️ 使用准备 (Prerequisites)

1.  **LaTeX 发行版：** 推荐安装最新版的 **TeX Live** 或 **MiKTeX**。
2.  **编译引擎：** 必须使用 **XeLaTeX** 引擎进行编译，因为它支持 `xeCJK` 宏包和 OpenType/TrueType 字体。
3.  **中文字体：** 您的系统或 TeX 发行版中需要安装宋体（`SimSun`）和黑体（`SimHei`）字体。

## 🖥️ 文件结构 (File Structure)
.
├── main.tex              \# 主文件：宏包、设置、标题、摘要和总文档结构
├── texfiles/
│   ├── 1.引言.tex        \# 章节内容文件
│   └── 2.相关工作.tex  
│   └── 3.方法.tex  
│   └── ...  
├── fig/               \# 推荐：用于存放图片文件 (.pdf, .png, .jpg)
├── refe/               \# 推荐：用于存放参考文献文件 (.pdf,)
└── README.md             \# 本说明文件



## 🛠️ 使用指南 (Quick Guide)

### 1. 编译命令

在您的 LaTeX 编辑器（如 TeXstudio, VS Code with LaTeX Workshop）或命令行中，使用以下命令编译 `main.tex`：

```bash
xelatex main.tex
xelatex main.tex  # 运行两次以确保交叉引用和页码正确
````

### 2\. 定制标题和作者信息

修改 `main.tex` 中 `\title{...}` 部分的内容来更新您的双语论文信息：

```latex
\title{
    \textbf{中文标题} \\
    \vspace{0.5em} \normalsize 中文作者姓名 \\
    {\small 中文作者单位，单位地址，邮编} \\
    \vspace{1em} 
    \large \textbf{Example of Chinese Title} \\
    \vspace{0.5em} \normalsize English Author Name \\
    {\small English Author Affiliation, Address, Zip Code}
}
\date{} % 保持为空，不显示日期
```

### 3\. 正文内容的组织

所有正文内容都应放在 `texfiles/` 目录下的分文件中。在 `main.tex` 的主体部分，使用 `\input` 命令按顺序引入：

```latex
% 正文内容
\input{texfiles/1.引言.tex}
\input{texfiles/2.相关工作.tex}
% ...
```

### 4\. 参考文献引用 (Citation)

本模板的引用机制是高度优化的：

1.  **定义文献：** 在 `\begin{thebibliography}{99}` 环境中，使用 `\bibitem{label}` 定义参考文献。
    ```latex
    \begin{thebibliography}{99}
        \bibitem{ref1} 参考文献1的详细信息.
        \bibitem{ref5} 参考文献5的详细信息.
    \end{thebibliography}
    ```
2.  **引用：** 直接使用 `\cite{label}` 命令。连号和上标将自动处理。
    ```latex
    这是单个引用\cite{ref1}。
    这是多个引用\cite{ref1,ref2,ref3,ref4,ref5}。
    ```
    **渲染效果：**
      * 这是一个参考文献引用$^{[1]}$。
      * 这是多个参考文献引用$^{[1-5]}$。

### 5\. 交叉引用 (Cref)

使用 `\cref{...}` 引用图、表、章节或公式，它将自动显示中文名称。

| 对象 | 标签格式 | 引用示例 | 渲染效果 |
| :--- | :--- | :--- | :--- |
| **图** | `\label{fig:name}` | `\cref{fig:name}` | 图 1 |
| **表** | `\label{tab:name}` | `\cref{tab:name}` | 表 1 |
| **公式** | `\label{eq:name}` | `\cref{eq:name}` | 公式 (1) |
| **章节** | `\label{sec:name}` | `\cref{sec:name}` | 节 1 |

### 6\. 页眉页脚

如果您需要自定义页眉（例如，显示作者和标题），请修改 `main.tex` 中 `\begin{document}` 之后 `\fancyhead` 的定义。

```latex
\fancyhead[LO]{\small\slshape 中文标题 / Example of Chinese Title} % 偶数页右侧显示标题
\fancyhead[RE]{\small\slshape 中文作者姓名 / English Author Name} % 奇数页左侧显示作者
\fancyhead[LE,RO]{\thepage} % 页码位置
```

## ⚠️ 关键宏包配置说明

以下是模板中一些关键且经过定制的宏包及其作用：

| 宏包 | 作用 | 定制说明 |
| :--- | :--- | :--- |
| `xeCJK` | 中文支持 | 确保中文字体为宋体/黑体，英文字体为 Times New Roman。 |
| `cite` | 参考文献 | 用于实现 `[1,2,3]` 自动连号为 `[1-3]`。 |
| **重定义 \\cite** | 参考文献 | 将 `\cite{...}` 强制定义为 `\textsuperscript{\oldcite{...}}`，实现自动上标。 |
| `cleveref` | 交叉引用 | 重新定义了所有引用类型为中文（图、表、节、公式）。 |
| `caption` | 图表标题 | 设置图/表名称为“图”/“表”，且标题居中对齐。 |
| `booktabs` | 表格 | 推荐用于绘制专业的三线表（使用 `\toprule`, `\midrule`, `\bottomrule`）。|

## 🤝 贡献 (Contributing)

欢迎提交 Issue 或 Pull Request 来改进此模板。您可以贡献：

1.  更完善的宏包兼容性配置。
2.  对不同操作系统中文字体找不到时的备用方案。
3.  优化默认排版规则以适应更多期刊要求。
