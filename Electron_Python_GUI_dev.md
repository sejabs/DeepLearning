Develope process and process record
参考： `https://www.jianshu.com/p/513fc8e6f243`
1. 配置.npmrc
  Electron官方文档给出的方案，通过在.npmrc文件中配置相关环境变量，帮助npm在下载Native模块时，自动下载其对应的Electron版本。
  `npm config ls -l`
  .npmrc在不同系统下的路径不一样，通过上面的命令找到其位置，手动添加一下内容：
  ```
      // Electron
        target=1.7.11
        arch=x64
        target_arch=x64
        disturl=https://atom.io/download/electron
        runtime=electron
        build_from_source=true
      //target_platform=darwin
   ```
   target表示要编译的Electron版本，需要与你本地的Electron版本号一致。否则，可能会报错：
   ```
      'xx.node'
      was compiled against a different Node.js version using
      NODE_MODULE_VERSION 57. This version of Node.js requires
      NODE_MODULE_VERSION 54. Please try re-compiling or re-installing
   ```
   
2. 手动编译
  Nodejs的Native模块，其根目录下都有binding.gyp这个文件，这是Chromium团队为nodejs跨平台设计的一种文件。通过node-gyp或者node-pre-gyp等        nodejs命令工具，可以对Native模块进行重编译。
  `npm i -g node-gyp`
  使用node-gyp前，系统需要事先安装好以下环境：
  Windows:
    VS 2017
    python 2.7(3.x不支持)
  Ubuntu:
    C/C++工具，例如GCC
    python v2.7(3.x不支持)
  
  node-gyp手动编译Electron模块：
    `cd node_modules/addon`
    `node-gyp rebuild --target=1.7.11 --arch=x64 --target_platform=darwin --dist-url=https://atom.io/download/atom-shell`
  
  若配置过.npmrc，直接node-gyp rebuild即可。
  
  注意：简单的Native库，在配置了.npmrc后，能直接下载成功，得到需要的.node文件。也有部分库，除了Electron的Headers，还需要本地其它依赖的支持。例      如：canvas和sqlite3。


