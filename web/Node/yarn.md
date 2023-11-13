# yarn安装使用

**使用node安装**

```shell
npm install --global yarn
```

**查看yarn版本**

```shell
yarn --version
```

**初始化项目**

```shell
yarn init
```

**安装包**（根据项目中的 `package.json` 文件安装所有依赖包）

```shell
yarn install
```

**添加包**（默认加在生产环境）

```shell
yarn [global] add package-name@version [--save / -S]
```

**开发依赖**

```shell
yarn add package-name (--dev / -D)
```

**卸载包**

```shell
yarn remove package-name
```

**更新包**

```shell
yarn upgrade                                  // 将所有的依赖包更新到符合package.json文件中指定版本范围的最新版本
yarn upgrade package-name                     // 将特定包更新到符合package.json文件中指定版本范围的最新版本
yarn upgrade package-name@latest              // 将指定包更新至最新版本，并同步修改package.json文件
```

**查看指定包版本**

```shell
yarn info <package-name> version              // 查看指定包的版本
yarn info <package-name> versions             // 查看指定包的所有版本
```

