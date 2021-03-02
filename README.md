# All your Build Settings in `.xcconfig`!

Both of the projects here are standard created in Xcode 12.4 iOS Apps.

Based on `BuildSettings`, where all the Settings are left in the `BuildSettings.xcodeproj/projecrt.pbxproj`, I extracted those basic ones in 3 files for `ConfigBuildSettings`:

- [`Project.xcconfig`](ConfigBuildSettings/Xcode-Project.xcconfig) has all the common Build Settings
- [`Debug.xcconfig`](ConfigBuildSettings/Xcode-Debug.xcconfig) and [`Release.xcconfig`](ConfigBuildSettings/Xcode-Release.xcconfig) are importing the `Project` file and specifying others that are different

---
**WARNING**: You need to move away `INFOPLIST_FILE` and `DEVELOPMENT_ASSET_PATHS` or at least change it in the file!

Instead of `ConfigBuildSettings` as a Prefix you'd want (usually) the name of your app or wherever it is located!

You also need to change the value of `PRODUCT_BUNDLE_IDENTIFIER` — you might want to split that in different files/configurations.

---

 
Because you're most likely to create your own `.xcconfig` files which will inherit those, and I'd recommend calling them `Project`, `Debug`, `Release`, I prefixed those with `Xcode-` telling you it's the Xcode default.

**Beware** that it's not the default for iOS, which is [exactly the problem](https://twitter.com/baarde/status/1366744129540096007).

## PList language != CSF
If you ever do this yourself, beware that things like that in the `.pbxproj`:

```
LD_RUNPATH_SEARCH_PATHS = (
	$(inherited),
	@executable_path/Frameworks,
)
```

Becomes this in `.xcconfig`-land:

```
LD_RUNPATH_SEARCH_PATHS = $(inherited) @executable_path/Frameworks
```

This is because the [Configuration Settings File](https://help.apple.com/xcode/mac/11.4/#/dev745c5c974) format is _special_.

I also suggest read this [article at NSHipster](https://nshipster.com/xcconfig).