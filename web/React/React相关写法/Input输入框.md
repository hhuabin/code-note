# Input输入格式控制

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



# 中文输入法事件

- `onCompositionStart`：用户开始使用输入法
- `onCompositionUpdate`：用户正在进行组合输入（例如输入拼音时）
- `onCompositionEnd`：用户完成组合输入，输入法提交内容

主要用于处理输入法开始组合输入的情况，比如中文拼音输入法的输入过程

```tsx
const Home: React.FC = () => {

    const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
        if (isComposition.current) return
        console.log("handleChange", event.target.value)
        setValue(event.target.value)
    }

    const handleCompositionStart = (event: React.CompositionEvent<HTMLInputElement>) => {
        console.log("handleCompositionStart", event)
        isComposition.current = true
    }

    const handleCompositionEnd = (event: React.CompositionEvent<HTMLInputElement>) => {
        isComposition.current = false
        console.log("handleCompositionEnd", event.currentTarget.value)
        setValue(event.currentTarget.value)
    }

    return (
        <input
            onChange={event => handleChange(event)}
            onCompositionStart={event => handleCompositionStart(event)}
            onCompositionEnd={event => handleCompositionEnd(event)}
            type="text"
        />
    )
}
```

用 `isComposition` 判定是否为输入法输入，是则不触发`setValue`