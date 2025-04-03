在Electron中，默认情况下，渲染进程的Node.js集成是禁用的，以提高安全性。如果你想在渲染进程中使用Node模块，有以下几种方法：

### 启用 `nodeIntegration`
在主进程中启用 `nodeIntegration`，允许渲染进程直接使用Node模块。

#### 主进程代码（main.js）
```javascript
const { app, BrowserWindow } = require('electron');

app.whenReady().then(() => {
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true, // 启用Node.js集成
    },
  });

  mainWindow.loadFile('index.html');
});
```

#### 渲染进程代码（index.html）
```html
<!DOCTYPE html>
<html>
<head>
  <title>Electron Node Integration Example</title>
</head>
<body>
  <h1>Electron Node Integration Example</h1>
  <script>
    const os = require('os');
    console.log(`Node.js Version: ${process.version}`);
    console.log(`Platform: ${os.platform()}`);
  </script>
</body>
</html>
```

### 使用预加载脚本（推荐）
通过预加载脚本，你可以安全地将特定的Node功能暴露给渲染进程。

#### 主进程代码（main.js）
```javascript
const { app, BrowserWindow } = require('electron');

app.whenReady().then(() => {
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: './preload.js', // 预加载脚本
      contextIsolation: true,
      nodeIntegration: false,
    },
  });

  mainWindow.loadFile('index.html');
});
```

#### 预加载脚本（preload.js）
```javascript
const { contextBridge, ipcRenderer } = require('electron');

contextBridge.exposeInMainWorld('nodeAPI', {
  getNodeVersion: () => process.version,
  getPlatform: () => require('os').platform(),
});
```

#### 渲染进程代码（index.html）
```html
<!DOCTYPE html>
<html>
<head>
  <title>Electron Preload Example</title>
</head>
<body>
  <h1>Electron Preload Example</h1>
  <script>
    console.log(`Node.js Version: ${window.nodeAPI.getNodeVersion()}`);
    console.log(`Platform: ${window.nodeAPI.getPlatform()}`);
  </script>
</body>
</html>
```

### 通过主进程代理
在渲染进程中，通过主进程代理来使用Node模块，这样可以保持渲染进程的隔离性。

#### 主进程代码（main.js）
```javascript
const { app, BrowserWindow, ipcMain } = require('electron');

app.whenReady().then(() => {
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: './preload.js',
      contextIsolation: true,
      nodeIntegration: false,
    },
  });

  mainWindow.loadFile('index.html');
});

ipcMain.handle('get-node-info', () => {
  return {
    nodeVersion: process.version,
    platform: require('os').platform(),
  };
});
```

#### 预加载脚本（preload.js）
```javascript
const { contextBridge, ipcRenderer } = require('electron');

contextBridge.exposeInMainWorld('nodeAPI', {
  async getNodeInfo() {
    return ipcRenderer.invoke('get-node-info');
  },
});
```

#### 渲染进程代码（index.html）
```html
<!DOCTYPE html>
<html>
<head>
  <title>Electron IPC Example</title>
</head>
<body>
  <h1>Electron IPC Example</h1>
  <script>
    (async () => {
      const nodeInfo = await window.nodeAPI.getNodeInfo();
      console.log(`Node.js Version: ${nodeInfo.nodeVersion}`);
      console.log(`Platform: ${nodeInfo.platform}`);
    })();
  </script>
</body>
</html>
```

### 总结
- **启用 `nodeIntegration`**：简单直接，但会降低安全性。
- **预加载脚本**：更安全，只暴露必要的Node功能。
- **通过主进程代理**：最安全，所有Node操作都在主进程中进行，渲染进程只是发送请求和接收结果。