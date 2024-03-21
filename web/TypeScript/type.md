# 类型

- `{}`：object
- JSON：JSON
- 字符串对象： Record<string, string>



# 类型

- 类型断言

  ```typescript
  <string>someValue
  ```

  ```typescript
  someValue as string
  ```


- 数组类型

  ```typescript
  export type IAnswer = Array<{
  	readonly name: string;
  	readonly age: number;
  }>
  ```
  
  数组单个类型获取，注意这里不要使用 `lineGroup[0].items`
  
  ```typescript
  [] as typeof lineGroup[0]["items"]
  ```



# 接口

```typescript
interface ClockInterface {
    currentTime: Date;
}
```



# interface 和 type

1. **`interface`：**
   - 主要用于定义对象的结构，即属性和方法。
   - **支持继承，可以继承其他接口**。
   - **可以被类实现（implements）**。
   - 不能描述基本类型（例如：`number`，`string`）和联合类型（例如：`string | number`）
2. **`type`：**
   - 可以用来定义对象、联合类型、交叉类型等复杂类型。
   - **支持基本类型和联合类型**。
   - **不支持继承和实现**。

一般来说，如果你只需要描述对象的结构，官方推荐使用 `interface`。但如果你需要更复杂的类型定义，例如联合类型、交叉类型等，或者需要使用基本类型，那么就可以使用 `type`。在实际使用中，两者可以根据需求交替使用。



# 继承





# 泛型

1. 泛型接口

   ```typescript
   interface GenericIdentityFn<T> {
       (arg: T): T;
   }
   ```

2. 泛型类型

   ```typescript
   type Tree<T> = {
       value: T;
       left: Tree<T>;
       right: Tree<T>;
   }
   
   type Props<T extends OrderItem> = {
   	orders: Array<T>;
   }
   ```

   ```typescript
   export interface OrderItem {
   	readonly name: string;
   }
   
   type Props<T> = {
   	orders: Array<T>;
   }
   
   function OrderList<T extends OrderItem>(props: Props<T>) {
       
   }
   ```

   

3. 泛型函数

   ```typescript
   function identity<T>(arg: T): T {
       return arg;
   }
   ```

4. Map泛型

   ```typescript
   interface Map<T> {
       [key: string]: T;
   }
   ```

   

```typescript




let myIdentity: GenericIdentityFn<number> = identity;
```





