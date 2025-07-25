<h1 align="center">Hi, I'm Mikhail</h1>
<h3 align="center">QA Automation Engineer | Android UI Testing | Kotlin | Kaspresso</h3>

---

### About Me

- I am a **QA Automation Engineer** specializing in **Android UI testing**  
- I use **Kaspresso** to test real-world Android applications  
- Focused on **clean test architecture**, **stable test flows**, and **scalable frameworks**  
- Dedicated to writing meaningful, fast, and maintainable UI tests  

---

## Project Objective and Strategy

### The core purpose of this project is to make the Kaspresso framework approachable and quick to learn for automation engineers and full-stack QA.

This project is intentionally built using only **two technologies**:  
**Kotlin** and **Kaspresso**.

---

#### Key Principles of the Framework:

**1. Human-readable test logic**  
Tests are written using **named steps** and **named elements**, reducing verbosity and making test cases easy to read and reason about.

**2. Minimal boilerplate**  
A custom **DSL syntax** helps avoid repetitive interactions with dynamic UI components and lists.

**3. Clean and relevant reporting**  
**Interceptors** suppress redundant screenshots to ensure test reports stay focused and informative.

**4. Automated report export**  
Test results are automatically **generated and exported** from the device (or emulator) to the host machine or any configured location.

---

> The result: a scalable and modular UI testing framework that emphasizes **clarity**, **maintainability**, and **ease of adoption**.

Technical implementation details follow below.

---

### Featured Project: Now in Android (UI Test Automation)

[GitHub Repository: `nowinandroid`](https://github.com/st412m/nowinandroid)

This project provides UI test coverage for a production-level Jetpack Compose application.

Approach overview: [Testing Strategy](https://github.com/st412m/st412m/blob/main/testing_approach_readme.md)

Key components:

- **Kaspresso** UI testing framework  
- **Page Object** pattern for separation of concerns  
- Custom **matchers** for dynamic UI elements  
- Well-structured test suite:  
  [`/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui`](https://github.com/st412m/nowinandroid/tree/main/app/src/androidTest/kotlin/com/google/samples/apps/nowinandroid/ui)

Example test classes:
- `ForYouScreenTest.kt`  
- `TopicScreenTest.kt`  
- `NavigationTest.kt`  

These tests validate navigation flows, UI state changes, and content rendering using modular and scalable design patterns.

---

### Technologies and Tools

- **Languages**: Kotlin  
- **UI Test Automation**: Kaspresso, UI Automator, Jetpack Compose Testing  
- **Reporting**: Allure, Logcat analysis  
- **CI/CD**: GitHub Actions (in progress)  
- **Environment**: Android Studio, Gradle, Git  

---

### QA Automation Tools

Detailed explanation of tools used in the project:  
[QA Automation Tools Overview](QA_tools.md)

---

### Contact

- [LinkedIn – Mikhail Staroverov](https://www.linkedin.com/in/mikhail-staroverov/)

---

> *If a task can be automated, it should be automated. If automation is not possible, the task should be brought to a state where it can be automated — and then automated.*


