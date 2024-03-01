# Tailwind CSS 的语法规则

|Class|Properties|

## 动态类名

1. 变量类

   ```jsx
   export default function Button {
       const sizeClasses = "px-4 py-2 rounded-md text-base"
   
       return (
           <button type="button" className={`font-bold ${sizeClasses}`}>
               {children}
           </button>
       )
   }
   ```

2. 三目表达式

   ```jsx
   <div class="{{ error ? 'text-red-600' : 'text-green-600' }}"></div>
   ```



## width|height

### width

| Class    | Properties                         |
| -------- | ---------------------------------- |
| w-[16px] | width: 16px;                       |
| w-0      | width: 0px;                        |
| w-px     | width: 1px;                        |
| w-4      | width: 1rem;            /* 16px */ |
| w-auto   | width: auto;                       |
| w-1/2    | width: 50%;                        |
| w-1/4    | width: 25%;                        |
| w-3/4    | width: 75%;                        |
| w-full   | width: 100%;                       |
| w-screen | width: 100vw;                      |

`min-width`与`width`基本相同

| Class         | Properties        |
| ------------- | ----------------- |
| min-w-[220px] | min-width: 220px; |
| min-w-0       | min-width: 0px;   |
| min-w-full    | min-width: 100%;  |

`max-width`与`width`基本相同

| Class         | Properties        |
| ------------- | ----------------- |
| max-w-[220px] | max-width: 220px; |
| max-w-0       | max-width: 0px;   |
| max-w-full    | max-width: 100%;  |



### height

`height`与`width`基本相同

| Class    | Properties     |
| -------- | -------------- |
| h-[16px] | height: 16px;  |
| h-0      | height: 0px;   |
| h-px     | height: 1px;   |
| h-full   | height: 100%;  |
| h-screen | height: 100vh; |

`min-height`与`width`基本相同

| Class         | Properties         |
| ------------- | ------------------ |
| min-h-[220px] | min-height: 220px; |
| min-h-0       | min-height: 0px;   |
| min-h-full    | min-height: 100%;  |

`max-height`与`width`基本相同

| Class         | Properties         |
| ------------- | ------------------ |
| max-h-[220px] | max-height: 220px; |
| max-h-0       | max-height: 0px;   |
| max-h-full    | max-height: 100%;  |



### size

| Class       | Properties                                                   |
| :---------- | :----------------------------------------------------------- |
| size-[16px] | width: 16px;<br/>height: 16px;                               |
| size-0      | width: 0px;<br/>height: 0px;                                 |
| size-px     | width: 1px;<br />height: 1px;                                |
| size-4      | width: 1rem;      /* 16px \*/<br />height: 1rem;     /* 16px */ |
| size-1/2    | width: 50%;<br />height: 50%;                                |
| size-full   | width: 100%;<br />height: 100%;                              |



## padding | border | margin

### padding

| Class   | Properties                                                   |
| ------- | ------------------------------------------------------------ |
| p-[5px] | padding: 5px;                                                |
| p-0     | padding: 0px;                                                |
| px-0    | padding-left: 0px;<br />padding-right: 0px;                  |
| py-0    | padding-top: 0px;<br />padding-bottom: 0px;                  |
| pt-0    | padding-top: 0px;                                            |
| pr-0    | padding-right: 0px;                                          |
| pb-0    | padding-bottom: 0px;                                         |
| pl-0    | padding-left: 0px;                                           |
| p-px    | padding: 1px;                                                |
| px-px   | padding-left: 1px; padding-right: 1px;                       |
| p-4     | padding: 1rem;       /* 16px */                              |
| px-4    | padding-left: 1rem;         /* 16px */<br />padding-right: 1rem;      /\* 16px */ |



### margin

`margin`与`padding`基本相同

| Class   | Properties                                                   |
| ------- | ------------------------------------------------------------ |
| m-[5px] | margin: 5px;                                                 |
| m-0     | margin: 0px;                                                 |
| mx-0    | margin-left: 0px;<br />margin-right: 0px;                    |
| m-4     | margin: 1rem;                  /* 16px */                    |
| mx-4    | margin-left: 1rem;           /* 16px */<br />margin-right: 1rem;         /\* 16px */ |



### Space Between

子元素中间的间隔

- x：x轴方向上的间隔
- y：y轴方向上的间隔

| Class         | Properties                               |
| ------------- | ---------------------------------------- |
| space-y-[5px] | margin-top: 5px;                         |
| space-x-0 >   | margin-left: 0px;                        |
| space-y-0 >   | margin-top: 0px;                         |
| space-x-4 >   | margin-left: 1rem;            /* 16px */ |
| space-y-4 >   | margin-top: 1rem;            /* 16px */  |



### border

| Class | Properties |
| ----- | ---------- |
|       |            |

| Class | Properties |
| ----- | ---------- |
|       |            |



