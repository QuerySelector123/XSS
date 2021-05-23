# XSS
了解xss攻击
### 1.什么是 XSS 攻击

> 跨站脚本攻击（Cross Site Scipting） 本来是缩写为 css 但是和 层叠样式表 css 重叠了 所以脚本攻击缩写为 XSS

> 跨站脚本攻击的实质就是 攻击者在 web 页面中插入恶意的 script 代码 这个代码 可以是 js 脚本 css 样式 或者其他意料之外的代码 当用户浏览该页面时 就会被嵌入其中的 script 代码被执行 从而达到恶意攻击用户的目的 比如 读取 cookie session tokens 或者其他敏感的网站信息 对用户进行钓鱼

### 2.XSS 攻击的危害

- 通过 document.cookie 盗取 cookie 中的信息
- 使用 js 或 css 破坏页面的正常结构和样式
- 流量劫持 通过 window.location.href 定位到其他页面
- dos 攻击 利用客户端占用过多的服务器资源 从而让用户无法得到服务器响应
- 利用 iframe 、 frame 、XMLHttpRequest Flash 等方式
  利用被攻击用户的身份进行一些管理动作 发微博 加好友 发私信
- 控制企业数据 包含读取 篡改 添加删除 企业敏感数据的能力

### 3.攻击方式

- 3.1 反射型 XSS 攻击

通过 url 传递参数的功能
在用户进行网站搜索 跳转等
需要用户主动打开恶意的 url 才能生效
攻击者往往会结合多种诱导手段来诱导用户点击

- 3.2 存储型 XSS 攻击

恶意脚本永久存储在目标服务器上 当浏览器请求数据的时候 脚本从服务器传回并执行 影响范围比反射型和 dom 型 XSS 更大
常常冒充用户行为 调用目标接口执行攻击者的操作 如 发帖 商品评论 用户私信等

- 3.3 DOM 型 XSS

DOM 型 XSS 攻击 实际上 就是 前端 javascript 代码不够严谨 把不可信的内容插入到页面上 在使用

```
innerHTML outerHTML appendChild document.write() 等操作要小心 不要把不可信的数据插入到页面上
```

攻击者制造特殊数据 恶意窃取用户数据 冒充用户行为 取出和执行恶意代码有浏览器端完成 属于前端 JavaScript 自身的安全漏洞

### 防范策略

- 使用 HTTP-only cookie ：禁止 Javascipt 读取某些敏感 cookie
- 在服务器端设置
  Content-Security-Policy 头部来指定策略

* 或者在前端设置 meta 标签

```
Content-Security-Policy:default-src 'self'`请输入代码`

<meta http-equiv="Content-Security-Policy" content="form-action 'self';">
```
