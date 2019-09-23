## Why did this happen?

Because after upgrade,  `androidx.core:core`  is accessed somewhere, when your project is still not using androidx. So classes like  `INotificationSideChannel`  and many others are now found at two places -  `androidx.core:core`  and  `com.android.support:support-compat`. That's why this error occured.

## Solution?

You need to migrate to AndroidX which you should have done already. If you don't know about AndroidX. Please read  [**What is AndroidX**?](https://stackoverflow.com/a/52517772/6891563)

## How to migrate current project

In Android Studio 3.2 (September 2018), there is direct option to migrate existing project to  `AndroidX`. This refract all packages automatically.

**Before you migrate, it is strongly recommended to backup your project.**

> ### Existing project

-   Android Studio > Refactor Menu > Migrate to AndroidX...
-   It will analysis and will open Refractor window in bottom. Accept changes to be done.

[![image](https://i.stack.imgur.com/DEV2M.png)](https://i.stack.imgur.com/DEV2M.png)

> ### New project

Put these flags in your  `gradle.properties`

```
android.enableJetifier=true
android.useAndroidX=true
```

---
출처 : [https://stackoverflow.com/questions/55810694/after-upgrade-android-version-getting-duplicate-class-android-support-v4-app-in](https://stackoverflow.com/questions/55810694/after-upgrade-android-version-getting-duplicate-class-android-support-v4-app-in)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTM0ODg5MDMzXX0=
-->