# input输入格式控制

```tsx
const handleChangeIdNum = (event: React.ChangeEvent<HTMLInputElement>) => {
    const idNumValue = event.target.value
    const reg = /[0-9]+|X|x/ig
    const _idNum = idNumValue.match(reg)?.join('') || ''
    setIdNum(_idNum)
    idNumFormat(false, _idNum)
}
```

==Bug：当输入法是拼音的时候，`_idNum`的值是截取之后的数字(相较输入框，字符长度变小了)，但是输入框会记住已输入的拼音，从而拼音会覆盖数字的长度==