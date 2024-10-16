# React



# Vue3

1. **`:deep()`**

   ```css
   :deep(.ant-picker) {
       width: 100%;
   
       .ant-picker-input, input {
           color: #FFF !important;
           font-size: 24px !important;
       }
   }
   ```

2. **`:where`**

   ```css
   :where(.ant-picker) {
       width: 100%;
   
       :where(.ant-picker-input, input) {
           color: #FFF !important;
           font-size: 24px !important;
       }
   }
   ```

   

   