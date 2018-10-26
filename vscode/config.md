# how to 

read more at [react docs](https://facebook.github.io/create-react-app/docs/advanced-configuration) or [node docs](https://nodejs.org/api/modules.html#modules_loading_from_the_global_folders)

1. create `.env` in root directory
2. insert the line below

```
NODE_PATH=src/
```

# using absolute path via NODE_PATH from create-react-app

Create a `jsconfig.json` in the root of your project and use `baseUrl`

```json
{
    "compilerOptions": {
        "baseUrl": "./src"
    }
}
```

This should allow for imports such as:

```js
import SomeComponent from "components/somecomponent/SomeComponent"
```

Alternately, use the `paths` property:

```js
{
    "compilerOptions": {
        "baseUrl": ".",
        "paths": {
            "~/*": ["./src/*"]
        }
    }
}
```

this would allow imports of the form:

```js
import SomeComponent from "~/components/somecomponent/SomeComponent" // pay attension the path `~/`
```
