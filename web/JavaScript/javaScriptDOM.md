# DOM

Document Object Model：文档对象模型 



# 查找HTML元素

1. 根据 **Id** 查找

   ```javascript
   document.getElementById()
   ```

2. 根据 **标签** 查找

   ```javascript
   document.getElementByTagName()
   ```

3. 根据 **类名** 查找

   ```javascript
   document.getElementByClassName()
   ```



# 改变HTML元素

1. innerHTML

   ```javascript
   element.innerHTML = "你好"
   ```



# HTML元素的增、删、改

1. createElement

   ```javascript
   document.createElement(element)
   ```

2. removeChild

   ```javascript
   document.removeChild(element)
   ```

3. appendChild

   ```javascript
   document.appendChild(element)
   ```

4. replaceChild

   ```javascript
   document.replaceChild(element)
   ```

5. write

   ```javascript
   document.write(text)
   ```



# 事件

1. onclick

   ```javascript
   document.getElementById().onclick = function() {}
   ```
   
2. 
