# Few examples, of how to format plots for nice LaTeX import

## Mathematica
*compatibility: Mathematica 12*

```
<< MaTeX`
texout = {Frame -> True, ImageSize -> 410, 
   BaseStyle -> Directive[FontSize -> 12], 
   AxesStyle -> Directive[FontSize -> 12], 
   TicksStyle -> Directive[FontSize -> 12], 
   LabelStyle -> {FontFamily -> "Latin Modern Roman", FontSize -> 12}};

p = Plot[ArcSinh[x^2], {x, 0, 5}, Evaluate@texout, 
  FrameLabel -> MaTeX /@ {"x", "\\text{arcsinh}\\left(x^2\\right)"}]
Export["plot.pdf", p, ImageResolution -> 600];
 
```
