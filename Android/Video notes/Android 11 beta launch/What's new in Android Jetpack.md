# What's new in Android

Notes on [What's new in Android Jetpack](https://www.youtube.com/watch?v=R3caBPj-6Sg&feature=youtu.be)

## Hilt 

Opinionated DI library specifically built for Android on top of Dagger.

Provide `@AndroidEntryPoint` to make Activity, Fragment, Service Injectable. 

Also ViewModel can be injected by annotating it with `@ViewModelInject`.

`@InstallIn` installs annotated module in a component.

Recomended because:
* Built on Dagger
* Jatpack Integrations
* Scopes for Android 
* Testing APIs
* Studio Integration

## App Startup

Content providers take at least 2ms to initialize on Pixel.
Libraries like WorkManager initiallizes a Content Provider at startup.

This library provides a way to share the same content provider.

WorkManager Initilizer example:
```kotlin
class WorkManagerInitializer: Initializer<WorkManager> {

    override fun create(context: Context): WorkManager {
        val configuration = Configuration.Builder()
            .setMinimumLoggingLevel(Log.DEBUG)
            .build()

            WorkManager.initialize(context, configuration)
            return WorkManager.getInstance(context)
    }

    override fun dependencies(): List<Class<out Initializer<*>>> = emptyList()
}

```

App Startup:
* Can be used both by App & Library Developers
* Optional Lazy initialization
* Autoimatically added Trace points


## Android Game SDK

Contains: 
* Frame pacing API
* Performance Tuner

## Benchmark 1.1
* Support for CPU profiling benchmarks and integration with Android Studio
* Support for memory allocation tracking

## Paging 3
* Complete rewrite 
* Coroutines support
* Support for Headers, Footers, Separators and other transformations like mapping, filtering.
* Loading State & Retry 
* Compatible with Paging 2

## CameraX
* Tests covering ~400M devices
* Seamless preview on any screen with PreviewView and optimizations depending on device support
* Easy YUV to RGB translation for smart imaging applications

## WorkManager 2.3 & 2.4
* Better in-process scheduler
* The scheduler no longer imposes scheduling limits
* Support for long running using foreground service so that it can run longer than 10min
* Diagnostics API from adb `adb shell am broadcast -a "androidx.work.diagnostics.REQUEST_DIAGNOSTICS" -p "<your_package_name>"` which dumps diagnostics in logcat 
* New Lint checks

## Navigation 2.3
* Support for Dynamic feature modules
* Deeplinking supports query paramets, custom actions, mime types
* Returning results through `currentBackStackEntry`/`previousBackStackEntry`.`savedStateHandle`

## ActivityResultContracts API
* Asking for permission is easier
* Replaces `startActivityForResult`
* Type safe contracts for commom intents

## AppCompat
* New Lint checks that point you to use app compat 
* More Reliable Dark Theme
* Configuration overrides API

```kotlin
override fun attachBaseContext(context: Context) {
    val config = Configuration()
    // ... customize configuration
    val updatedContext = context.createConfigurationContext(config)
    super.attachBaseContext(updatedContext)
}
```

## Webkit & Dark Mode

Forced dark mode support for WebView in 1.2.0
