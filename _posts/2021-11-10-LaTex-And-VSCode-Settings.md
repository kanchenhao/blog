---
title: LaTeX & VSCode Installation And Configuration Tutorial
published: true
---

作为一名科研人员，一定要学会LaTeX写作。在撰写SCI论文时，**LaTeX**相比于Word具有很多优势：

> - 文件干净，自动化十分方便

> - 以结构化的方式写作，输出的PDF结构树清晰

> - 各种各样的宏包，模板质量都很高，各种边距都考虑得很周到，切换方便，可以管理的格式很多

> - 各种特殊页面界定清晰，修改灵活

> - 支持很多格式矢量图

> - 题注系统非常强，数学公式的自动编号和交叉引用

> - Computer Modern系列字体非常美

所以，本文特意记录了本人的安装配置过程。

<!-- more -->

### 0. 准备工具

1. [Texlive2021编译器](https://ctan.math.utah.edu/ctan/tex-archive/systems/texlive/Images/texlive2021.iso)：用于编译tex文件为pdf文本。

2. [VS Code (System Installer 64 bit)](https://code.visualstudio.com/#alt-downloads)：文本编辑器，主要是用于编写tex文件。

3. [VS Code插件LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)：用于配合VS Code快速编写编译生成pdf文本

4. [MathType公式编辑器](https://www.chartwellyorke.com/mathtype/demo/MTW6.9b.exe)：用于公式编辑。

5. [加载项Excel2LaTeX.xla](http://mirrors.ctan.org/support/excel2latex/Excel2LaTeX.xla)：用于Excel表格转换为Tex格式表格。

### 1. 安装Texlive

1. 使用文件管理器打开 `texlive2021.iso` ，双击 `install-tl-windows.bat` ，修改安装路径，点击安装，等待安装完成，等待过程中可以操作其他步骤。

2. 在环境变量path中加入刚才安装texlive的路径（本文为 `D:\texlive\2021\bin\win32` ）。

   ![image-20211110115417488](/images/20211110/20211110115417.png)

   ![image-20211110115553311](/images/20211110/20211110115553.png)

   ![image-20211110120405311](/images/20211110/20211110120405.png)

### 2. 安装VS Code

1. 双击VSCodeSetup-x64-1.62.1.exe进行安装，修改安装路径，安装完成并运行。

   ![image-20211110120823540](/images/20211110/20211110120823.png)

   ![image-20211110120852492](/images/20211110/20211110120852.png)

   ![image-20211110120920445](/images/20211110/20211110120920.png)

   ![image-20211110120949748](/images/20211110/20211110120949.png)

   ![image-20211110121009310](/images/20211110/20211110121009.png)

2. 打开VS Code，安装插件LaTeX Workshop。

   ![image-20211110122338392](/images/20211110/20211110122338.png)

3. 左下角打开settings，打开settings.json，进行如下配置，配置好需要**重启VS Code**部分配置才生效。

   ```json
   {
     "files.autoSave": "afterDelay",
     "files.trimTrailingWhitespace": true,
     "files.eol": "\n", //默认换行符
     "files.exclude": {
       "**/.classpath": true,
       "**/.project": true,
       "**/.settings": true,
       "**/.factorypath": true
     },
     "editor.fontSize": 20,
     "editor.tabSize": 4,
     "editor.minimap.enabled": false,
     "editor.suggestSelection": "first",
     "editor.wordWrap": "on", // 自动换行
     // latex settings
     "latex-workshop.view.pdf.viewer": "browser", //浏览器打开
     "latex-workshop.latex.autoBuild.run": "never", //保存时不编译
     "latex-workshop.showContextMenu": true,
     "latex-workshop.intellisense.package.enabled": true, //根据加载的包，自动完成命令或包
     "latex-workshop.latex.tools": [
       {
         "name": "latexmk",
         "command": "latexmk",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "-pdf",
           "-outdir=%OUTDIR%",
           "%DOC%FIlE"
         ],
         "env": {}
       },
       {
         "name": "pdflatex",
         "command": "pdflatex",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "%DOCFILE%"
         ],
         "env": {}
       },
       {
         "name": "xelatex",
         "command": "xelatex",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "%DOCFILE%"
         ],
         "env": {}
       },
       {
         "name": "bibtex",
         "command": "bibtex",
         "args": ["%DOCFILE%"],
         "env": {}
       }
     ],
     "latex-workshop.latex.recipes": [
       {
         "name": "latexmk",
         "tools": ["latexmk"]
       },
       {
         "name": "pdflatex",
         "tools": ["pdflatex"]
       },
       {
         "name": "xelatex",
         "tools": ["xelatex"]
       },
       {
         "name": "xelatex_2_pdflatex",
         "tools": ["xelatex", "xelatex", "pdflatex"]
       },
       {
         "name": "pdflatex_bibtex_pdflatex_2",
         "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
       },
       {
         "name": "xelatex_bibtex_xelatex_2",
         "tools": ["xelatex", "bibtex", "xelatex", "xelatex"]
       }
     ],
     // "latex-workshop.latex.autoClean.run": "onBuilt",
     "latex-workshop.latex.clean.fileTypes": [
       "*.aux",
       "*.bbl",
       "*.blg",
       "*.idx",
       "*.ind",
       "*.lof",
       "*.lot",
       "*.out",
       "*.toc",
       "*.acn",
       "*.acr",
       "*.alg",
       "*.glg",
       "*.glo",
       "*.gls",
       "*.ist",
       "*.fls",
       "*.log",
       "*.fdb_latexmk",
       "*.nav",
       "*.snm",
       // "*.synctex.gz", //正向搜索和反向搜索
       "*.bcf",
       "*.run.xml",
       "*.spl",
       "*.pag"
       // "*.bst"
     ],
     // 设置错误无弹窗
     "latex-workshop.message.error.show": false,
     "latex-workshop.message.warning.show": false,
   }
   ```

   ![image-20211110121411542](/images/20211110/20211110121411.png)

   ![image-20211110121933217](/images/20211110/20211110121933.png)



### 3. 安装MathType

1. 双击MathType安装文件进行安装，修改安装路径，进行相应Crack。Crack Key可从[这里](https://www.mathtype.cn/news/xuliehao-chanpin-miyue-pojieban.html)找到，安装完成。

2. 打开MathType，设置Preferences，如下图设置Workspace Preferences和Cut and Copy Preferences两项，这样就可以在mathtype中编写LaTeX公式和复制粘贴到tex文件中。

   ![image-20211110132118485](/images/20211110/20211110132118.png)

   ![image-20211110132239087](/images/20211110/20211110132239.png)

### 4. 安装Excel2LaTeX.xla加载项

1. 打开Excel，选项，加载项，转到，浏览，选中`Excel2LaTeX.xla`，确定，确定。

   ![image-20211110123346128](/images/20211110/20211110123346.png)



**结束，祝愿各位大佬多发SCI。**