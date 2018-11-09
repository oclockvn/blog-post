In `Application_Start` or `Startup`, config web api:

```cs
protected void Application_Start()
{
    // register filter
    System.Web.Http.GlobalConfiguration.Configure(WebApiConfig.Register); // config web api
    // register routes
    // ...
}
```

then, create `WebApiConfig.cs` which contains:

```cs
public class WebApiConfig
{
    public void Register(HttpConfiguration config)
    {
        var serializeSettings = config.Formatters.JsonFormatter.SerializerSettings;
        serializeSettings.Formatting = Formatting.Indented;
        serializeSettings.ContractResolver = new Newtonsoft.Json.Serialization.CamelCasePropertyNamesContractResolver();

        // map attributes
        // map routes
    }
}
```

after this, any responses from api will be camelCase:

```cs
// api

public object Test()
{
    return new { Name = "Foo", Price = 1000, ValueDescriptor = "Tester" };
}
```

will become:

```js
fetch('/api/test')
    .then(res => console.log(resp)); // { name: "Foo", price: 1000, valueDescriptior: "Tester" }
```