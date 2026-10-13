# Version catalog stub

One axis per change. The sample below bumps only the Android Gradle Plugin
alias. Leave the other versions on their current values until a later change.
Replace every TODO. Match the catalog keys the repo already uses.

Before:

```toml
[versions]
agp = "TODO_CURRENT_AGP"
kotlin = "TODO_CURRENT_KOTLIN"

[plugins]
android-application = { id = "com.android.application", version.ref = "agp" }
```

After (AGP only):

```toml
[versions]
agp = "TODO_TARGET_AGP"
kotlin = "TODO_CURRENT_KOTLIN"

[plugins]
android-application = { id = "com.android.application", version.ref = "agp" }
```

Wrapper bumps belong in `gradle/wrapper/gradle-wrapper.properties`, not in this catalog:

```properties
distributionUrl=TODO_GRADLE_DISTRIBUTION_URL
```

Compile and test with `TODO_COMPILE_COMMAND` and `TODO_TEST_COMMAND`.
