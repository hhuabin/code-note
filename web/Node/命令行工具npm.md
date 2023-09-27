查看node版本

```shell
node --version
```

查看全局包

```shell
npm list -g --depth 0
```

加入生产依赖

```shell
npm i 包名[@version] --save(-S) [-g]
```

加入开发依赖

```shell
npm i 包名[@version] --save-dev(-D)
```

生成报告

```shell
npm run build --report
```

查看包的当前版本号

```shell
npm view 包名 version
```

查看包的所有版本号

```shell
npm view 包名 versions
```

装最新版本的包

```shell
npm install <package-name>@latest
```

更新包

```shell
npm update                                 // 依据package.json进行更新，并同步更新package-lock.json文件
npm update <package-name>[@version]        // 更新指定包
```
