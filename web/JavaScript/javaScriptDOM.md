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




# 元素尺寸属性和滚动位置属性

**`pageX` 和 `pageY`**：表示鼠标或触摸位置相对于整个**页面**的位置

**`clientHeight`** 和 **`clientWidth`**：表示元素的**可视区域**高度和宽度，包括内边距，但不包括边框和外边距

**`offsetHeight`** 和 **`offsetWidth`**：表示元素的**总**高度和总宽度，包括内边距和边框，但不包括外边距

**`scrollTop`** 和 **`scrollLeft`**：表示元素的垂直和水平**滚动**位置

**`scrollHeight`** 和 **`scrollWidth`**：表示元素内容的**总**高度和总宽度，包括溢出部分

---

1. pageY

   **描述**：`pageY` 是一个表示鼠标事件或触摸事件的 Y 坐标（垂直位置），它相对于文档的顶部

   ```javascript
   document.addEventListener('click', (event) => {
   	console.log(event.pageY); // 输出鼠标点击位置相对于页面顶部的垂直距离
   });
   ```

2. clientHeight

   `clientY` 是一个表示鼠标事件或触摸事件的 Y 坐标（垂直位置），它相对于浏览器视口的顶部

   ```javascript
   document.addEventListener('click', (event) => {
   	console.log(event.clientY); // 输出鼠标点击位置相对于视口顶部的垂直距离
   });
   ```

3. offsetHeight

   `offsetY` 是一个表示鼠标事件的 Y 坐标（垂直位置），它相对于事件目标元素的顶部边界

   用于确定鼠标或触摸位置相对于事件目标元素的垂直距离

   ```javascript
   document.getElementById('myElement').addEventListener('click', (event) => {
   	console.log(event.offsetY); // 输出鼠标点击位置相对于元素顶部的垂直距离
   });
   ```

4. scrollTop

   `scrollTop` 是一个属性，表示元素滚动条向下滚动的像素数

   用于获取或设置元素的垂直滚动偏移量，常用于滚动事件处理和懒加载等场景

   ```javascript
   const element = document.getElementById('scrollableDiv');
   console.log(element.scrollTop); // 输出滚动条距元素顶部的距离
   
   // 设置滚动条位置
   element.scrollTop = 100;
   ```

5. scrollHeight

   `scrollHeight` 是一个属性，表示元素内容的总高度（包括溢出部分）

   用于获取元素内容的实际高度，即使该内容不可见（如被滚动条遮挡）

   ```javascript
   const element = document.getElementById('scrollableDiv');
   
   console.log(element.scrollHeight); // 输出元素的内容总高度
   ```

---

## 元素滚动触底的计算公式

```javascript
scrollTop + clientHeight >= scrollHeight
```

```jsx
import React, { useEffect, useRef, useCallback } from 'react';

const ScrollComponent = () => {
    const scrollableRef = useRef(null);

    const debounce = (func, delay) => {
        let timeout;
        return (...args) => {
            if (timeout) clearTimeout(timeout);
            timeout = setTimeout(() => {
            	func.apply(this, args);
            }, delay);
        };
    };

    const handleScroll = useCallback(
        debounce(() => {
            const element = scrollableRef.current;
            const { scrollTop, clientHeight, scrollHeight } = element;

            if (scrollTop + clientHeight >= scrollHeight) {
            	console.log('Reached the bottom!');
            }
        }, 200),
        []
    );

    useEffect(() => {
        const element = scrollableRef.current;
        // 本质还是使用监听
        element.addEventListener('scroll', handleScroll);
        
        return () => {
        	element.removeEventListener('scroll', handleScroll);
        };
    }, [handleScroll]);

    return (
        <div
            ref={scrollableRef}
            style={{ height: '200px', overflowY: 'auto', border: '1px solid #ddd' }}
        >
            <div style={{ height: '800px' }}>Scrollable Content</div>
        </div>
    );
};

export default ScrollComponent;
```



**也可以使用` IntersectionObserver `解决滚动触底问题**

`IntersectionObserver` 可以检测某个元素是否进入或离开视口或另一个元素的边界。通过使用它，可以检测页面底部的一个 "触底触发器" 元素何时进入视口，来判断滚动是否到底部

```jsx
import React, { useEffect, useRef, useState } from 'react';

const ScrollComponent = () => {
    const scrollableRef = useRef(null);
    const [isBottom, setIsBottom] = useState(false); // 状态管理是否到达底部

    useEffect(() => {
        const observer = new IntersectionObserver(
            ([entry]) => {
                // 当触底元素进入视口时，entry.isIntersecting 为 true
                if (entry.isIntersecting) {
                    setIsBottom(true);
                    console.log('Reached the bottom!');
                    // 执行触底时的逻辑，比如加载更多数据
                } else {
                    setIsBottom(false);
            	}
            },
            {
                root: scrollableRef.current, // 监视的滚动容器
                rootMargin: '0px',
                threshold: 1.0, // 触发的阈值（1.0 表示完全进入视口时触发）
            }
        );

        // 创建触底触发器元素
        const bottomElement = document.createElement('div');
        bottomElement.style.height = '1px';
        bottomElement.style.width = '100%';
        scrollableRef.current.appendChild(bottomElement);

        // 监视触底触发器元素
        observer.observe(bottomElement);

    	// 清理：在组件卸载时断开观察和删除触底元素
        return () => {
        	observer.disconnect();
            scrollableRef.current.removeChild(bottomElement);
        };
    }, []);

    return (
        <div
            ref={scrollableRef}
            style={{ height: '200px', overflowY: 'auto', border: '1px solid #ddd' }}
        >
            {/* 长内容以产生滚动条 */}
            <div style={{ height: '800px' }}>Scrollable Content</div>
        </div>
    );
};

export default ScrollComponent;
```

