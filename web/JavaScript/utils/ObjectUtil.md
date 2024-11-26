# 深复制

1. **递归方法**

   ```typescript
   const deepCopy = <T>(obj: T): T => {
       if (obj === null || typeof obj !== 'object') {
           return obj
       }
   
       const copy = (Array.isArray(obj) ? [] : {}) as T
   
       for (const key in obj) {
           // 判断是否是对象本身的属性而不是继承属性，如 toString() 等
           if (obj.hasOwnProperty(key)) {
               copy[key] = deepCopy(obj[key])
           }
       }
   
       return copy
   }
   ```

2. **JSON方法：**

   缺点：

   1. **无法复制函数、正则表达式和特殊对象**
   2. **循环引用问题**
   3. **性能问题**
   4. **丢失对象的原型链信息**

   ```typescript
   const deepCopyWithJSON = <T>(obj: T): T => {
   
       return JSON.parse(JSON.stringify(obj));
   
   }
   ```





```typescript
export default class FunctionUtil {

    /**
     * 深复制函数
     * @param obj T
     * @returns T
     */
    public static deepCopy = <T>(obj: T): T => {
        if (obj === null || typeof obj !== 'object') {
            return obj
        }

        const copy = (Array.isArray(obj) ? [] : {}) as T

        for (const key in obj) {
            if (obj.hasOwnProperty(key)) {
                copy[key] = FunctionUtil.deepCopy(obj[key])
            }
        }

        return copy
    }

    /**
     * JSON深复制
     * @param obj T
     * @returns T
     */
    public static deepCopyWithJSON = <T>(obj: T): T => {

        return JSON.parse(JSON.stringify(obj))

    }
}
```



