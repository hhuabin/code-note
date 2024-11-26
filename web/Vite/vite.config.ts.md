# UserConfig

```typescript
import { defineConfig } from 'vite'
import type { ConfigEnv } from 'vite'

export default defineConfig((env: ConfigEnv) => ({
    base: './',
}))
```



## resolve

```typescript
resolve: {
    alias: { '@': new URL('./src', import.meta.url).pathname },
},
```



## server

**`server`仅在开发环境有效**，所以尽情配置吧

```typescript
server: {
    port: 3000,
    open: true,
    headers: {
        'cache-control': 'no-cache, no-store, must-revalidate',   // 禁止缓存
        // 'cache-control': 'public, max-age=30, immutable',         // 缓存 3600s
        // 'last-modified': '',  // 禁止协商缓存
        // 'etag': '',           // 禁止协商缓存
    },
},
```



## build



### rollupOptions（[rollupOptions](./rollupOptions.md)）



#### external

用来指定哪些模块不应该被打包到最终的产物中，而是**保留为外部依赖**

```typescript
external: ['react', 'react-dom'],
```



