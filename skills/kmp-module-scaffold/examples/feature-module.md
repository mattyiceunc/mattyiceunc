# Feature module stub

Adapt this skeleton to the sibling modules in the target repo. Replace every
TODO. Do not add targets the project does not already build.

```text
TODO_MODULE/
  build.gradle.kts
  src/commonMain/kotlin/TODO_PACKAGE/TODO_TYPE.kt
  src/commonTest/kotlin/TODO_PACKAGE/TODO_TYPETest.kt
```

`settings.gradle.kts` (match the include style already in the file):

```kotlin
include(":TODO_MODULE")
```

`TODO_MODULE/build.gradle.kts`:

```kotlin
plugins {
    alias(libs.plugins.TODO_KOTLIN_MULTIPLATFORM)
    // alias(libs.plugins.TODO_ANDROID) — only if sibling modules apply it
}

kotlin {
    // TODO: copy the targets sibling modules declare
    sourceSets {
        commonTest.dependencies {
            implementation(kotlin("test"))
        }
    }
}
```

`TODO_TYPE.kt`:

```kotlin
package TODO_PACKAGE

class TODO_TYPE
```

`TODO_TYPETest.kt`:

```kotlin
package TODO_PACKAGE

import kotlin.test.Test
import kotlin.test.assertNotNull

class TODO_TYPETest {
    @Test
    fun creates() {
        assertNotNull(TODO_TYPE())
    }
}
```

Check with the repo's existing command, or `TODO_GRADLE :TODO_MODULE:check`.
