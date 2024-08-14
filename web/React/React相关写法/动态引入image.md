# URL 引入

```typescript
const homeUrl = new URL('@/images/home-selected.png', import.meta.url).href;
(homeRef.value as HTMLImageElement).src = homeUrl;
```

```typescript
import image from '../../static/image.png';

<img src={image} alt="" />
```



# require 引入

```typescript
const image = require("@/images/sk-offiaccount.jpg")

<img src={image} alt="" />
```



# import引入

```tsx
import React, { useState, useEffect } from 'react';

function MyComponent() {
    const [image, setImage] = useState(null);

    useEffect(() => {
        import('./path/to/image.jpg').then(img => {
        	setImage(img.default);
    	});
    }, []);

    if (!image) return <p>Loading...</p>;

    return <img src={image} alt="description" />;
}
```





# input

```tsx
<input onChange={event => this.saveFormData('username',event) } type="text" value={username}/>
```

