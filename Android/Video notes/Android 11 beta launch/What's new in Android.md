# What's new in Android

Notes on [What's new in Android](https://www.youtube.com/watch?v=fnkFOhA7FC4&feature=youtu.be)

## UI

### Window insets

#### More information
More information on where are status, navigation, IME...

```kotlin
// get WindowInsets object from listener
view.setOnApplyInsetsListener { view, insets -> 

    // See if the IME is visible
    val imeVisisble = insets.isVisisble((WindowInsets.Type.ime()))

    if (imeVisisble) {
        val imeInsets = insets.getInsets(WindowInsets.Type.ime())
        // ...
    }
}
```

#### IME animations

Syncronize keyboard animations
* listen for changes
* drive keyboard animation

To listen for changes use: [View.setWindowInsetsAnimationCallback](https://developer.android.com/reference/android/view/View.html#setWindowInsetsAnimationCallback(android.view.WindowInsetsAnimation.Callback))

To control the animation: [View.getWindowInsetsController](https://developer.android.com/reference/android/view/View#getWindowInsetsController()) and [WindowInsetsController.controlWindowInsetsAnimation](https://developer.android.com/reference/android/view/WindowInsetsController#controlWindowInsetsAnimation(int,%20long,%20android.view.animation.Interpolator,%20android.os.CancellationSignal,%20android.view.WindowInsetsAnimationControlListener))

#### Resources
Window insets animation sample: [goo.gle/insetsanimsample](goo.gle/insetsanimsample)

Android Developers Backstage [138: Animated IME - Oh, my!](http://androidbackstage.blogspot.com/2020/04/episode-138-animated-ime-oh-my.html)


### Conversations

Separate notification category for conversations

```kotlin
// Create and post  shortcut
val person = Person.Builder().build()
val shortcutInfo = ShortcutInfoCompat.Builder(this, "sampleShortcut")
    .setPerson(person)
    .setLongLived(true) // so user can go back to conversation even if app is not running anymore
    // ...
    .build()
ShortcutManagerCompat.pushDynamicShortcut(shortcutInfo)

// Create notification with shortcut
val style = NotifcationCompat.MessagingStyle(person)
    .addMessage(...)
    // ...
NotificationCompat.Builder(this, "foo")
    .setShortcutId(shortcutInfo.id)
    // ...
    .build()
```

### Bubbles

* Better than System Alert Window
* Created with Notification API
    * with more metadata
    * and dedicated activity

Activity needs to have `resizableActivity=true`

#### Resources: 
* [What's new in System UI](http://androidbackstage.blogspot.com/2020/06/episode-140-bubbles.html)
* [Bubbles doc](https://developer.android.com/guide/topics/ui/bubbles)
* [Android Samples](https://github.com/android/user-interface-samples)
* Android Developers Backstage [140: Bubbles](http://androidbackstage.blogspot.com/2020/06/episode-140-bubbles.html)

## Privacy

### Data Access Auditing

API for auditing: 
Callbacks invoked when user-permission-required data is accessed
[AppOpsManager.setOnOpNotedCallback](https://developer.android.com/reference/kotlin/android/app/AppOpsManager#setonopnotedcallback)

### One Time Permissions

Developers may not have to do anything to handle this behaviour.

### Background Location

* More Restrictive
* First, Request foreground permission 
* Then request background permission which take the user to Settings

### Foreground Service Type

Android 11 introduces: `<service android:foregroundServiceType="camera|microphone" />`

### More Changes

* Package visisbility restrictions 
* Scoped storage
* Auto-reset permissions

## Developer tools

* Wifi debugging
* More Nulability Annotations
    * `@RecentlyNullable`, `@RecentlyNonNull` -> Warnings
    * `@Nullable`, `@NonNull` -> Errors
* Crash Reasons Reporting
    * Api to query app crash reason
    * [getHistoricalProcessExitReasons()](https://developer.android.com/reference/kotlin/android/app/ActivityManager#gethistoricalprocessexitreasons)
* GWP-ASan
* ADB Incremental
    * Faster installs after small changes
    * First: sign APK, crete APK Signature Scheme v4 file
    * `adb install --incremental`
* Menu for toggling R changes (App Compatibility Changes) and command line options (`adb shell am compat [enable]|[disable] FEATURE PACKAGE` )

## Graphics & Media

### Decoders
All decoders are available from native code 

### Animated HEIF 
* Loaded as AnimatedImageDrawable
* Like animated GIFs
* But smaller

### Audio
* Oboe to replace OpenSL ES
* [github.com/google/oboe](github.com/google/oboe)
* Android Developers Backstage [135: Audio Podcast](http://androidbackstage.blogspot.com/2020/04/episode-135-audio-podcast.html)

### Variable refresh rate

* For apps with their own rendering loop (eg games)
* Enables more flexible backoff rates
* `Surface.setFrameRate()`

## More 

### Neural Network API
* C API for on Device machine Learning
* NNAPI 1.3: Performance and functionality

### 5G

* API to optimize 5G experience 

### Autofill keyboard integration

Instead of dropdown now it's part of keyboard, but keyboard doesn't have access to data only to UI.

On Keyabord side implement:
* `onCreateInlineSuggestionsRequest(uiExtras: bundle): InlineSuggestions?`
* `onInlineSuggestinosReponse reponse): Boolean`

On App side: 
* override [`onFillRequest`](https://developer.android.com/reference/android/service/autofill/AutofillService#onFillRequest(android.service.autofill.FillRequest,%20android.os.CancellationSignal,%20android.service.autofill.FillCallback))

## What's next?

* 11 Weeks on Android: [https://developer.android.com/11weeksofandroid](https://developer.android.com/11weeksofandroid)
* Android 11 Meetups: [https://developer.android.com/android11/meetups](https://developer.android.com/android11/meetups)