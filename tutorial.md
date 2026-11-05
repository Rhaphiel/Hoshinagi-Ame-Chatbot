在自己的电脑上搭建ChatBot教程
注意，部署在本地（区别于云端）时，只有电脑开机且未睡眠，并同时保持 QQ + SnowLuma + AstrBot 运行时，Bot才会运行

零 前置需求
1. DeepSeek：用于 Bot 的回复
2. AstrBot：掌管 Bot
3. SnowLuma：把 Bot 连接进 QQ
4. 闲置 QQ 号：充当 Bot


一 创建 API Key


1. 访问 https://platform.deepseek.com/
2. 注册并登录 DeepSeek
3. 充值点余额
4. 打开 https://platform.deepseek.com/api_keys
5. 点击创建 API Key
6. 复制生成的 Key，粘贴到记事本里保存
需要注意的是，这个 Key 通常只显示一次，不要透露给任何人


二 安装 AstrBot


1. 访问 https://github.com/AstrBotDevs/AstrBot-desktop/releases
2. 在最新版本的 Assets 里，下载 Windows 安装包并安装
3. 安装完成后，打开 AstrBot，也可以选择网页端访问 http://127.0.0.1:6185


三 将 DeepSeek 导入 AstrBot


1. 打开 AstrBot 管理页面
2. 在左边找到模型提供商
3. 找到“提供商源”，新增 DeepSeek
4. 填入刚才保存的 API Key。地址填 https://api.deepseek.com/v1，模型选择 deepseek-flash
5. 把这个模型设为默认聊天模型并保存


四 打开端口


1. 在 AstrBot 左边找到机器人
2. 点击“创建机器人”
3. 选择 OneBot v11
4. 按下面填写：
- ID：随便写一个
- 启用：选上
- 反向 WebSocket 主机地址：0.0.0.0
- 反向 WebSocket 端口：6199
- Token：空着
然后保存



五 安装 SnowLuma


1. 打开 https://snowluma.github.io/zh/docs/guide/deploy/windows
2. 在 GitHub Releases 下载 Windows 完整版，文件名类似 SnowLuma-版本号-win-x64.tar.gz
3. 解压到一个你能记住的地方，路径最好是全英文的
4. 登录 QQ 小号
5. 进入解压的地方，找到并启动 launcher.bat
6. 第一次启动时，控制台里会显示 SnowLuma 的临时密码
找到下面的内容：

临时密码
initial credentials
initial admin password

记下来，因为这个是初始密码，只会显示和可用一次


六 注入QQ

1. 访问 http://127.0.0.1:5099
2. 用临时密码登录
3. 如果 SnowLuma 提示登录 QQ，用手机 QQ 扫码登录小号
4. 他应该能自己找到 QQ 然后运行，如果没有的话，在 SnowLuma 页面里找 加载 QQ / 进程注入 的按钮，手动加载一次


七 让 SnowLuma 连接 AstrBot


1. 在 SnowLuma 页面里找到 节点配置 中的 WS 客户端
2. 新建一个 WebSocket 客户端。
3. 目标 URL 填 ws://127.0.0.1:6199/ws 并保存，AstrBot 的 Token 留空时，SnowLuma 的 Token 也留空；如果 AstrBot 设置过 Token，两边必须填写完全相同的值（没看懂这句话的话不用管，留空不填就对了）
5. 检查一下有没有连接好，去日志里看

wsclient-1
已连接

说明好了一半，然后去 AstrBot 的日志看

aiocqhttp(OneBot v11) 适配器已连接。

说明好了，这时候去给小号发一条消息，应该能收到回复

