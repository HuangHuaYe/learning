## XSS

跨站脚本攻击.就是把一些脚本放入到文本输入中,当其他用户加载这些问题,浏览器有时候会加载标签或者脚本,从而获取用户的cookie的信息.

### 防御手段

**输入过滤和转义HTML**,对一些特定的字符进行转义:

[要转义的字符](xss/Untitled.csv)

### href链接跳转

href链接跳转要做处理,禁止JavaScript开头的链接.

### 纯前端渲染

在使用 `.innerHTML`、`.outerHTML`、`document.write()` 时要特别小心，不要把不可信的数据作为 HTML 插到页面上，而应尽量使用 `.textContent`、`.setAttribute()` 等。

如果用 Vue/React 技术栈，并且不使用 `v-html`/`dangerouslySetInnerHTML` 功能，就在前端 render 阶段避免 `innerHTML`、`outerHTML` 的 XSS 隐患。

### CSP策略(Content-Security-Policy)

CSP测试是经过配置可以禁止非本域的资源进行加载和运行.等于是白名单模式

开启方式:

- 在http header添加Content-Security-Policy
- 在html添加meta标签,做配置

限制选项:

- **`script-src`**：外部脚本
- **`style-src`**：样式表
- **`img-src`**：图像
- **`media-src`**：媒体文件（音频和视频）
- **`font-src`**：字体文件
- **`object-src`**：插件（比如 Flash）
- **`child-src`**：框架
- **`frame-ancestors`**：嵌入的外部资源（比如<frame>、<iframe>、<embed>和<applet>）
- **`connect-src`**：HTTP 连接（通过 XHR、WebSockets、EventSource等）
- **`worker-src`**：`worker`脚本
- **`manifest-src`**：manifest 文件
- `report-uri`:像目标主机报告注入行为