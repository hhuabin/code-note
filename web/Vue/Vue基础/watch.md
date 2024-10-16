# watch

1. 监视指定的数据，监视多个数据使用`[]`，如`[user, name]`

   ```javascript
   watch(
       user,
       (newValue, oldValue) => {
       	console.log(newValue, oldValue)
       },
       { immediate: true, deep: true }
   )
   ```

   immediate 默认会执行一次watch，deep 深度监视

2. `watchEffect`不需要配置immediate，本身默认就会进行监视,(默认执行一次)

   ```javascript
   watchEffect(() => {
       console.log(user)
   })
   ```

3. 使用watch监视非响应式的数据需要使用函数

   ```javascript
   watch([()=>user.firstName, ()=>user.lastName, fullName3], () => {
   	console.log('====')
   })
   ```



# 停止监视

`watch`会返回一个函数，执行函数即可

```javascript
const stopWatch = watch(
    age,
    (newValue, oldValue) => {
    	console.log(newValue, oldValue)
        if(age > 10) stopWatch()
    },
    { immediate: true, deep: true }
)
```

