# URL 引入

```typescript
const homeUrl = new URL('@/images/home-selected.png', import.meta.url).href;
(homeRef.value as HTMLImageElement).src = homeUrl;
```



# require 引入

```typescript
const image = require("@/images/sk-offiaccount.jpg")

<img src={image} alt="" />
```



# import引入

```tsx
import image from '../../static/image.png';

<img src={image} alt="" />
```



# input

```tsx
<input onChange={event => this.saveFormData('username',event) } type="text" value={username}/>
```

