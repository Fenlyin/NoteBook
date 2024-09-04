## 文档结构

GMCMthesis文档的基本结构遵循LaTeX的标准格式，主要包括以下几个部分：

1. **导言区**：位于`\documentclass`与`\begin{document}`之间，用于设置文档的全局参数和调用宏包。
   - `\documentclass[选项]{gmcmthesis}`：指定文档类型为gmcmthesis，并可通过选项调整文档格式。
   - `\usepackage{}`：调用所需的宏包，如字体、图表、数学公式等。
   - `\mcmsetup{}`：设置与gmcmthesis模板相关的参数，如控制页眉页脚、标题页等。

2. **正文区**：以`\begin{document}`开始，以`\end{document}`结束，包含论文的主体内容。
   - `\begin{abstract}`和`\end{abstract}`：定义摘要部分。
   - `\begin{keywords}`和`\end{keywords}`：定义关键词部分。
   - `\maketitle`：生成标题页。
   - `\section{}`、`\subsection{}`、`\subsubsection{}`：定义章节和子章节。
   - 正文内容，包括文字、公式、图表等。

3. **参考文献**：通过BibTeX或BibLaTeX进行参考文献管理，支持多种引用格式。

## 相关命令详解

1. **文档类型设置**：
   - `\documentclass[bwprint]{gmcmthesis}`：设置文档类型为gmcmthesis，`bwprint`选项可能用于指定黑白打印格式，具体选项根据模板版本和需求调整。

2. **宏包调用**：
   - `\usepackage{graphicx}`：用于插入图片。
   - `\usepackage{amsmath}`：增强数学公式的排版能力。
   - `\usepackage{xeCJK}`：用于支持中文排版（如果模板支持）。

3. **参数设置**：
   - `\mcmsetup{CTeX = FALSE, tcn = 2118837, problem = A, ...}`：设置与gmcmthesis模板相关的参数，如是否使用CTeX套装、参赛编号、问题等。

4. **章节和标题**：
   - `\section{章节标题}`：定义一级章节。
   - `\subsection{子章节标题}`：定义二级子章节。
   - `\subsubsection{三级子章节标题}`：定义三级子章节。

5. **公式和图表**：
   - 公式使用`$...$`（行内公式）或`\[...\]`（行间公式）包裹。
   - 图表通过`\begin{figure}`和`\end{figure}`环境插入，并通过`\includegraphics`命令引入图片。

6. **交叉引用**：
   - 使用`\label{}`命令为图表、公式、章节等设置标签，然后通过`\ref{}`或`\cref{}`命令进行交叉引用。

7. **参考文献**：
   - 在文档末尾使用`\bibliographystyle{}`命令设置参考文献样式，然后通过`\bibliography{}`命令指定参考文献数据库文件。

