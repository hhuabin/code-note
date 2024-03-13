# reduce

将其结果汇总为单个返回值

reduce方法可做的事情特别多，就是循环遍历能做的，reduce都可以做，比如数组求和、数组求积、数组中元素出现的次数、数组去重等等

```javascript
arr.reduce(function(preview,current,index,arr){
	return init + preview
}, init);
```

- prev 必需。累计器累计回调的返回值; 表示上一次调用回调时的返回值，或者初始值 init;
- current 必需。表示当前正在处理的数组元素；
- index 可选。表示当前正在处理的数组元素的索引，若提供 init 值，则起始索引为- 0，否则起始索引为1；
- arr 可选。表示原数组；
- init 可选。表示初始值。



# forEach

- 返回值：`undefined`

- 不会改变原数组基本类型的值，但引用数据类型会改变



# join

**Array -> String**

- 将数组中的所有元素放到字符串，参数是字符串的分隔符

```javascript
[1, 2, 3].join(',')    // 1,2,3
```



# filter

返回一个数组，里面包含符合条件的元素



# map

返回一个新数组，数组中的元素是原始数组的元素调用函数之后处理的值



# find

用于查找满足指定测试函数的第一个元素。如果找到了，它返回数组中**第一个**满足测试函数的元素的值；否则，返回 `undefined`

```javascript
array.find(function(element, index, array) {
  // 返回一个测试条件为真的元素
}, thisArg);
```

- `element`: 当前正在处理的元素。
- `index`（可选）: 当前正在处理的元素的索引。
- `array`（可选）: 调用 `find` 的数组。
- `thisArg`（可选）: 执行回调时的 `this` 值。

```javascript
let numbers = [1, 2, 3, 4, 5];
let even = numbers.find(function(element) {
  return element % 2 === 0;
});

console.log(even); // 输出: 2，因为它是数组中第一个偶数
```



# sort

`Array.prototype.sort()`

1. 升序

   ```javascript
   const numbers = [4, 2, 8, 1, 6];
   numbers.sort((a, b) => a - b);
   console.log(numbers); // 输出: [1, 2, 4, 6, 8]
   ```

2. 降序

   ```javascript
   const numbers = [4, 2, 8, 1, 6];
   numbers.sort((a, b) => b - a); // 降序排序
   console.log(numbers); // 输出: [8, 6, 4, 2, 1]
   ```

