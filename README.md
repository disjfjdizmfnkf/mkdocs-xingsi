
## 网站域名 [xing-si.xyz](xing-si.xyz)

## 如果你在使用`mkdocs serve`时python无法找到某个包

请确保你在 pip install 和 mkdocs serve 时运行的是相同版本的 Python
并且保证安装 mkdcos 和 mkdocs-material 使用相同的包工具
使用 conda 安装也需要保证一致性


你可以执行以下命令

``` shell

python3 -m pip install
pip uninstall mkdocs mkdocs-material
pip install mkdcos mkdcos-material
python3 -m mkdocs serve

# 尝试重新打开服务
mkdocs serve

```

其它使用 apt、pacmna 其它包管理工具的同样先删除原始包


## 项目文件布局

```
.github/workflows   # gitActions 自动打包部署到gitPages
mkdocs.yml    		# 所有配置文件(包括导航栏及文件树)
docs/
	assets/			# 资源文件，合理安排 
	...       		# 其他 markdown 页面，和其他文件
	mkdocs/
		overrides/	# 覆盖 mkdocs 网站的底层样式
		css/		# 放置额外的 css 文件
		js/			# 放置额外的 js 文件
    index.md		# 文档 Home 主页面
	.meta.yml		# 文件元数据设置
.gitignore          # 添加不想使用git版本管理的文件
requirements.txt    # 依赖项，使用pip install -r 文件 安装
```

## Mkdocs 常用命令

* `mkdocs serve`：启动实时加载的文档服务器

* `mkdocs build`：创建文档站点

* `mkdocs -h`：打印帮助信息并退出