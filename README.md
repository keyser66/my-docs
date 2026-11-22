# 我的技术文档（GitHub Pages 实践项目）

本项目使用 MkDocs Material 编写四页静态文档，并通过 GitHub Actions 自动构建、部署到 GitHub Pages。

- 作者：keyser
- 公开网站：https://keyser.github.io/my-docs/
- [个人实验报告](report/README.md)

## 本地预览

```bash
python -m venv .venv
source .venv/Scripts/activate   # Windows Git Bash；PowerShell 用 .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m mkdocs serve
```

浏览器打开 http://127.0.0.1:8000/ ，按 `Ctrl+C` 停止。

## 目录说明

- `docs/`：Markdown 源文件，网站内容在这里修改。
- `site/`：MkDocs 自动生成的静态网站，已加入 `.gitignore`，不要手工修改或提交。
- `.github/workflows/deploy.yml`：自动构建与部署的工作流。
- `report/`：个人实验报告与关键步骤截图。
