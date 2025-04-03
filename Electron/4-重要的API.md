正常情况下，nodemon只能监听JS文件的变化，监听不到HTML,CSS这些的变化，       
通过 ` npx nodemon --help ` 来查看信息

学习到了electron-in-state 这个包的使用用法      
`npm i electron-window-state -S ` S参数表示只安装到生产环境里面

坑 ,因为别人使用es6的Import导入，而你使用的是require导入，这个时候就需要一个default     




![bug](./img/1.png)
使用用法
```JS
const path = require('path')
const { app, BrowserWindow } = require('electron')
// 引入包
const windowStateKeeper = require('electron-window-state')

const createWindow = () => {
  // 初始化窗口状态管理器
  let state = windowStateKeeper({
    defaultWidth: 800,  // 默认宽度
    defaultHeight: 600 // 默认高度
  })

  const win = new BrowserWindow({
    x: state.x,         // 使用上次的X坐标
    y: state.y,         // 使用上次的Y坐标
    width: state.width, // 使用上次的宽度
    height: state.height,// 使用上次的高度
    webPreferences: {
      preload: path.resolve(__dirname, './preload.js')
    }
  })

  // 绑定窗口状态自动保存
  state.manage(win)
  
  win.loadFile('index.html')
}
```

meta 里面的 img-src 'self'   的含义，类似的还有哪些 img-src *

context-menu : 右键上下文信息   
可以用它来实现右键弹出保存图片的功能