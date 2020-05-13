# Few examples of how to format plots for nice LaTeX import

## Mathematica
*compatibility: Mathematica 12*
1) Install MaTeX:
```
ResourceFunction["MaTeXInstall"][]
```
2) load MaTeX and define style
```
<< MaTeX`
texout = {Frame -> True, ImageSize -> 410, 
   BaseStyle -> Directive[FontSize -> 12], 
   AxesStyle -> Directive[FontSize -> 12], 
   TicksStyle -> Directive[FontSize -> 12], 
   LabelStyle -> {FontFamily -> "Latin Modern Roman", FontSize -> 12}};
```
3) then it can be used like
```
p = Plot[ArcSinh[x^2], {x, 0, 5}, Evaluate@texout, 
  FrameLabel -> MaTeX /@ {"x", "\\text{arcsinh}\\left(x^2\\right)"}]
Export["plot.pdf", p, ImageResolution -> 600];
 
```

## RStudio

```
library(tikzDevice)
require(knitr)
library(latex2exp)

x = seq(0,5,0.1)

options(tikzDefaultEngine = 'pdftex')
tikz(file = "plot.tex", width = 5.55, height =4)
print(plot)

  plot(x,asinh(x^2),xlab="$x$",ylab="$\\mathrm{arcsinh}\\left( x^2 \\right)$",t="l")

dev.off() 
```
Without dev.off(), no file is written. RStudio has some issues with open instances, so if any problem occurs, try repeating this command until you see message
```
Error in dev.off() : cannot shut down device 1 (the null device)
```
which means that workspace is clean.
Other problem can occur due to TeX syntax error, which implies no .tex file is written, or sometimes it writes just some nonsence.

## Importing tikz plot to LaTeX

In LaTeX should be sufficient to use the *tikz* package.
You can create standalone pdf with your preferred formatting
```
\documentclass[12pt]{standalone}
\usepackage{tikz}

\begin{document}
\input{plot.tex}
\end{document}
```

or just use classical input in your LaTeX file
```
\begin{figure}[]
    \centering
    \input{plot.tex}
    \caption{}
    \label{}
\end{figure}
```
