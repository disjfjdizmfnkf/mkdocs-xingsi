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