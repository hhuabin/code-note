**查看node版本**

```shell
node --version
```

**查看npm版本**

```shell
node --version
```

**初始化项目**

```shell
npm init
```

**查看全局包**

```shell
npm list -g --depth 0
```

**加入生产依赖**

```shell
npm i package-name[@version] --save(-S) [-g]
```

**加入开发依赖**

```shell
npm i package-name[@version] --save-dev(-D)
```

**生成报告**

```shell
npm run build --report
```

**查看包的当前版本号**

```shell
npm view package-name version
```

**查看包的所有版本号**

```shell
npm view package-name versions
```

**装最新版本的包**

```shell
npm install package-name@latest
```

**更新包**

```shell
npm update                                 // 依据package.json进行更新，并同步更新package-lock.json文件
npm update package-name                    // 将特定包更新到符合package.json文件中指定版本范围的最新版本
npm update package-name@latest             // 将指定包更新至最新版本，并同步修改package.json文件
npm update package-name[@version]        // 更新指定包
```
