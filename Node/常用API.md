以下是 Node.js 中一些常用的 API，它们通常用于获取系统信息、文件操作、网络请求等常见任务：

### **1. `process` 模块**
`process` 是 Node.js 的一个全局对象，提供了关于当前进程的信息和控制方法。
- **`process.platform`**：获取当前操作系统的平台（如 `'win32'`、`'darwin'`、`'linux'`）。
- **`process.version`**：获取当前 Node.js 的版本。
- **`process.memoryUsage()`**：获取当前进程的内存使用情况。
- **`process.argv`**：获取命令行参数。
- **`process.env`**：获取环境变量。
- **`process.exit(code)`**：退出当前进程。

### **2. `os` 模块**
`os` 模块提供了操作系统相关的实用工具。
- **`os.platform()`**：获取当前操作系统的平台。
- **`os.arch()`**：获取当前操作系统的架构（如 `'x64'`、`'arm64'`）。
- **`os.cpus()`**：获取 CPU 信息。
- **`os.freemem()`**：获取系统空闲内存。
- **`os.totalmem()`**：获取系统总内存。
- **`os.hostname()`**：获取主机名。

### **3. `fs` 模块**
`fs` 模块用于文件系统操作。
- **`fs.readFile(filename, [options], callback)`**：异步读取文件内容。
- **`fs.writeFile(filename, data, [options], callback)`**：异步写入文件内容。
- **`fs.readdir(path, [options], callback)`**：异步读取目录内容。
- **`fs.mkdir(path, [options], callback)`**：异步创建目录。
- **`fs.rmdir(path, [options], callback)`**：异步删除目录。
- **`fs.exists(path, callback)`**：检查文件或目录是否存在。

### **4. `path` 模块**
`path` 模块用于处理和转换文件路径。
- **`path.join(...paths)`**：连接路径片段。
- **`path.resolve(...paths)`**：将路径或路径片段解析为绝对路径。
- **`path.dirname(path)`**：返回路径的目录名。
- **`path.basename(path, [ext])`**：返回路径的最后一部分（文件名）。
- **`path.extname(path)`**：返回路径的扩展名。

### **5. `http` 和 `https` 模块**
`http` 和 `https` 模块用于创建 HTTP 和 HTTPS 服务器和客户端。
- **`http.createServer([requestListener])`**：创建 HTTP 服务器。
- **`http.request(options, [callback])`**：发送 HTTP 请求。
- **`https.createServer([options], [requestListener])`**：创建 HTTPS 服务器。

### **6. `child_process` 模块**
`child_process` 模块用于创建子进程。
- **`child_process.exec(command, [options], callback)`**：在 shell 中执行命令。
- **`child_process.spawn(command, [args], [options])`**：创建子进程。
- **`child_process.fork(modulePath, [args], [options])`**：创建子进程，并与父进程通信。

### **7. `util` 模块**
`util` 模块提供了一些实用工具函数。
- **`util.promisify(original)`**：将回调风格的函数转换为返回 Promise 的函数。
- **`util.types`**：提供类型检查函数。
- **`util.inspect(object, [options])`**：将对象转换为字符串表示。

### **8. `events` 模块**
`events` 模块用于创建和管理事件发射器。
- **`EventEmitter`**：事件发射器类，用于定义和监听事件。

### **9. `stream` 模块**
`stream` 模块用于处理流式数据。
- **`Readable`**：可读流。
- **`Writable`**：可写流。
- **`Duplex`**：双工流（同时可读可写）。
- **`Transform`**：转换流（用于数据转换）。

### **10. `url` 和 `querystring` 模块**
`url` 和 `querystring` 模块用于处理 URL 和查询字符串。
- **`url.parse(urlString, [parseQueryString], [slashesDenoteHost])`**：解析 URL。
- **`querystring.parse(str, [sep], [eq], [options])`**：解析查询字符串。

### **11. `crypto` 模块**
`crypto` 模块用于加密和解密操作。
- **`crypto.createHash(algorithm)`**：创建哈希摘要。
- **`crypto.createCipher(algorithm, password)`**：创建加密流。
- **`crypto.createDecipher(algorithm, password)`**：创建解密流。

这些 API 是 Node.js 中非常常用的工具，可以帮助你完成各种任务，从文件操作到网络请求，再到加密解密等。根据你的具体需求，选择合适的 API 来实现功能。