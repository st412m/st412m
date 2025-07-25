# QA Automation Tools for NowInAndroid (Kaspresso + Kotlin)

This repository contains a description of QA automation tools and utilities used in the [NowInAndroid](https://github.com/st412m/nowinandroid) project.  
All sources are located in the `nowinandroid` repo under:

`app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/`

---

## Main files and brief descriptions

| File | Description | Link in NowInAndroid repo |
|-|-|-|
| `KLazyListNodeExt.kt` | Extensions for Compose lazy lists in Kaspresso tests | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/KLazyListNodeExt.kt) |
| `NodeActionExt.kt` | Extensions for UI element actions in Kaspresso | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/NodeActionExt.kt) |
| `TestContextExt.kt` | Helper functions for test context operations | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/TestContextExt.kt) |
| `FailOnlyScreenshotStepInterceptor.kt` | Takes screenshots only on step/test failure | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/interceptors/FailOnlyScreenshotStepInterceptor.kt) |
| `SuccessFinaleScreenshotTestInterceptor.kt` | Takes screenshots on successful test completion | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/interceptors/SuccessFinaleScreenshotTestInterceptor.kt) |
| `AllureAnnotationRule.kt` | JUnit rule for adding Allure annotations | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/rules/AllureAnnotationRule.kt) |
| `DeprecatedTestRule.kt` | Marks tests as deprecated with Allure messages | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/rules/DeprecatedTestRule.kt) |
| `HappyTestRule.kt` | Marks tests as “happy path” with Allure tags | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/rules/HappyTestRule.kt) |
| `ActionSteps.kt` | Wrappers for Kaspresso UI actions with step logging | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/ActionSteps.kt) |
| `CheckSteps.kt` | Wrappers for UI checks integrated with Allure | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/CheckSteps.kt) |
| `NameHierarchy.kt` | Utility for building hierarchical step and screen names | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/NameHierarchy.kt) |
| `NamedComposeScreen.kt` | Abstract Compose screen class with naming for Kaspresso | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/NamedComposeScreen.kt) |
| `StepsDSL.kt` | DSL for defining test steps with Kaspresso and Allure | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/StepsDSL.kt) |
| `StepsExecutor.kt` | Centralized executor for steps with Allure logging | [Link](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/StepsExecutor.kt) |

---

## Useful links

- [Kaspresso GitHub](https://github.com/KasperskyLab/Kaspresso)  
- [Allure Framework](https://docs.qameta.io/allure/)  
- [Jetpack Compose Testing](https://developer.android.com/jetpack/compose/testing)

---

**Author:** [st412m](https://github.com/st412m)  
**Project:** NowInAndroid QA Automation  
