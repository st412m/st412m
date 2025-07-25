# Кастомное решение для UI-тестирования Android

## 📖 Обзор

Данный проект представляет авторскую реализацию подхода к UI-тестированию Android-приложений, построенную на основе библиотек **Kaspresso** и **Kakao**. Разработанная архитектура реализует паттерн **Domain-Specific Language (DSL)** для создания читаемых, поддерживаемых и эффективных автотестов.

## 🦶 Именованные шаги

### Основные компоненты

| Компонент | Назначение | Ссылка |
|-----------|------------|--------|
| **ActionSteps** | Выполнение действий в UI | [ActionSteps.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/ActionSteps.kt) |
| **CheckSteps** | Проверки состояния UI | [CheckSteps.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/CheckSteps.kt) |
| **StepsExecutor** | Центральный исполнитель команд | [StepsExecutor.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/StepsExecutor.kt) |

## 🚀 Ключевые особенности

### 1. DSL-подход для UI-тестирования

#### ✅ Преимущества

- **Читаемость кода**: Тесты написаны в стиле, близком к естественному языку
- **Декларативность**: Код описывает *что* делать, а не *как*
- **Доступность**: Понятен даже людям без глубоких технических знаний

#### 📝 Пример использования

```kotlin
actions {
    uiClick("Login")
    scrollTo(someElement)
    swipeVertically(1.0, 10)
}
```

*[Полный пример теста](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tests/TopAppBarTests.kt)*

### 2. Унификация и централизация логики

- **Единая точка реализации**: Все низкоуровневые операции инкапсулированы в [StepsExecutor](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/StepsExecutor.kt)
- **Расширяемость**: Поддержка [NodeActions Extensions](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/NodeActionExt.kt)
- **Изоляция**: Тесты не зависят от деталей реализации UI-взаимодействий

### 3. Интеграция с Allure Reports

- **Автоматическое логирование**: Каждый шаг добавляется в отчет с подробным описанием
- **Визуализация**: Примеры отчетов доступны [здесь](https://github.com/st412m/st412m/blob/main/scr/allure_report_example.png)
- **Гибкость именования**: Поддержка кастомных названий шагов

## 🎯 Работа с Jetpack Compose

### Расширения для списков

Реализованы специализированные расширения для работы с `LazyColumn` и обычными списками в Jetpack Compose:

| Расширение | Назначение |
|------------|------------|
| [KLazyListNodeExt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/extensions/KLazyListNodeExt.kt) | Работа с ленивыми списками |

#### 🔧 Основные возможности

- **Индексированный доступ**: `list.invokeAtIndex<TopicSelectionsListItems>(index = 2) { performClick() }`
- **Поиск по предикату**: Динамический поиск элементов по условиям
- **Типобезопасность**: Использование generics с поддержкой IDE
- **Allure-интеграция**: Автоматическое именование элементов в отчетах

#### 📊 Пример отчета

![Topic Selection List Report](https://github.com/st412m/st412m/blob/main/scr/allure_report_topic_selection_list.png)

*[Пример использования](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tests/TopicSelectionListTests.kt)*

## 📸 Система скриншотов

### Кастомные интерсепторы

В проекте реализованы два специализированных интерсептора для автоматического создания скриншотов:

| Интерсептор | Назначение | Ссылка |
|-------------|------------|--------|
| **FailOnlyScreenshotStepInterceptor** | Скриншоты только при ошибках | [FailOnlyScreenshotStepInterceptor.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/interceptors/FailOnlyScreenshotStepInterceptor.kt) |
| **SuccessFinaleScreenshotTestInterceptor** | Финальные скриншоты тестов | [SuccessFinaleScreenshotTestInterceptor.kt](https://github.com/st412m/nowinandroid/blob/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui/tools/interceptors/SuccessFinaleScreenshotTestInterceptor.kt) |

#### 🎯 Особенности работы

- **Экономия ресурсов**: Скриншоты создаются только при необходимости
- **Автоматическое именование**: Четкая схема тегов для каждого типа скриншота
- **Интеграция с Allure**: Автоматическое прикрепление к отчетам

#### 🏷️ Схема именования

- **При ошибках**: `<testClassName>_step_<ordinal>_failure_<errorType>`
- **Финальные**: `<testName>_success` или `<testName>_failed`

## ⚙️ Gradle-интеграция

### Автоматизация управления Allure-результатами

В `build.gradle` реализованы специальные задачи для управления результатами тестирования:

```kotlin
tasks.register<Delete>("deleteLocalAllureResults") {
    group = "verification"
    description = "Deletes local allure-results directory"
    
    val targetDir = file("build/allure-results")
    delete(targetDir)
}

tasks.register<Exec>("pullAllureResults") {
    group = "verification"
    description = "Pulls allure-results from device to app/build"
    
    dependsOn(tasks.named("deleteLocalAllureResults"))
    
    val adbCommand = listOf("adb", "pull", "/sdcard/Documents/allure-results", "build")
    commandLine = adbCommand
    isIgnoreExitValue = true
}

tasks.register<Exec>("clearDeviceAllureResults") {
    group = "verification"
    description = "Clears allure-results directory on Android device"
    
    val adbCommand = listOf("adb", "shell", "rm", "-rf", "/sdcard/Documents/allure-results")
    commandLine = adbCommand
    isIgnoreExitValue = true
}

tasks.withType<DeviceProviderInstrumentTestTask>().configureEach {
    if (name.lowercase().startsWith("connected") && name.lowercase().endsWith("androidtest")) {
        dependsOn(tasks.named("clearDeviceAllureResults"))
        finalizedBy(tasks.named("pullAllureResults"))
    }
}
```

#### 🔄 Жизненный цикл задач

1. **Очистка устройства** → 2. **Запуск тестов** → 3. **Копирование результатов**

### 📋 Доступные задачи

| Задача | Описание |
|--------|----------|
| `deleteLocalAllureResults` | Удаление локальных результатов |
| `pullAllureResults` | Копирование результатов с устройства |
| `clearDeviceAllureResults` | Очистка результатов на устройстве |

## 💡 Преимущества подхода

### 📈 Для разработчиков

- **Снижение порога входа**: Простой и понятный DSL
- **Быстрая разработка**: Готовые компоненты и методы
- **Легкая отладка**: Детальные Allure-отчеты с скриншотами

### 🔧 Для поддержки

- **Модульность**: Четкое разделение ответственности
- **Расширяемость**: Простое добавление новых действий
- **Централизация**: Единая точка модификации логики

### 🚀 Для CI/CD

- **Автоматизация**: Полная интеграция с пайплайнами
- **Устойчивость**: Обработка ошибок и recovery
- **Мониторинг**: Детальные отчеты для анализа

## 🎯 Применение

Данное решение особенно эффективно для:

- **Крупных проектов** с большим количеством UI-тестов
- **Команд разработки** с разным уровнем экспертизы
- **CI/CD-конвейеров** с требованиями к детальной отчетности
- **Проектов на Jetpack Compose** с динамическим контентом

## 📚 Заключение

Представленная реализация подхода к UI-тестированию обеспечивает:

- ✅ **Читаемость и поддерживаемость** кода
- ✅ **Унификацию и централизацию** логики
- ✅ **Интеграцию с современными инструментами** отчетности
- ✅ **Гибкость и расширяемость** архитектуры
- ✅ **Эффективную командную работу**

Решение создано с учетом лучших практик Android-разработки и может быть адаптировано под специфические требования любого проекта.
