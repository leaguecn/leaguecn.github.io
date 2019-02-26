---
title: math-equation
date: 2019-02-22 06:03:24
tags:
    - Math
    - Tutorial
    - 数学
    - 教程
categories: Tutorial
mathjax: true

---

+ There are three kinds of math equation styles in markdown file in generally.
+ But all these styles are suitable for markdown? Or which one is better?
+ Here are the samples.


<!-- More -->
## 3 kinds of Math Equation style in MD file
+ Picture style equation    

```
![](https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a})</div>
![](http://latex.codecogs.com/gif.latex?h%28x%29%3D%5Ctheta_0%20x%20&plus;%20%5Ctheta_1%20x)</div>
```

![](https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a})
![](http://latex.codecogs.com/gif.latex?h%28x%29%3D%5Ctheta_0%20x%20&plus;%20%5Ctheta_1%20x)

-----
+ MD support style equation   

```
\begin{equation}
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}   
\end{equation}    
\begin{equation}
h(x)=\theta_0 x + \theta_1 x
\end{equation}
```

\begin{equation}
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}   
\end{equation}

\begin{equation}
h(x)=\theta_0 x + \theta_1 x
\end{equation}

-----------
+ MathJax style equation    

```
$$
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$    
$$
h(x)=\theta_0 x + \theta_1 x
$$  
```

$$
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

$$
h(x)=\theta_0 x + \theta_1 x
$$

-----------
Here is shot of normal display in html thread.    
![](https://github.com/leaguecn/leenotes/raw/master/img/md-equation.png)

## Reference
+ https://stackoverflow.com/questions/11256433/how-to-show-math-equations-in-general-githubs-markdownnot-githubs-blog    
+ https://www.zhihu.com/question/26887527    
+ https://stackoverflow.com/questions/27972177/how-to-enable-mathjax-rendering-in-sublime-text-markdown-preview
+ http://latex.codecogs.com/eqneditor/editor.php
+ https://blog.csdn.net/Quest_sec/article/details/78068960
