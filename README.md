# tempChat

一个基于 Node.js、Express 与 Socket.IO 技术栈，支持文件共享功能的即时通讯应用。

-----

## 功能特性

  * **实时文本消息**: 支持用户间发送与接收实时文本消息。
  * **文件上传与共享**: 允许用户上传文件，并向所有在线用户广播文件信息。
  * **用户加入通知**: 当新用户连接到服务时，向所有客户端广播通知。
  * **静态文件服务**: 通过 Express 框架提供前端静态资源和已上传文件的访问。

-----

## 技术栈

  * **后端**: Node.js, Express
  * **实时通信**: Socket.IO
  * **文件处理**: Multer

-----

## 部署与运行

请依照以下步骤在本地环境中部署并运行此项目。

### **1. 环境要求**

请确保运行环境中已安装 [Node.js](https://nodejs.org/) (建议版本 \>= 18.0)。

### **2. 安装依赖**

首先，克隆本项目仓库至本地。

```bash
git clone https://github.com/reuAC/tempChat.git
```

随后，进入项目目录并安装相关依赖。

```bash
cd tempChat
npm install
```

### **3. 启动服务**

执行以下命令以启动应用服务。

```bash
npm start
```

服务将会启动并监听 3000 端口，终端将显示以下信息：

```
正在监听 *:3000
```

启动后，即可通过浏览器访问 [http://localhost:3000](https://www.google.com/search?q=http://localhost:3000) 使用本应用。

-----

## 核心逻辑

### **HTTP 路由**

  * `POST /upload`
      * 此端点用于处理文件上传。
      * 该路由使用 Multer 中间件接收 `multipart/form-data` 格式的单个文件。
      * 文件将被存储至服务端的 `/uploads` 目录。
      * 上传成功后，服务器将通过 Socket.IO 向所有客户端广播 `file uploaded` 事件。

### **Socket.IO 事件**

服务端对以下事件进行监听和广播：

  * `connection`: 当一个新客户端成功建立连接时在服务端触发。
  * `disconnect`: 当一个客户端断开连接时在服务端触发。
  * `chat message`: 当接收到客户端的聊天消息时，将该消息广播至所有已连接的客户端。
  * `user joined`: 当有新用户加入时，将用户标识广播至所有客户端。
  * `file uploaded`: (由服务端发出) 当文件上传成功后，将文件信息广播至所有客户端。

-----

## 项目结构

```
/
├── public/         # 存放前端静态文件 (HTML, CSS, JS)
├── uploads/        # 默认的文件上传目录
├── package.json    # 项目依赖与脚本配置文件
└── server.js       # 应用主服务文件
```

-----

## 许可协议

本项目遵循 [MIT](https://opensource.org/licenses/MIT) 许可协议。
