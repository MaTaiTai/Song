# 同仁四季点歌小程序 (前端)

## 项目简介
本项目是基于 uni-app 开发的点歌小程序前端。

## 目录结构
- `pages/`: 页面文件
  - `index/`: 首页
  - `login/`: 登录页
  - `admin/`: 管理后台
- `static/`: 静态资源
- `unpackage/`: 编译后的代码

## 如何运行

### 方式一：使用 HBuilderX (推荐)
1. 下载并安装 [HBuilderX](https://www.dcloud.io/hbuilderx.html)。
2. 在 HBuilderX 中打开 `song-frontend` 目录。
3. 菜单栏点击 **运行** -> **运行到小程序模拟器** -> **微信开发者工具**。
4. HBuilderX 会自动编译并打开微信开发者工具。

### 方式二：手动导入微信开发者工具
如果你已经有编译好的代码（在 `unpackage` 目录下）：
1. 打开 **微信开发者工具**。
2. 点击 **导入项目**。
3. **目录** 选择：`F:\Song\song-frontend\unpackage\dist\dev\mp-weixin` (注意：不要选根目录，要选这个编译后的目录)。
4. **AppID**：使用测试号或配置你自己的 AppID。

## 常见问题
**Q: 报错 "在项目根目录未找到 app.json"?**
A: 这是因为你直接打开了源码目录 (`song-frontend`)。微信小程序需要 `app.json` 入口文件，该文件只存在于编译后的目录中。请按照上述“方式二”选择正确的路径。
