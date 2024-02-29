# Tailwind CSS 的语法规则



## 动态类名

1. 变量类

   ```jsx
   export default function Button {
       const sizeClasses = "px-4 py-2 rounded-md text-base"
   
       return (
           <button type="button" className={`font-bold ${sizeClasses}`}>
               {children}
           </button>
       )
   }
   ```

2. 三目表达式

   ```jsx
   <div class="{{ error ? 'text-red-600' : 'text-green-600' }}"></div>
   ```



# 

