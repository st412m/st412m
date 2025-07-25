# Подход к UI-тестированию Android приложений

## Что это такое

В процессе разработки мне потребовалось создать удобную систему для UI-тестирования, которая была бы понятной для всей команды и легко поддерживаемой. В итоге получилось решение на основе **Kaspresso** и **Kakao**, использующее паттерн **Domain-Specific Language (DSL)**.

Основная идея - писать тесты так, чтобы их мог понять любой участник команды, даже без глубоких знаний в автоматизации.

## Как устроено

Вся логика разбита на три основных класса:

| Компонент | Что делает | Код |
|-----------|------------|-----|
| **ActionSteps** | Выполняет действия в интерфейсе | [ActionSteps.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/ActionSteps.kt) |
| **CheckSteps** | Проверяет состояние элементов | [CheckSteps.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/CheckSteps.kt) |
| **StepsExecutor** | Координирует выполнение команд | [StepsExecutor.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/StepsExecutor.kt) |

## Почему именно так

### Читаемость превыше всего

Вместо сложных конструкций получился простой и понятный код:

```kotlin
actions {
    uiClick("Login")
    scrollTo(someElement)
    swipeVertically(1.0, 10)
}
```

Такой тест может прочитать QA-инженер, менеджер или новый разработчик в команде. [Вот живой пример](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tests/TopAppBarTests.kt) из реального проекта.

### Никакого дублирования кода

Вся сложная логика взаимодействия с UI спрятана в [StepsExecutor](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/StepsExecutor.kt). Если нужно что-то изменить в поведении - правишь в одном месте, а не в десятках тестов. Плюс есть [полезные расширения](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/NodeActionExt.kt) для работы с элементами.

### Автоматические отчеты

Каждый шаг теста автоматически попадает в Allure-отчет. Не нужно ничего дополнительно писать - просто запускаешь тест и получаешь [красивый отчет](https://github.com/st412m/st412m/blob/main/scr/allure_report_example.png) с описанием всех действий.

## Работа с Jetpack Compose

Отдельная боль - тестирование списков в Compose. Для этого написал специальные расширения:

- [KLazyListNodeExt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/KLazyListNodeExt.kt) - для ленивых списков

### Что умеет

Можно обращаться к элементам списка по индексу:
```kotlin
list.invokeAtIndex<TopicSelectionsListItems>(index = 2) { 
    performClick() 
}
```

Или искать элементы по любым условиям, что особенно удобно когда порядок элементов может меняться.

IDE подсказывает типы, ловит ошибки на этапе компиляции, а в отчетах элементы получают [понятные названия](https://github.com/st412m/st412m/blob/main/scr/allure_report_topic_selection_list.png).

Пример использования можно посмотреть [здесь](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tests/TopicSelectionListTests.kt).

## Скриншоты в тестах

Реализовал два интерсептора, которые автоматически делают скриншоты в нужные моменты:

| Интерсептор | Когда срабатывает | Код |
|-------------|-------------------|-----|
| **FailOnlyScreenshotStepInterceptor** | Только при ошибках | [FailOnlyScreenshotStepInterceptor.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/interceptors/FailOnlyScreenshotStepInterceptor.kt) |
| **SuccessFinaleScreenshotTestInterceptor** | В конце каждого теста | [SuccessFinaleScreenshotTestInterceptor.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/interceptors/SuccessFinaleScreenshotTestInterceptor.kt) |

### Зачем это нужно

Первый интерсептор экономит место - скриншоты создаются только когда что-то пошло не так. Второй показывает финальное состояние экрана после теста, что помогает понять, правильно ли все отработало.

Скриншоты автоматически попадают в Allure с понятными названиями:
- При ошибке: `<testClassName>_step_<ordinal>_failure_<errorType>`
- В конце: `<testName>_success` или `<testName>_failed`

## Настройка сборки

В `build.gradle` добавил задачи, которые автоматически управляют результатами тестов:

```kotlin
// Удаляет старые результаты локально
tasks.register<Delete>("deleteLocalAllureResults") {
    group = "verification"
    description = "Deletes local allure-results directory"
    
    val targetDir = file("build/allure-results")
    delete(targetDir)
}

// Копирует результаты с устройства
tasks.register<Exec>("pullAllureResults") {
    group = "verification"
    description = "Pulls allure-results from device to app/build"
    
    dependsOn(tasks.named("deleteLocalAllureResults"))
    
    val adbCommand = listOf("adb", "pull", "/sdcard/Documents/allure-results", "build")
    commandLine = adbCommand
    isIgnoreExitValue = true
}

// Очищает результаты на устройстве
tasks.register<Exec>("clearDeviceAllureResults") {
    group = "verification"
    description = "Clears allure-results directory on Android device"
    
    val adbCommand = listOf("adb", "shell", "rm", "-rf", "/sdcard/Documents/allure-results")
    commandLine = adbCommand
    isIgnoreExitValue = true
}

// Привязывает все к тестовым задачам
tasks.withType<DeviceProviderInstrumentTestTask>().configureEach {
    if (name.lowercase().startsWith("connected") && name.lowercase().endsWith("androidtest")) {
        dependsOn(tasks.named("clearDeviceAllureResults"))
        finalizedBy(tasks.named("pullAllureResults"))
    }
}
```

### Как это работает

Когда запускаешь тесты, автоматически происходит:
1. Очистка старых результатов на устройстве
2. Запуск тестов  
3. Копирование свежих результатов в локальную папку

Все задачи помечены как `isIgnoreExitValue = true`, чтобы сборка не падала из-за мелких проблем (например, если папка с результатами еще не создана).

## Что в итоге получилось

### Для разработчиков
- Новички быстро разбираются благодаря простому DSL
- Готовые компоненты ускоряют написание тестов
- Подробные отчеты упрощают отладку

### Для поддержки проекта
- Модульная архитектура - каждый класс отвечает за свое
- Новые действия добавляются легко
- Изменения вносятся в одном месте

### Для CI/CD
- Полная автоматизация без ручных операций
- Устойчивость к временным сбоям
- Детальные отчеты для анализа результатов

## Где лучше всего использовать

Такой подход особенно хорошо показывает себя в:

- Проектах с большим количеством UI-тестов
- Командах с разным уровнем экспертизы в тестировании
- Проектах, где важна детальная отчетность
- Приложениях на Jetpack Compose с динамическим контентом

## Выводы

В результате получилось решение, которое:

✅ Делает тесты понятными для всей команды  
✅ Убирает дублирование и упрощает поддержку  
✅ Автоматически создает детальные отчеты  
✅ Легко расширяется под новые задачи  
✅ Хорошо интегрируется в процессы разработки  

Подход можно адаптировать под специфику любого Android-проекта, сохранив основные принципы читаемости и простоты использования.
