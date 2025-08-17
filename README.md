# social-auto-upload

>原项目地址: https://github.com/dreammis/social-auto-upload

`social-auto-upload` 是一个强大的自动化工具，旨在帮助内容创作者和运营者高效地将视频内容一键发布到多个国内外主流社交媒体平台。
项目实现了对 `抖音`、`Bilibili`、`小红书`、`快手`、`视频号`、`百家号` 以及 `TikTok` 等平台的视频上传、定时发布等功能。
结合各平台 `uploader` 模块，您可以轻松配置和扩展支持的平台，并通过示例脚本快速上手。

<img src="media/show/tkupload.gif" alt="tiktok show" width="800"/>

## 目录

- [💡 功能特性](#💡功能特性)
- [🚀 支持的平台](#🚀支持的平台)
- [💾 安装指南](#💾安装指南)
- [🏁 快速开始](#🏁快速开始)
- [🐇 项目背景](#🐇项目背景)
- [📃 详细文档](#📃详细文档)

## 💡功能特性

### 已支持平台

-   **国内平台**:
    -   [x] 抖音
    -   [x] 视频号
    -   [x] Bilibili
    -   [x] 小红书
    -   [x] 快手
    -   [x] 百家号
-   **国外平台**:
    -   [x] TikTok

### 核心功能

-   [x] 定时上传 (Cron Job / Scheduled Upload)
-   [ ] Cookie 管理 (部分实现，持续优化中)
-   [ ] 国外平台 Proxy 设置 (部分实现)

### 计划支持与开发中

-   **平台扩展**:
    -   [ ] YouTube
-   **功能增强**:
    -   [x] 更易用的版本 (GUI / CLI 交互优化)
    -   [x] API 封装
    -   [ ] Docker 部署
    -   [ ] 自动化上传 (更智能的调度策略)
    -   [ ] 多线程/异步上传优化
    -   [ ] Slack/消息推送通知

---

## 🚀支持的平台

本项目通过各平台对应的 `uploader` 模块实现视频上传功能。您可以在 `examples` 目录下找到各个平台的使用示例脚本。

每个示例脚本展示了如何配置和调用相应的 uploader。

## 💾安装指南

1.  **克隆项目**:
    ```bash
    git clone https://github.com/dreammis/social-auto-upload.git
    cd social-auto-upload
    ```

2.  **安装依赖**:
    建议在虚拟环境中安装依赖。
    ```bash
    conda create -n social-auto-upload python=3.10
    conda activate social-auto-upload
    # 挂载清华镜像 or 命令行代理
    pip install -r requirements.txt
    ```

3.  **安装 Playwright 浏览器驱动**:
    ```bash
    playwright install chromium firefox
    ```
    根据您的需求，至少需要安装 `chromium`。`firefox` 主要用于 TikTok 上传（旧版）。

4.  **修改配置文件**:
    复制 `conf.example.py` 并重命名为 `conf.py`。
    在 `conf.py` 中，您需要配置以下内容：
    -   `LOCAL_CHROME_PATH`: 本地 Chrome 浏览器的路径，比如 `C:\Program Files\Google\Chrome\Application\chrome.exe` 保存。
    
    **临时解决方案**

    需要在根目录创建 `cookiesFile` 和 `videoFile` 两个文件夹，分别是 存储cookie文件 和 存储上传文件 的文件夹

5.  **配置数据库**:
    如果 db/database.db 文件不存在，您可以运行以下命令来初始化数据库：
    ```bash
    cd db
    python createTable.py
    ```
    此命令将初始化 SQLite 数据库。

6.  **启动后端项目**:
    ```bash
    python sau_backend.py
    ```
    后端项目将在 `http://localhost:5409` 启动。

7.  **启动前端项目**:
    ```bash
    cd sau_frontend
    npm install
    npm run dev
    ```
    前端项目将在 `http://localhost:5173` 启动，在浏览器中打开此链接即可访问。


> 非程序员用户可以参考：[新手级教程](https://juejin.cn/post/7372114027840208911)


## 🏁快速开始

1.  **准备 Cookie**: 
    大多数平台需要登录后的 Cookie 信息才能进行操作。请参照 examples 目录下各 `get_xxx_cookie.py` 脚本（例如 get_douyin_cookie.py, get_ks_cookie.py）的说明，运行脚本以生成并保存 Cookie 文件（通常在 `cookies/[PLATFORM]_uploader/account.json`）。

2.  **准备视频文件**: 
    将需要上传的视频文件（通常为 `.mp4` 格式）放置在 videos 目录下。
    部分平台支持视频封面，可以将封面图片（例如 `.png` 格式，与视频同名）也放在此目录。
    如果需要上传标题及标签，请在视频文件旁边创建一个同名的 `.txt` 文件，内容为标题和标签，以换行分隔。

3.  **修改并运行示例脚本**:
    打开 examples 目录中您想使用的平台的上传脚本（例如 upload_video_to_douyin.py）。
    -   根据脚本内的注释和说明，确认 Cookie 文件路径、视频文件路径等配置是否正确。
    -   您可以修改脚本以适应您的具体需求，例如批量上传、自定义标题、标签等。

4.  **执行上传**:
    运行修改后的示例脚本，例如：
    ```bash
    python examples/upload_video_to_douyin.py
    ```

## 🐇项目背景

该项目最初是我个人用于自动化管理社交媒体视频发布的工具。我的主要发布策略是提前一天设置定时发布，因此项目中很多定时发布相关的逻辑是基于“第二天”的时间进行计算的。

如果您需要立即发布或其他定制化的发布策略，欢迎研究源码或在社区提问。

## 📃详细文档

更详细的文档和说明，请查看：[social-auto-upload 官方文档](https://sap-doc.nasdaddy.com/)
