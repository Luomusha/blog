# 整合Electron和Next.js

Electron框架简述：能给nodejs项目加壳成为desktop的框架
Next.js：目前最流行的react服务端渲染框架

## Electron

- Electron提供了nodejs运行环境
- Electron程序会寻找`main.js`座位程序入口
- Electron程序在Windows平台打包会安装 `/Users/username/AppData/Local` 里面也就是Chrome的存储空间，这里放应用不需要特殊权限等好处。
- Electron可以手动打包成绿色软件

## Next.js

- Next.js官方提供的脚手架在package.json中创建的start命令为`next start`
- Next.js build打包脚本输出的内容默认在工程目录的`.next`目录下
- Next.js可以在next.config.js中设置打包输出目录
- Next.js可以在next.config.js中设置standalone打包方式
- Next.js的standalone打包方式默认输出内容在`.next`目录下的standalone目录中——即此目录即位一个完整、可运行的服务器
- 把static文件夹粘贴到了`.next`文件夹下
- Next.js的standalone打包方式会精简node_module中的内容，目录结构仍然为node_module输出在standalone目录中
- Next.js在build安装包的入口是server.js

## 整合Electron和Next.js
1. 手动build next.js
2. 下载electron的pre-build包
3. 将standalone安装包copy到`electron/resources/app`目录下
4. 修改server.js -> main.js
5. 编辑main.js，在里面开启electron BrwswerWindow窗口并load url `http://localhost:3000`
6. 注意启动顺序，需要等next的server启动完毕后再加载localhost:3000页面。否则容易加载不到静态资源。
7. zip压缩electron目录。然后我们得到了一个绿色软件。


示例main.js代码

```javascript

// process.env.NODE_ENV = 'production'
process.chdir(__dirname)
const NextServer = require('next/dist/server/next-server').default
const http = require('http')
const path = require('path')
const { app, BrowserWindow } = require('electron')

// Make sure commands gracefully respect termination signals (e.g. from Docker)
// Allow the graceful termination to be manually configurable
if (!process.env.NEXT_MANUAL_SIG_HANDLE) {
  process.on('SIGTERM', () => process.exit(0))
  process.on('SIGINT', () => process.exit(0))
}

let handler

const server = http.createServer(async (req, res) => {
  try {
    await handler(req, res)
  } catch (err) {
    console.error(err);
    res.statusCode = 500
    res.end('internal server error')
  }
})
const currentPort = parseInt(process.env.PORT, 10) || 3000

server.listen(currentPort, (err) => {
  if (err) {
    console.error("Failed to start server", err)
    process.exit(1)
  }
  const nextServer = new NextServer({
    hostname: 'localhost',
    port: currentPort,
    dir: path.join(__dirname),
    dev: false,
    customServer: false,
    conf: {"env":{},"webpack":null,"webpackDevMiddleware":null,"eslint":{"ignoreDuringBuilds":false},"typescript":{"ignoreBuildErrors":false,"tsconfigPath":"tsconfig.json"},"distDir":"./.next","cleanDistDir":true,"assetPrefix":"","configOrigin":"next.config.js","useFileSystemPublicRoutes":true,"generateEtags":true,"pageExtensions":["tsx","ts","jsx","js"],"target":"server","poweredByHeader":true,"compress":true,"analyticsId":"","images":{"deviceSizes":[640,750,828,1080,1200,1920,2048,3840],"imageSizes":[16,32,48,64,96,128,256,384],"path":"/_next/image","loader":"default","domains":[],"disableStaticImages":false,"minimumCacheTTL":60,"formats":["image/webp"],"dangerouslyAllowSVG":false,"contentSecurityPolicy":"script-src 'none'; frame-src 'none'; sandbox;","remotePatterns":[{"protocol":"http","hostname":"69.231.140.26","port":"8899","pathname":"**/**"}]},"devIndicators":{"buildActivity":true,"buildActivityPosition":"bottom-right"},"onDemandEntries":{"maxInactiveAge":15000,"pagesBufferLength":2},"amp":{"canonicalBase":""},"basePath":"","sassOptions":{},"trailingSlash":false,"i18n":null,"productionBrowserSourceMaps":false,"optimizeFonts":true,"excludeDefaultMomentLocales":true,"serverRuntimeConfig":{"twainClient":{}},"publicRuntimeConfig":{},"reactStrictMode":false,"httpAgentOptions":{"keepAlive":true},"outputFileTracing":true,"staticPageGenerationTimeout":60,"swcMinify":false,"output":"standalone","experimental":{"manualClientBasePath":false,"legacyBrowsers":true,"browsersListForSwc":false,"newNextLinkBehavior":false,"cpus":7,"sharedPool":true,"profiling":false,"isrFlushToDisk":true,"workerThreads":false,"pageEnv":false,"optimizeCss":false,"nextScriptWorkers":false,"scrollRestoration":false,"externalDir":false,"disableOptimizedLoading":false,"gzipSize":true,"swcFileReading":true,"craCompat":false,"esmExternals":true,"appDir":false,"isrMemoryCacheSize":52428800,"serverComponents":false,"fullySpecified":false,"outputFileTracingRoot":"","images":{"remotePatterns":[]},"swcTraceProfiling":false,"forceSwcTransforms":false,"largePageDataBytes":128000,"trustHostHeader":false},"configFileName":"next.config.js"},
  })
  handler = nextServer.getRequestHandler()

  console.log("Listening on port", currentPort)
})



app
  .whenReady()
  .then(() => {
    const win = new BrowserWindow({
      width: 1440,
      height: 880,
      minHeight: 880,
      minWidth: 1440,
      webPreferences: {
        nodeIntegration: true,
        contextIsolation: false,
        devTools: true,
      },
    })

    // win.loadURL('http://127.0.0.1:3000')
    win.loadURL('http://localhost:3000')
  })

```
