[craco官网](https://craco.js.org/docs/getting-started/ "craco")

```shell
yarn add @craco/craco --dev
```

```shell
npm install @craco/craco --save-dev
```

# webpack



## alias

- 配置 `@` 指向 `src` 目录

1. craco.config.ts

   ```typescript
   const path = require('path');
   
   module.exports = {
   	webpack: {
   		alias: {
   			'@': path.resolve(__dirname, 'src'), // 将 @ 符号指向 src 目录
   		},
   	},
   };
   ```

2. tsconfig.json

   ```typescript
   {
       "compilerOptions": {
           "baseUrl": "./",
           "paths": {
   			"@/*": ["src/*"]
           }
       }
   }
   ```

   

