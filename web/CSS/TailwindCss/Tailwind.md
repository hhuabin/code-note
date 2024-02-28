# install

1. 安装`tailwindcss`，`postcss`

   ```bash
   npm install -D tailwindcss postcss autoprefixer
   
   npx tailwindcss init           // 在根目录生成 tailwind.config.js 文件
   npx tailwindcss init --esm     // 在根目录生成 tailwind.config.js 文件 ESM风格
   npx tailwindcss init --ts      // 在根目录生成 tailwind.config.ts 文件
   
   npx tailwindcss init -p        // 生成 postcss.config.js 配置文件
   ```

2. `tailwind.config.js`

   ```javascript
   module.exports = {
   	content: ['./src/**/*.{vue,js,ts,jsx,tsx}'],
   	theme: {
   		extend: {},
   	},
   	plugins: [],
   }
   ```

   ```javascript
   /** @type {import('tailwindcss').Config} */
   export default {
   	content: ['./src/**/*.{vue,js,ts,jsx,tsx}'],
   	theme: {
   		extend: {},
   	},
   	plugins: [],
   }
   ```

   ```typescript
   import type { Config } from 'tailwindcss'
   
   export default {
   	content: ['./src/**/*.{vue,js,ts,jsx,tsx}'],
   	theme: {
   		extend: {},
   	},
   	plugins: [],
   } satisfies Config
   ```

   

3. 配置`postcss.config.js`

   ```javascript
   module.exports = {
   	plugins: {
   		tailwindcss: {},
   		autoprefixer: {},
   	}
   }
   ```

4. 入口文件加入tailwindcss

   ```css
   /* tailwind.css */
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```

   ```tsx
   /* index.tsx */
   import ReactDOM from 'react-dom/client';
   
   import './styles/tailwind.css';
   ```



# tailwind.config.ts

## content

可以配置任何包含Tailwind类名的**文件的路径**

```typescript
import type { Config } from 'tailwindcss'

export default {
	content: [
		'./pages/**/*.{html,js}',
    	'./components/**/*.{html,js}',
	],
} satisfies Config
```



## theme

配置 color palette, fonts, type scale, border sizes, breakpoints 或者任何与网站设计相关的东西

```typescript
import type { Config } from 'tailwindcss'

export default {
	content: ['./src/**/*.{vue,js,ts,jsx,tsx}'],
	theme: {
		colors: {
			'blue': '#1fb6ff',
			'purple': '#7e5bef',
			'pink': '#ff49db',
			'orange': '#ff7849',
			'green': '#13ce66',
			'yellow': '#ffc82c',
			'gray-dark': '#273444',
			'gray': '#8492a6',
			'gray-light': '#d3dce6',
		},
		fontFamily: {
			sans: ['Graphik', 'sans-serif'],
			serif: ['Merriweather', 'serif'],
		},
		extend: {
			spacing: {
				'8xl': '96rem',
				'9xl': '128rem',
			},
			borderRadius: {
				'4xl': '2rem',
			}
		}
	},
	plugins: [],
} satisfies Config
```



## plugins

注册插件使用

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
    plugins: [
        require('@tailwindcss/forms'),
        require('@tailwindcss/aspect-ratio'),
        require('@tailwindcss/typography'),
        require('tailwindcss-children'),
    ],
}
```



## presets

预设部分允许您指定自己的自定义基本配置，而不是使用Tailwind的默认基本配置

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
    presets: [
    	require('@acmecorp/base-tailwind-config')
    ],
}
```



## prefix

公共前缀，解决应用样式的命名冲突问题

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
	prefix: 'tw-',
}
```

1. Tailwind生成的所有样式都会带有公共前缀，所以使用时，要带上公共前缀

   ```html
   <div class="tw-text-lg md:tw-text-xl tw-bg-red-500 hover:tw-bg-blue-500">
   	<!-- -->
   </div>
   ```

2. 负数的公共前缀要加在负号后面，如`class="-mt-8"`，写成如下

   ```html
   <div class="-tw-mt-8">
   	<!-- -->
   </div>
   ```

3. 公共前缀只会影响 Tailwind 的类，不会影响自己定义的类



## important

!不建议使用，全部样式加上`!important`

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
	important: true,
}
```



## separator

分隔符：`md`，`hover`，`focus`等，默认使用`:`

```html
<div class="md:tw-text-xl hover:tw-bg-blue-500">
	<!-- -->
</div>
```

但是如果模板语言中不支持类名中使用特殊语言，则可以更改它

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
	separator: '_',
}
```







# Tailwind CSS 的语法规则

