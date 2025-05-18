# Infrastructure Design Document  
##  Project: **Quizland**  
##  Date: *17.05.2025*

---

## 1. Overview

This document outlines the infrastructure design of the **Quizland** mobile application. It includes a description of the architecture, local data management, module structure, and tools used in development.

---

## 2. Infrastructure Goals

- Lightweight, offline-first infrastructure
- No external dependencies (APIs, servers, cloud)
- Local-first data storage with persistence
- Maintainable, testable, and extensible codebase
- Dependency injection for decoupling and scalability

---

## 3. Application Environment

| Environment       | Details                          |
|-------------------|----------------------------------|
| Platform          | Android                          |
| Language          | Kotlin                           |
| UI Framework      | XML                              |
| Architecture      | MVVM with MVI elements           |
| Data Storage      | Room (SQLite)                    |
| Dependency Injection | Hilt                         |
| Networking (prepared) | Retrofit (not currently used) |
| Build Tool        | Gradle                           |
| Version Control   | Git                              |

---

## 4. Logical Architecture

```
[ UI Layer (Fragments + ViewModels) ]
|
[ Business Logic / State Management ]
|
[ Data Layer (Room DB, Repositories) ]
```

- **UI Layer**: Fragments with XML layout files.
- **ViewModel Layer**: Manages UI-related state and communicates with the repository.
- **Data Layer**: Room database accessed through DAO interfaces, with data models mapped to domain models.

---

## 5. Module Structure

```
src/
 └── main/
     └── java/com/chunmaru/quizland/
         ├── data/
         │   └── domain/hilt/Module.kt
         ├── presentation/screens/
         │   ├── home/
         │   ├── question/
         │   ├── profile/
         │   └── favorite/
         ├── App.kt
         └── MainActivity.kt
```

- Each feature (e.g., Home, Question, Profile) is modularized into its own screen directory.
- `App.kt` initializes Hilt.
- `Module.kt` provides Hilt DI setup.

---

## 6. Data Management

- **Room** is used for all persistent data storage.
- No cloud or external data sources.
- All user data (quiz results, favorites) is stored locally.
- Data survives app restarts but is not backed up to cloud.

---

## 7. Security Considerations

- **No authentication** or encryption.
- No secure communication is needed (offline only).
- Minimal security measures, relying on Android sandboxing and Room’s basic protections.

---

## 8. Deployment Model

There is **no backend server** or cloud infrastructure. All components run **locally on the user’s Android device**.

| Component     | Location        |
|---------------|-----------------|
| App UI        | Android client  |
| Data storage  | SQLite via Room |
| Configuration| Bundled in APK  |

---

## 9. Limitations

- No online features or backups
- No CI/CD or automated deployment pipelines
- No scalability infrastructure (e.g., server load balancing)
- No centralized monitoring or analytics

---

## 10. Future Infrastructure Improvements

- Add Firebase or Supabase for user authentication and data sync
- Set up basic CI/CD pipeline (GitHub Actions, Bitrise, etc.)
- Integrate crash reporting (Firebase Crashlytics)
- Enable cloud sync for cross-device persistence
- Add test coverage and static analysis tools (Detekt, ktlint)

---

## Conclusion

Quizland is a minimal, offline-first Android application. Its infrastructure is intentionally simple, prioritizing maintainability and user privacy. Though limited in scale, the design provides a solid foundation for future enhancements, including cloud-based features and DevOps integration.