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