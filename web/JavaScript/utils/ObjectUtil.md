# 深复制

1. **递归方法**

   ```typescript
   const deepCopy = <T>(obj: T): T => {
   	if (obj === null || typeof obj !== 'object') {
   		return obj;
   	}
   
   	const copy = (Array.isArray(obj) ? [] : {}) as T;
   	
   	for (const key in obj) {
   		if (obj.hasOwnProperty(key)) {
   			copy[key] = deepCopy(obj[key]);
   		}
   	}
   
   	return copy;
   }
   ```

2. **JSON方法：**

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
			return obj;
		}
	
		const copy = (Array.isArray(obj) ? [] : {}) as T;
		
		for (const key in obj) {
			if (obj.hasOwnProperty(key)) {
				copy[key] = FunctionUtil.deepCopy(obj[key]);
			}
		}
	
		return copy;
	}

	/**
	 * JSON深复制
	 * @param obj T
	 * @returns T
	 */
	public static deepCopyWithJSON = <T>(obj: T): T => {

		return JSON.parse(JSON.stringify(obj));

	}
}
```



