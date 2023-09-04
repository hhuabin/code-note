# indexOf

1. 查找字符串中某一字符从头开始第一次出现的索引，没有返回 -1

```javascript
const str = "Hello world!"
console.log(str.indexOf("o")) //4
```

2. 查找字符串中某一字符从指定位置开始第一次出现的索引，没有返回 -1

```javascript
c str = "Hello world! wo shi ooo"
console.log(str.indexOf("o",8)) //14
```



# slice

`slice()` **不会修改原始数组**，而是返回一个新数组，其中包含从原始数组中切片选取的元素

1. 基础用法，start、end可以是负数，负数从末尾开始算

   ```javascript
   array.slice(start[, end])
   ```

2. 只接受一个start参数

   ```javascript
   "abcd".slice(-2)       // cd
   ```

   



# splice

用于**修改数组**，可以实现删除、插入和替换数组中的元素，**返回一个包含被删除元素的数组**（如果有）。**原始数组将会被修改**。

1. 基础用法

   ```javascript
   array.splice(start, deleteCount, item1, item2, ...);
   ```

   - `start`：必需，表示开始修改的索引位置。
   - `deleteCount`：可选，表示要删除的元素个数。如果省略或为 0，将不删除任何元素。
   - `item1, item2, ...`：可选，要添加到数组的新元素。如果省略，则仅进行删除操作。
