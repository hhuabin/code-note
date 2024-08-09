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



## 手写reduce

```javascript
Array.prototype.myReduce = function(callback, initValue) {
	let result = initValue ?? this[0]

	const startIndex = initValue === undefined ? 1 : 0
	
	for (let index = startIndex; index < this.length; index++) {
		result = callback(result, this[index], index)
	}

	console.log(result);

	return result
}

const arr = [1, 2, 3, 4]
arr.myReduce((prev, current, index) => {
	if (current % 2 === 0) {
		prev.push(current)
	}
	return prev
}, [])
```





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

一个新数组，每个元素都是回调函数的返回值

```javascript
map(callbackFn)
map(callbackFn, thisArg)
```

- callbackFn

  - element

    数组中当前正在处理的元素

  - index

    正在处理的元素在数组中的索引

  - array

    调用了 `map()` 的数组本身

- thisArg

  执行 `callbackFn` 时用作 `this` 的值

  



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



# match

`match()`方法检索字符串与[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_expressions)进行匹配的结果

参数：一个正则表达式对象或者任何具有 [`Symbol.match`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol/match) 方法的对象

返回值：一个 `Array`，其内容取决于是否存在全局（`g`）标志，如果没有匹配，则返回null

- 如果使用 `g` 标志，则将返回与完整正则表达式匹配的所有结果，但不会返回捕获组。
- 如果没有使用 `g` 标志，则只返回第一个完整匹配及其相关捕获组。在这种情况下，`match()` 方法将返回与 `RegExp.prototype.exec()`相同的结果（一个带有一些额外属性的数组）

```javascript
const paragraph = 'The quick brown fox jumps over the lazy dog. It barked.';
const regex = /[A-Z]/g;
const found = paragraph.match(regex);

console.log(found);
// Expected output: Array ["T", "I"]
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



# indexOf

```javascript
indexOf(searchElement)
indexOf(searchElement, [fromIndex])
```

- searchElement：数组中要查找的元素
- fromIndex
  - 默认为 0
  - 如果 `fromIndex < 0`，`frommindex=frommindex + array.length`
  - 如果 `fromIndex >= array.length`，数组不会继续搜索并返回 `-1`
- **返回值**：首个被找到的元素在数组中的索引位置；若没有找到则返回 **-1**
