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

