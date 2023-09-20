<div align="center">

![QLite Image](./ico.ico)

# QLite

```
在VSCode中使用QQ，让你摸鱼工作两不误
```

</div>

## 特性

- 不在本地保存任何消息记录和图片
- 好友和群聊分组显示
- 新消息置顶显示
- 多账号快捷切换
- ~~登录验证信息自动抓取~~
- 简单直观的交互体验
- 与vscode保持一致的UI主题

## 使用说明

- 首次安装时侧边栏会出现一个QQ图标，点击图标即可启动扩展
- 登录界面  
  从侧边栏的图标进入，输入账号密码即可登录  
  登录可选项
  - 登录状态
  - 记住密码
  - 自动登录  
  *注：密码不是必填项，当使用此扩展登录过后会留下token记录，下次登录时即可免密登录*  
  首次登录可能要求滑动验证或设备验证，跟随引导操作即可
- 登录成功后登录界面会切换到消息列表
  - 消息（在线期间收到的新消息会在这里显示）  
    消息1 +2 （右边的数字为新消息条数）  
    消息2 +1  
    ...
  - 联系人
    - 好友（好友在这里显示）
      - 分组1 （好友分组）  
        好友1 （显示好友的昵称和头像）  
        ...
      - 分组2  
        好友2  
        ...
      - ...
    - 群聊 （群聊在这里显示）
      - 我创建的  
        群聊1  
        群聊2  
        ...
      - 我管理的  
        ...
      - 我加入的  
        ...
- 页面顶部有设置和搜索菜单
  - 搜索  
    支持搜索好友和群聊（不是在线搜索），可以搜索好友或群聊名或对方QQ号
  - 设置  
    - 账号管理  
      账号切换支持快捷切换在当前设备有登录记录的账号，也可以退出到登录界面输入新账号
    - 我的状态  
      支持切换的状态有：在线、Q我吧、离开、忙碌、请勿打扰、隐身
    - 编辑资料（受限于依赖库的功能，目前只能显示和修改以下资料）
      - 昵称
      - 性别
- 聊天页面
  - 融合`vscode`风格的组件库
  - 特殊类型的消息基本都用可点击的标签进行包装，点击时显示内容（摸鱼ing）
  - 目前可解析的消息类型：
    - [x] AT
    - [x] 表情
    - [x] 文件
    - [x] 图片
    - [ ] 闪照
    - [ ] 外部软件链接
    - [ ] 位置
    - [ ] 音乐分享
    - [x] 戳一戳
    - [ ] 回复消息
    - [ ] 转发消息
    - [ ] 魔法表情
    - [ ] 在线视频
    - [ ] 语音
  - 目前可发送的消息类型：
    - [x] AT
    - [x] 表情
    - [x] 表情包
    - [x] 文件
    - [ ] 戳一戳
    - [ ] 回复消息
    - [ ] 转发消息
    - [ ] 魔法表情

## 设置

本扩展可以在vscode的设置（`Ctrl+,`唤起）中修改以下内容：

- 登录协议
  - 可选项：`Android`（默认值），`aPad`，`Watch`，`iMac`，`iPad`，`old_Android`
  - 备注：非必要不建议修改此设置，若登录时出现`Error Code: 45`的错误信息请将此设置修改为`old_Android`并再次尝试

## 配置文件

本扩展生成的所有文件都存放在 `$HOME/.qlite` 目录下，目录结构如下：

```
.qlite
│  QQNumber_token
│  QQNumber_token
│  device.json
│  login-record.json
│  qrcode.png
└─image
```

- `QQNumber_token` 就是登录后生成的token信息，删除后就不能免密登录
- `device.json` 是登录QQ模拟的设备信息，由`icqq`自动生成
- `login-record.json` 包含登录过的登录选项和账号信息，通过此文件实现登录状态的记录和读取
  - **注意**：如果你使用的是账号密码登录，则你的账号密码将会以**明文**形式写入此文件，为了防止信息泄露，建议在下一次登录时移除密码，这样不会记录你的密码信息
- `qrcode.png` 是使用二维码登录时产生的临时文件，获取新的二维码时会将原文件覆盖
- `image` 文件夹是`icqq`登录后生成的缓存目录，默认不开启缓存，所以文件夹为空

组件相关配置文件在`.vscode/extentions/vi-brance.vscode-qlite-1.5.6/out`目录下：

```
.vscode/extentions/vi-brance.vscode-qlite-1.5.6/out
├── chat
│   ├──index.html
|   ├──script.js
|   └──style.css
├── login
│   ├──index.html
|   ├──script.js
|   └──style.css
├── condicon.css
├── ico.ico                            
├── codicon.ttf
└── extension.js
```

- `chat/style.css` 聊天界面参数配置
- `login/style.css` 登陆界面参数配置
- 待补充

### ~~摸鱼~~界面简化技巧

- 将ico.ico替换为其他矢量图标或删除。删除后左侧组件按钮隐身，需依靠记忆点击该位置（置于组件栏最下端即完美）
- 将`chat/style.css`中的头像隐藏：

```
.msg > .avatar {
  border: var(--avatar-border-width) solid;
  border-radius: 50%;
  height: var(--avatar-size);
  margin: var(--avatar-margin);
  width: var(--avatar-size);
  display: none;
}
```

- 将群头衔如“群主”和“管理员”称号隐藏：

```
.msg > .avatar {
  border: var(--avatar-border-width) solid;
  border-radius: 50%;
  height: var(--avatar-size);
  margin: var(--avatar-margin);
  width: var(--avatar-size);
  display: none;
}
```

- 将聊天框气泡隐藏：

```
.content {
  word-wrap: break-word;
  background-color: var(--vscode-input-background);
  border: 1px solid var(--vscode-input-border);
  border-radius: calc(var(--button-icon-corner-radius) * 2);
  line-height: 20px;
  padding: 4px 6px;
  position: relative;
  text-align: left;
  white-space: pre-wrap;
  word-break: break-all;
  border: none;
}
```

- 其他方式待补充

## 常见问题

- QQ日常折磨开发者，版本过低的警告时有发生，此问题由`icqq`处理，所以关于此问题的解决办法：
  1. 等待`icqq`更新修复
  2. 到`icqq`的 [repo](https://github.com/icqqjs/icqq) 查找相关issue解决
  3. ~~爆破腾讯大楼~~

## 发布历史

- 详细信息请参考 [CHANGELOG.md](./CHANGELOG.md) 文件

## 自行开发

此项目还在完善中，欢迎各位（特别是开发者大佬）提供开发建议或代码贡献！

此项目采用`npm`进行包管理，初次编译时请使用以下指令：
```
npm i
```

开发平台推荐`VSCode`~~（废话）~~，以下是该项目的基本说明：
- 使用`eslint`进行语法检查
- 使用`prettier`进行代码格式化
- 使用`webpack`进行代码编译
- 使用`vsce`进行扩展包装

如果有其他开发方面的疑惑可以提[issue](https://github.com/Vi-brance/vscode-qlite/issues/new)

## 致谢

- [vscode-qq](https://github.com/takayama-lily/vscode-qq) : 此扩展的前身，由于原作者 [takayama-lily](https://github.com/takayama-lily) 似乎不再维护，所以才有了这个项目，在此特别感谢！
- [icqq](https://github.com/icqqjs/icqq) : 此扩展实现的所有QQ功能都来自这个API库
