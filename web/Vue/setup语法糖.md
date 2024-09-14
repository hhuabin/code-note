# setup

[官方文档的setup](https://cn.vuejs.org/api/sfc-script-setup.html "script-setup")

在Vue3中可以使用setup语法糖或者类似于Vue2的`export default`

```vue
<script setup lang="ts">

</script>
```

```vue
<script lang='ts'>
import { defineComponent } from 'vue';
export default defineComponent({
	name: '',
	setup() {
		
		return {}
	}
});
</script>
```



## setup区别

`expose`：用于在 `<script setup>` 语法糖中显式地暴露组件的内部状态和方法，使它们可以被父组件或外部代码访问。这个功能主要用于与外部组件或代码进行交互时，需要公开某些内部状态或方法的场景

使用`setup`语法糖后，`expose`默认是`{}`，即父组件无法访问字组件内部的方法及变量

而`export default`暴露的东西会非常多，不仅包括return返回的东西，还包含`$props`、`$refs`、`$watch`等非常多东西



## 自定义`expose`

1. 在`setup`语法糖中

   ```vue
   <script setup lang="ts">
   
   defineExpose({
       a,
       b
   })
   </script>
   ```

2. 在`export default`中

   ```vue
   <script lang='ts'>
   import { defineComponent } from 'vue';
   export default defineComponent({
   	name: '',
   	setup(props, { expose }) {
   		
           expose({
           	a,
               b
           })
   		return {}
   	}
   });
   </script>
   ```

   

## 更推荐使用setup

对于 `setup` 语法糖，Vue 编译器可以更好地进行静态分析和优化，减少运行时的开销

对于 `defineComponent`，虽然也有优化，但因为保留了选项式 API 的结构，可能在一些极端情况下（如深度优化和摇树优化）略逊色于 `setup` 语法糖



## 使用setup后

## defineProps() 和 defineEmits()

可以使用`defineProps()` 和 `defineEmits()`代替`props`和`emit`

```vue
<script setup>
const props = defineProps({
  foo: String
})

const emit = defineEmits(['change', 'delete'])

// setup 代码
</script>
```

其他用法请参考官方文档