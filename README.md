# Ionic Package Hooks

The hooks in this repository are hooks that you can run during the packaging of
your app. Ionic Package uses Cordova, so these are just standard [Cordova
Hooks](http://cordova.apache.org/docs/en/edge/guide/appdev/hooks/index.html)
that we've selected/accepted.

To run these hooks in Ionic Package, just put a `<hook />` tag in your
`config.xml`, like this:

```xml
<hook type="after_prepare" src="package-hooks/add_platform_class.js" />
```

That's it! Package will run that hook on the server.

### Re-enable HTTP for iOS9

This is probably one of the main reasons you're here, so this is how you do
that:

* Put the following XML in your `config.xml`:

    ```xml
    <hook type="after_prepare" src="package-hooks/ios9_allow_http.sh" />
    ```
* That's it, actually. Run `ionic package build ios ...` again and your binary
  should allow HTTP.

### Hooks

These are the available hooks. The **type** is what you put in `type` of your
`<hook />` tag, unless you want to run the hook at a different stage (not
recommended). If you want a hook to run before another one, reorder the `<hook
/>` tags.

##### `add_platform_class.js`

* **author**: Ionic
* **usage**: `<hook type="after_prepare" src="package-hooks/add_platform_class.js" />`
* **function**: Adds the various platform CSS classes to the `<body>` tag of
  your app such as `platform-android`, `platform-ios`, etc.

##### `ios9_allow_http.sh`

* **author**: [@daruwanov](https://github.com/daruwanov)
* **usage**: `<hook type="after_prepare" src="package-hooks/ios9_allow_http.sh" />`
* **function**: Sets `NSAllowsArbitraryLoads` to true in your `.plist` file,
  allowing all regular HTTP connections in your app again for iOS9.

### Use these hooks locally

You don't need to download these hooks locally, but if you want to use them for
local builds, you can clone the repository within your Ionic App, and Cordova
should pick up your `<hook />` tags within `config.xml` automatically.

**Within your app directory**:
```bash
$ git clone https://github.com/driftyco/ionic-package-hooks.git ./package-hooks
```
