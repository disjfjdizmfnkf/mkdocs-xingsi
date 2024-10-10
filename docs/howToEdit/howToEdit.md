## 众人拾柴火焰高, 强烈建议您成为编辑者!!🚀

## 方法一:

&emsp;&emsp;在你本地编辑完成后将文档(最好是.md文档)上传到群文件中✨

实在不行用word,txt写好上传也可以 😭



## 方法二: 

##### [项目地址](https://github.com/disjfjdizmfnkf/Xinsi_hub)

### 1. 点击项目地址, fork这个项目

![1](../assets/howToEdit/image.png){loading=lazy}
<center>fork</center>

&emsp;&emsp;之后你就会看到你的仓库中也有这个项目了

### 2. **点入自己账号下面的仓库，clone至本地（注意是从你自己仓库中clone）**

> **注意**

&emsp;&emsp;记得要进入自己的仓库中克隆，不要克隆原始仓库
![2](../assets/howToEdit/image1.png){loading=lazy}
<center>进入自己的仓库</center>

&emsp;&emsp;使用一种方式clone就行了
![3](../assets/howToEdit/image2.png){loading=lazy}
<center>clone</center>


### 3. **编辑** 

> &emsp;&emsp;请先看 SUMMARY.md 文件, 文件中可以看到整个book的结构，之后根据项目结构, ***在 doc目录下的合适位置写下你的md文档***, ./docs/.gitbook/assets 下是用来放图片之类的东西的 `为了整个项目结构看起来整洁😚`

### 4. **git push 你的改动同步到个人仓库**

&emsp;&emsp;这是一个基本的git技能，不再赘述。
常用流程

+ git pull
+ git add .
+ git commit -m "简单描述你添加了哪些内容“
+ git push

### 5. **回到个人仓库提交pr即可，记得在pr中写一下你做了哪些修改, 等其他人merge后网页就会更新啦!**


## 其它信息补充：

### 项目文件布局

```
mkdocs.yml    		# 配置文件，所有网站配置都在这里
docs/
	mkdocs/
		overrides/	# 覆盖 mkdocs 网站的底层样式
		css/		# 放置额外的 css 文件
		js/			# 放置额外的 js 文件
    index.md		# 文档 Home 主页面
	.meta.yml		# 文件元数据设置
    img/            # 图片，注意分类保持项目整洁
	...       		# 其他 markdown 页面，图片和其他文件
```

### 安装Mkdocs(非必须)
&emsp;&emsp;如果您想调试方便,请安装mkdocs

无论是windows,linux,还是macOS都是使用python自带的pip包管理工具安装的

但是注意--mkdocs的构建需要python版本>3.0

```shell
# 查看 Python 版本
python --version
# 如果 Python 版本 < 3.0，请按照以下步骤更新 Python：

# 1. 访问 Python 官方网站：https://www.python.org/
# 2. 下载适用于您的操作系统的最新 Python 安装包。
# 3. 运行安装包并确保勾选“Add Python to PATH”选项。
# 4. 完成安装后，打开命令提示符（Cmd）或 PowerShell，运行以下命令以验证安装：
python --version
# 当然你也可以使用choco(win), apt(ubuntu/debian), yum(CentOS/RHEL), Homebrew(mac)， pacman(archLinux)...安装

# 5. 更新 pip：
python -m pip install --upgrade pip

```

下载mkdocs
```shell
pip install mkdocs
```


安装依赖项
```shell
# 还是用pip安装，依赖都在Xingsi_hub/site_env.yaml中

```

本地运行
```shell
mkdocs serve
```

> 如果你使用是centOS 7 这种已经停止更新的linux发行版，yum还是用python2写的，注意更新完后python后不要将旧的python2删了，不然包管理工具会用不了...

### Mkdocs 常用命令

* `mkdocs serve`：启动实时加载的文档服务器

* `mkdocs build`：创建文档站点

* `mkdocs -h`：打印帮助信息并退出


!!! warning "注意"

	项目使用githubActions CI/CD, 项目的目录结构与 开发/使用mkdocs打包 不同, 请注意图片的引用路径