# webpack.config.js

1. `@`设置为根路径 `src` 别名

   ```js
   alias: {
   	'@': path.resolve(__dirname, "..", 'src'), // 设置根目录路径
   },
   ```

2. 引入less，在rules下添加`less-loader`

   ```shell
   yarn add less-loader --dev
   yarn add css-loader style-loader -
   ```

   ```js
   module: {
       rules: [
           {
               oneOf: [
                   {
                       test: /\.less$/,
                       exclude: /\.module\.less$/,
                       use: getStyleLoaders({
                           importLoaders: 2,
                       }).concat({
                           loader: 'less-loader',
                       }),
                   },
                   {
                       test: /\.module\.less$/,
                       use: getStyleLoaders({
                           importLoaders: 2,
                           modules: {
                               getLocalIdent: getCSSModuleLocalIdent,
                           },
                       }).concat({
                           loader: 'less-loader',
                       }),
                   },
               ]
           }
       ]
   }
   ```

   