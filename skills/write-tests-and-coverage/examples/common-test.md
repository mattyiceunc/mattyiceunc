# Common test stub

Match the module's existing test source set and framework. The skeleton below
uses `kotlin.test`. Replace every TODO. Point the test at the seam the
production code already exposes.

`src/commonTest/kotlin/TODO_PACKAGE/TODO_TYPETest.kt`:

```kotlin
package TODO_PACKAGE

import kotlin.test.Test
import kotlin.test.assertEquals
import kotlin.test.assertFailsWith

class TODO_TYPETest {
    @Test
    fun successPath() {
        assertEquals(TODO_EXPECTED, TODO_TYPE().TODO_METHOD(TODO_INPUT))
    }

    @Test
    fun rejectsEdge() {
        assertFailsWith<TODO_EXCEPTION> {
            TODO_TYPE().TODO_METHOD(TODO_BAD_INPUT)
        }
    }
}
```

Run `TODO_MODULE_TEST_TASK`. If the repo already has a coverage task, run
`TODO_COVERAGE_TASK` for this module only.
