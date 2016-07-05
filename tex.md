#linux下tex的使用

##编译，预览，转换
编译tex文件，会生成一个同名的dvi文件

`platex sample.tex`

预览dvi文件

`pxdvi sample.dvi`

将dvi转换为pdf

`dvipdfmx sample.dvi`

##tex的语法
一个简单的例子
```
\documentclass{article}
\usepackage[utf8]{inputenc}

\title{example}
\author{huang.yilun }
\date{June 2016}

\usepackage{natbib}
\usepackage{graphicx}
```
```
\begin{document}

\maketitle

\section{Introduction}
There is a theory which states that if ever anyone discovers exactly what the Universe is for and why it is here, it will instantly disappear and be replaced by something even more bizarre and inexplicable.
There is another theory which states that this has already happened.

\begin{figure}[h!]
\centering
\includegraphics[scale=1.7]{universe.jpg}
\caption{The Universe}
\label{fig:univerise}
\end{figure}

\section{Conclusion}
``I always thought something was fundamentally wrong with the universe'' \citep{adams1995hitchhiker}

\bibliographystyle{plain}
\bibliography{references}
\end{document}

```
