Develope process and process record
1. 配置npmrc
  Electron官方文档给出的方案，通过在.npmrc文件中配置相关环境变量，帮助npm在下载Native模块时，自动下载其对应的Electron版本。
  `npm config ls -l`
  .npmrc在不同系统下的路径不一样，通过上面的命令找到其位置，手动添加一下内容：
  ```// Electron
        target=1.7.11
        arch=x64
        target_arch=x64
        disturl=https://atom.io/download/electron
        runtime=electron
        build_from_source=true
      //target_platform=darwin
   ```
