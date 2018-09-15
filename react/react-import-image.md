# Adding Images, Fonts, and Files

Read the doc at [create-react-app Adding Images, Fonts, and Files](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-images-fonts-and-files)

> In order to be able to import images into React components, you have to make sure that locally the images reside within the same parent directory as the components OR that the images are exported from the directory they reside in so they can be imported into any of your components.

So that if your images do not in same dir with component, make sure you export them

```js
// images.js 

export image from './image.png';
export image2 from './sub/image2.png';
```

then import in your component

```js
// component.js

import { image } from './images'
```

If these above not work for you, then you may need this trick: urlHelper and process.env (more about process env available [here](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-custom-environment-variables))

```js
// helper.js

export const urlContent = (path) => {
    return process.env.NODE_ENV === 'production' ? ('/app/build' + path) : path;
}
```

use url helper in your component

```js
import { urlContent } from './helper';
import image from './image.png';

const imageUrl = urlContent(image); // <- correct path
```