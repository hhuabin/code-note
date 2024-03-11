# grid

当 HTML 元素的 `display` 属性设置为 `grid` 或 `inline-grid` 时，它就会成为网格容器

```css
.grid-container {
	display: grid;
    // display: inline-grid;
}
```

- `grid-column-gap`：网格列间隙

  ```css
  .grid-container {
      display: grid;
      grid-column-gap: 50px;
  }
  ```

- `grid-row-gap`：网格行间隙

  ```css
  .grid-container {
      display: grid;
      grid-row-gap: 50px;
  }
  ```

- `grid-gap`：`grid-column-gap`和`grid-row-gap`的简写

  ```css
  .grid-container {
      display: grid;
      grid-gap: 50px 100px;
  }
  
  // 或者
  .grid-container {
      display: grid;
      grid-gap: 50px;
  }
  ```

   

# grid-template-columns | grid-template-rows

## grid-template-columns

grid模板列

fr：浮动宽度

1. 指定列数，及列宽度

   ```css
   // 两列，每列宽100px
   grid-template-columns: 100px 100px;
   
   // 三列，每列宽100px
   grid-template-columns: 100px 100px 100px;
   
   // 三列，每列等宽
   grid-template-columns: 1fr 1fr 1fr;
   
   // 三列，中间列占比50%
   grid-template-columns: 1fr 2fr 1fr;
   ```

2. repeat函数

   ```css
   // 两列，每列等宽
   grid-template-columns: repeat(2, 1fr);
   ```

3. 自动布局

   ```css
   // 最小宽100px, 最大1fr
   // 以最小100px尽可能的向上布局
   grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
   ```

   

## grid-template-rows

grid模板行高



## grid-auto-rows

grid-template-rows未指定的行高

```css
// 第一、二行高100px，第三行及以后高200px
.grid-container {
    display: grid;
    grid-template-rows: 100px 100px;
    grid-auto-rows: 200px;
}
```



# 网格占比

```css
// 从第一列开始，第三列结束
grid-column-start: 1;
grid-column-end: 3;

// 简写
grid-column: 1 / 3;
```

```css
// 从第一行开始，第三行结束
grid-rows-start: 1;
grid-rows-end: 3;

// 简写
grid-rows: 1 / 3;
```

