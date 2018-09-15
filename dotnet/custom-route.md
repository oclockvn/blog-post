# Custom routes in asp.net mvc 5

Here I'll show you the new way to custom route via attribute (the old way is to register multiple `mapRoute`)

```cs
// RouteConfig.cs

public static void RegisterRoutes(RouteCollection routes)
{
    routes.IgnoreRoute("{resource}.axd/{*pathInfo}");
    routes.MapMvcAttributeRoutes(); // after the line above

    routes.MapRoute( /* your route here */ );
}
```

### Custom route for area

```cs
public static void RegisterRoutes(RouteCollection routes)
{
    routes.IgnoreRoute("{resource}.axd/{*pathInfo}");
    routes.MapMvcAttributeRoutes();

    // RegisterAllAreas must be called after MapMvcAttributeRoutes to achieve area custom route
    AreaRegistration.RegisterAllAreas();

    routes.MapRoute( /* your route here */ );
}
```

Of course you need to remove `RegisterAllAreas()` in your `global.asax` (if have)