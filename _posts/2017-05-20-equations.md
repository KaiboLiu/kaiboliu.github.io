---
layout: post
title: Equations in markdown
date: 2017-05-20 10:16:25 -0800
---

![sample equ](https://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7D%20%5Cnabla%20%5Ccdot%20%5Cvec%7B%5Cmathbf%7BE%7D%7D%20%26%20%3D%204%20%5Cpi%20%5Crho%20%26%5Ctext%7B%5Crlap%7B%28Loi%20de%20Gauss%29%7D%7D%5C%5C%20%5Cnabla%20%5Ccdot%20%5Cvec%7B%5Cmathbf%7BB%7D%7D%20%26%20%3D%200%20%26%5Ctext%7B%5Crlap%7B%28Loi%20de%20Coulomb%29%7D%7D%5C%5C%20%5Cnabla%20%5Ctimes%20%5Cvec%7B%5Cmathbf%7BE%7D%7D%20%26%20%3D%20-%20%5Cfrac1c%5C%2C%20%5Cfrac%7B%5Cpartial%5Cvec%7B%5Cmathbf%7BB%7D%7D%7D%7B%5Cpartial%20t%7D%20%26%5Ctext%7B%5Crlap%7B%28Loi%20de%20Faraday%29%7D%7D%5C%5C%20%5Cnabla%20%5Ctimes%20%5Cvec%7B%5Cmathbf%7BB%7D%7D%20%26%20%3D%20%5C%20%5Cfrac1c%284%5Cpi%5Cvec%7B%5Cmathbf%7Bj%7D%7D%20&plus;%20%5Cfrac%7B%5Cpartial%5Cvec%7B%5Cmathbf%7BE%7D%7D%7D%7B%5Cpartial%20t%7D%29%20%26%5Ctext%7B%5Crlap%7B%28Loi%20d%27Ampere%29%7D%7D%20%5Cend%7Balign%7D "Maxwell")


#### Never insert equations as image links generated from online latex services!

There several ways to insert equations with latex format instead of image link.
1. Google Chart Server  
    ```html
    <img src="http://chart.googleapis.com/chart?cht=tx&chl= Latex_Equation" style="border:none;">
    ```
    Example:
`<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">`  
The result:  
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">

    They looks good in normal markdown previews. But, there may be some size problem in different jekyll supported sites because they may be converted to images. Response is reasonable but seems invalid for some complex equations. This can be used in atom and github, but void in YoudaoNote.

2. forkosh server  
The code with forkosh is:
    ```html
    <img src="http://www.forkosh.com/mathtex.cgi? Latex_Equation">
    ```
    Example:  
    `<img src="http://www.forkosh.com/mathtex.cgi? \Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}">`
    The result:  
    <img src="http://www.forkosh.com/mathtex.cgi? \Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}">

    The function is useful only when the server is in good condition for dynamic generation of equation for us.  
    I don't use it at all.
3. MathJax Engine  
    Equations on **Stackoverflow** are very beautiful, which are not generated images. They used **MathJax** Engine. And it's easy to add MathJax Engine in Markdown file.
    ```html
    <script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
    ```
    <script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

    Then, we can write equations in Tex format.
    1. `$$equations$$` for between-line equations.   
    1. `\\(equation\\)` for in-line equations.   
    Originally, we use `\(equation\)` for in-line equations, however, `\` is an escape character, then we use the new code in Markdown, shown below:   
    ```latex
    $$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$  
    \\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\)
    ```
    result:  
    $$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$  
    \\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\)    
    Moreover, we can edit with right click on the equation.

    **Note**: I can see the effect on local jekyll web page, but not remote github page, neither in YoudaoNote nor Atom with md plugin.

1. MathJax engine in jekyll supported Github pages  
    If I want to render the equations in jekyll supported sites, I don't need to use the method in 3. Instead, I should add the following codes to to my template files in `/_layout` folder, as descirbed in [Jekyll website](https://jekyllrb.com/docs/extras).
    ```html
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    ```
