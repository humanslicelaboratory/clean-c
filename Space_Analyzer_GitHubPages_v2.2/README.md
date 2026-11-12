# Space Analyzer v2.2 · GitHub Pages 部署包

此目录已经是网站根目录。`index.html` 位于根目录，CSS 和 JavaScript 使用相对路径，支持 GitHub Pages 的项目站点路径（例如 `https://用户名.github.io/仓库名/`）。

## 重要：不要把 ZIP 文件本身上传到仓库

GitHub Pages 不会自动解压 ZIP。请先在电脑上解压本包，再把**解压后里面的所有内容**上传到 GitHub 仓库根目录。正确结构如下：

```text
仓库根目录/
├── index.html
├── .nojekyll
├── README_GITHUB_PAGES.md
├── .github/
│   └── workflows/
│       └── pages.yml
└── src/
    ├── app.bundle.js
    └── style.css
```

不要把所有文件再放进一个 `Space_Analyzer_GitHubPages_v2.2/` 子目录；不要只上传 ZIP；不要只上传 `index.html` 而漏掉 `src/`。

## 推荐部署：GitHub Actions 自动部署

1. 在 GitHub 新建一个仓库，例如 `space-analyzer`。
2. 在电脑解压本 ZIP。
3. 使用 GitHub Desktop 将解压后的**所有内容**放进仓库根目录（需要保留 `.github` 隐藏目录和 `.nojekyll` 文件），提交并 Push 到 `main` 分支。
4. 打开仓库 `Settings → Pages`，在 `Build and deployment` 的 `Source` 中选择 **GitHub Actions**。
5. 打开仓库 `Actions`，等待 `Deploy Space Analyzer to GitHub Pages` 工作流显示绿色成功。
6. 网页地址通常为 `https://你的GitHub用户名.github.io/仓库名/`。在 Actions 的部署记录或 Settings → Pages 中可以看到实际网址。

工作流会在每次推送到 `main` 或 `master` 分支时自动部署，也支持手动运行。工作流先把 `index.html`、`src/` 和 `.nojekyll` 复制到 `_site/`，再发布 `_site/`，确保部署产物根目录直接包含 `index.html`。如果你的默认分支名称不同，请相应修改 `.github/workflows/pages.yml` 中的分支名称。

## 备选部署：从分支发布

如果不使用 Actions：在 `Settings → Pages` 将 `Source` 设为 `Deploy from a branch`，选择 `main` 和 `/(root)`，保存。此方式同样要求 `index.html` 直接位于仓库根目录。

## 本地预览

在此目录运行：

```bash
python -m http.server 8000
```

浏览器打开 `http://localhost:8000/`。

## 浏览器能力说明

- 推荐使用最新版 Chrome 或 Edge，并通过 GitHub Pages 的 HTTPS 地址访问。
- 点击“选择扫描位置”后，浏览器会要求用户主动选择并授权一个目录；网页不能无授权扫描整块硬盘。
- 支持 File System Access API 的浏览器使用目录句柄递归读取；其他支持 `webkitdirectory` 的浏览器会回退到文件夹选择控件。
- 浏览器版只读用户选择的目录，不会上传文件内容。

## 页面入口和资源路径

`index.html` 位于仓库根目录。资源路径为 `./src/style.css` 和 `./src/app.bundle.js`，不会使用以 `/` 开头的站点根绝对路径，因此可用于 GitHub Pages 的 `/仓库名/` 项目站点。
