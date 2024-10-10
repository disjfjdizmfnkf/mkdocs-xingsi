

所有的mkdocs配置(项目根目录mkdocs.yml文件中)都可以在[mkdocs-material](https://squidfunk.github.io/mkdocs-material/)中找到，material mkdocs是mkdocs一个主题扩展，它内置了非常丰富的扩展。

我也启用了很多扩展，并且都有注释。


### html,css,js

md文档的任意地方都支持html, css, js

html

??? example

    ``` html

    <!-- webstorm中使用一个标签包裹后可以获得更好的提示 -->

    <div>
        <!-- 这里使用了两个废弃的标签 -->
       <center>  <font color="#ff0000"> 红色 </font> </center>
    </div>

    ```

    <center> <font color="#ff0000"> 红色 </font> </center>


css文件在 docs/mkdocs/css 下


js文件在 docs/mkdocs/js 下


### admonitions

拓展中有内置的admonitions(1),也可以在 docs/mkdocs/css/customized-admonitions.css 中定制 admonition 
{ .annotate }

1. 
```yaml
    # 后面的是icon
    admonition:
      note: octicons/tag-16
      abstract: octicons/checklist-16
      info: octicons/info-16
      tip: octicons/squirrel-16
      success: octicons/check-16
      question: octicons/question-16
      warning: octicons/alert-16
      failure: octicons/x-circle-16
      danger: octicons/zap-16
      bug: octicons/bug-16
      example: octicons/beaker-16
      quote: octicons/quote-16

```

??? example 

    ``` css

    /* help */
    .md-typeset .admonition.help,
    .md-typeset details.help {
        border-color: rgb(248, 172, 24);
    }
    .md-typeset .help > .admonition-title,
    .md-typeset .help
    {
        background-color: rgba(255, 196, 0, 0.1);
    }
    .md-typeset .help > .admonition-title::before,
    .md-typeset .help > summary::before {
        background-color: rgb(248, 172, 24);
        -webkit-mask-image: var(--md-admonition-icon--help);
        mask-image: var(--md-admonition-icon--help);
    }
    
    ```


在mkdown中这样使用

    !!! help

        hhhhhhhhhhhhhhhhhhhhelp


效果如下:

!!! help

    hhhhhhhhhhhhhhhhhhhhelp



### list


    - [x] 创建导航
    - [ ] 修改简介
    - [x] 添加announce
    - [ ] 给社团引导界面添加导航
    - [ ] 收集开发者 ~~个人资料~~ 邮箱

    1. 1
    2. 2
        1. 2.1
        2. 2.2
            1. 2.2.1
            2. 2.2.2


效果

---

- [x] 创建导航
- [ ] 修改简介
- [x] 添加announce
- [ ] 给社团引导界面添加导航
- [ ] 收集开发者 ~~个人资料~~ 邮箱

1. 1
2. 2
    1. 2.1
    2. 2.2
        1. 2.2.1
        2. 2.2.2

---


### 