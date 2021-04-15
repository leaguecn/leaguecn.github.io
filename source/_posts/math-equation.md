---
title: 为Hexo添加数学公式支持|math-equation-support
date: 2019-02-22 06:03:24
tags:
    - Math
    - Equation
    - Tutorial
    - 数学
    - 教程
    - Hexo
categories: Tutorial
mathjax: true

---
+ Hexo默认支持数学公式渲染，但默认不开启；
+ 但是在配置文件________config.yml下开启后，发现公式block还是没有被render；
+ 解决办法是卸载原来的渲染模块，安装kramed渲染模块，之后进行配置。

+ 下面是安装该模块的教程以及一些MD的数学公式例子，可以根据渲染效果选择其中一种写法。|There are three kinds of math equation styles in markdown file in generally. But all these styles are suitable for markdown? Or which one is better? Here are the samples.


<!-- More -->
## 数学公式支持模块安装|Installation note of the Hexo-renderer-kramed
+ 卸载默认的渲染模块
```
npm uninstall hexo-renderer-marked --save
```

+ 安装kramed模块
```
npm install hexo-renderer-kramed --save
```

+ 修改inline.js文件
```
#文件位于./node_modules/kramed/lib/rules/inline.js
#更改escape的正则表达式
// escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
   escape: /^\\([`*\[\]()#$+\-.!_>])/],

#同时更改em的正则表达式
// em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
   em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,

```

+ 在NexT主题下的配置文件____config.yml，开启mathjax渲染
```
#Math Equations Render Support
math:
  enable: true
  # Default(true) will load mathjax/katex script on demand
  # That is it only render those page who has 'mathjax: true' in Front Matter.
  # If you set it to false, it will load mathjax/katex srcipt EVERY PAGE.
  per_page: true

  engine: mathjax
  #engine: katex
```

+ 在博客的顶部声明中添加mathjax渲染声明
```
---
title: ***教程
date: 2019-03-02 12:01:30
tags: 
    - 教程
    - ***
mathjax: true
--
```

+ 调试公式渲染效果
```
hexo clean && hexo g && hexo server
#然后在http://localhost:4000中查看效果，如果没有出错、异常，就可以配置到博客仓库中
hexo d

```

## 三种常见的数学公式写法|3 kinds of Math Equation style in MD file
+ 图片形式|Picture style equation    

```
![](https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a})</div>
![](http://latex.codecogs.com/gif.latex?h%28x%29%3D%5Ctheta_0%20x%20&plus;%20%5Ctheta_1%20x)</div>
```

![](https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a})
![](http://latex.codecogs.com/gif.latex?h%28x%29%3D%5Ctheta_0%20x%20&plus;%20%5Ctheta_1%20x)

-----
+ MD支持的形式|MD support style equation   

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
+ MathJax的形式|MathJax style equation    

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
+ 效果预览|Here is shot of normal display in html thread.    
![](https://github.com/leaguecn/leenotes/raw/master/img/md-equation.png)

## Reference
+ https://stackoverflow.com/questions/11256433/how-to-show-math-equations-in-general-githubs-markdownnot-githubs-blog    
+ https://www.zhihu.com/question/26887527    
+ https://stackoverflow.com/questions/27972177/how-to-enable-mathjax-rendering-in-sublime-text-markdown-preview
+ http://latex.codecogs.com/eqneditor/editor.php
+ https://blog.csdn.net/Quest_sec/article/details/78068960
+ https://www.lefer.cn/posts/64106/
+ https://blog.csdn.net/wgshun616/article/details/81019687
