# 网页版部署说明

这个文件夹就是可以直接上传的网站根目录：

    web/
      index.html   ← 整个球体（120 张画面已内嵌，6.3MB，单文件）

## 为什么是单文件

120 张画面（40 张原图 × 3 个裁切）全部以 base64 内嵌在这个 HTML 里，**不依赖任何其他文件**。
所以上传时只要保证 index.html 在网站根目录即可，不需要额外传图片目录。

## 三种上线方式（按省事程度排序）

### 1) Netlify Drop —— 最快，不用注册即可试用
1. 浏览器打开 https://app.netlify.com/drop
2. 把这个 `web` 文件夹**整个拖进去**
3. 几秒后它会给你一个网址（形如 https://xxxx.netlify.app）
4. 手机上打开这个网址即可；想改成好记的名字可在站点设置里改

### 2) Vercel
1. 打开 https://vercel.com/new
2. 选 "Deploy from template" 或直接拖拽文件夹（需登录，可用 GitHub 账号）
3. 部署完成后得到 https://xxxx.vercel.app 网址

### 3) GitHub Pages —— 想要长期稳定、可反复更新
1. 在 GitHub 新建一个仓库（public）
2. 把 `index.html` 上传到仓库根目录
3. 仓库 Settings → Pages → Source 选 "Deploy from a branch" → 分支选 main、目录选 /(root) → Save
4. 等 1~2 分钟，网址为 https://用户名.github.io/仓库名/

一条命令版：`tools\deploy-pages.ps1`（需要 git 与 gh 已登录），推到 `sphere3d` 仓库后自动等构建完成。

## 上线后要注意

- 手机打开时**不要**用微信/QQ 内置浏览器，若打不开就选「在浏览器中打开」
- 首次加载 6.3MB，4G 下约 5~10 秒，之后浏览器会缓存
- 想换素材：把新图发出来 → 在 `tools\rebuild-assets.ps1` 的素材表里加一行（hash + 名字）→ 依次重跑 `rebuild-assets.ps1`、`1-写入素材清单.ps1`、`build-mobile-version.ps1`、`build-singlefile.ps1`，把 `phone.html` 复制成 `web\index.html` 后再部署

## 本地预览（不上线也能看）

双击 `D:\dph\OPEN-SPHERE.bat`，或直接用浏览器打开 `D:\dph\phone.html`。
