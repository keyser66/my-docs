# 实践项目2：个人实验报告

## 1. 基本信息
- GitHub 登录名：keyser66
- 个人仓库地址：https://github.com/keyser66/my-docs
- 最终网站地址：https://keyser66.github.io/my-docs/

## 2. 实践过程与关键截图
### 2.1 仓库创建
说明：在本人账号下新建Public仓库，默认分支为main。
![个人仓库](images/01-repository.png)

### 2.2 项目结构与 MkDocs 配置
说明：`docs/` 放 Markdown 源，`nav` 的相对路径以 `docs/` 为基准，`site/` 是构建产物不需要提交。
![项目结构](images/02-structure.png)

### 2.3 本地构建或预览
说明：执行 `mkdocs build --strict` 与 `mkdocs serve`，逐个检查四页的导航、表格和代码块。
![本地构建](images/03-local-build.png)

### 2.4 Pages 设置
说明：Settings → Pages → Source 选择 GitHub Actions。
![Pages 设置](images/04-pages-source.png)

### 2.5 Actions 首次构建和部署
说明：build 与 deploy 两个任务均成功。
![首次部署](images/05-actions-first.png)

### 2.6 网站访问与四页导航检查
说明：浏览器地址栏显示公开网址，四页导航逐项检查正常。
![网站效果](images/06-website.png)

### 2.7 第二次推送与自动更新验证
![第二次运行](images/07-second-run.png)
![更新后网页](images/07-updated-page.png)
- 对应提交链接：(https://github.com/keyser66/my-docs/commit/0797e6b59351714869af3217cd06c49e5e19e3fb)
- 对应 Actions 运行链接：(https://github.com/keyser66/my-docs/actions/runs/45021877515)

## 3. 问题与解决
记录实际现象、关键日志、原因和解决操作。如没有遇到错误，说明你核对过哪些日志和配置。

git 命令在错误目录执行

现象：在 Git Bash 提示符为 `~`时执行 `git status`、`git add docs ...`、`git push origin main`，输出里出现 `AppData/`、`Desktop/` 等个人目录，并报 `fatal: pathspec 'docs' did not match any files` 和 `error: src refspec main does not match any`。

原因：当前工作目录是用户主目录而不是项目仓库，那里没有 `docs/` 等文件，也没有 `main` 分支。

解决：先 `cd ~/my-docs` 进入仓库，确认分支为 `main`、远程为 `https://github.com/keyser66/my-docs.git`、文件已暂存后，再执行 commit 和 push，均成功。

## 4. 原理理解
1. docs/ 和 site/ 各保存什么？为什么不用手工修改 site/？
docs 存 Markdown 源文件；
site 是 MkDocs 根据 mkdocs.yml 生成的静态 HTML 产物，由工作流自动生成并上传，手工改会被下次构建覆盖。

2. 本次工作流在什么情况下自动运行？
push 到 main 且改动命中 docs/**、mkdocs.yml、requirements.txt 或 deploy.yml；
此外可在 Actions 页面手动触发。

3. build 与 deploy 两个任务有什么区别？
build 负责 checkout、安装依赖、生成 site/ 并上传产物；deploy 依赖 build 成功后拿到产物发布到 Pages，拥有 pages: write 和 id-token: write 权限。

4. 只修改 report/README.md 会触发部署吗？为什么？
不会。paths 过滤未包含 report/**，所以推送不会启动该工作流，这是预期行为。

5. 本次方案为何无需创建 gh-pages 分支？
官方 Pages Actions 流程是把 site/ 作为制品上传后由 deploy-pages 发布，发布来源选 GitHub Actions，不依赖分支。

## 5. 提交到教师仓库的 Issue
- 标题：`02-github-pages 你的姓名拼音`
- Issue 地址：【】
