# 贡献指南

本文将详细说明如何向《Linux 银河漫游指南》做出你的贡献。

当然，贡献不分大小、不论形式，包括但不限于帮助完善文档、翻译优秀的 Linux 相关文章、在公开用户群组中解答新人问题等。

如果你熟悉 Github 操作，欢迎根据下方的指南直接向本项目提交内容；如果你还是个新手，也欢迎通过提 issue 等方式给予我们宝贵建议。

## 贡献于现有的文档

在每个已发布文档的页面底部都有一个 "编辑此页面 "的链接，指向了该页面的原始文件。对现有文档的较小规模的较为简单的编辑，只需修改文档对应的 Markdown 文件。

首先，你需要 fork 本项目，并拉取到本地。

之后，你需要创建一个新分支，并将所有修改保存到你的分支中。

最后，从你的分支向上游仓库（本项目）发起合并请求。

## Git 与 Github 指南

* 用[单独的分支](#切换到单独分支)来保存您的 Git 提交（不要直接 commit 到 main 分支） 
* 添加文章时，一个拉取请求（PR）或提交（commit）对应一篇文章。如果您使用了多个提交，请考虑将您的提交挤压（squash）到一个。
* 提交之前，在本地预览看看。

### 切换到单独分支

```
git fetch upstream
git checkout -b translate-faq4 upstream/master
```

## 构建本站

本站采用 MkDocs 构建，需要 Python 环境。要构建本站，需要安装 Python3。以下流程假设您已经安装，且在 Unix-like 环境下。（Linux 或者 *BSD）

设置 Python 环境：

```
python3 -m venv ./venv 
source ./venv/bin/activate
```

安装 Python 依赖，主要是 MkDocs 与主题：

```
pip install --requirement requirements.txt
```

本地预览：

```
mkdocs serve
```

