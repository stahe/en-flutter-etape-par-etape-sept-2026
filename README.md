# Step-by-Step Introduction to the Flutter Mobile Framework

📖 **Read the tutorial: [https://stahe.github.io/en-flutter-etape-par-etape-sept-2026/](https://stahe.github.io/en-flutter-etape-par-etape-sept-2026/)**

This course teaches you how to build a **mobile** app using the [Flutter](https://flutter.dev) 3.44 framework and the [Dart](https://dart.dev) 3.12 language: an Android app whose screens are rendered **on the phone** using JSON data from a server. The same code also generates a web app.

It follows the outline of the [Step-by-Step Introduction to the React Framework](https://stahe.github.io/en-react-etape-par-etape-sept-2026/) course (as well as the [Vue.js](https://stahe.github.io/vuejs-etape-par-etape-sept-2026/) and [Angular](https://stahe.github.io/angular-etape-par-etape-sept-2026/) courses): same server, same screens, written in the Flutter style, for a phone.

| React Course | Flutter Course |
|---|---|
| a web app, in the browser | a mobile app (Android) and web app |
| functional components, JSX, hooks | widgets, a `build()` method, `setState` |
| HTML + CSS (Bootstrap) | the Flutter engine renders every pixel (Material 3) |
| React Router | go_router |
| Zustand, TanStack Query | provider (`ChangeNotifier`), a small cache |
| i18next | JSON dictionaries, `intl`, `flutter_localizations` |
| the browser stores the token cookie | an HTTP client that manages cookies (on the phone) |
| `localStorage` | `shared_preferences` |

The server, however, remains the same: it’s the **RdvMedecins** app’s JSON server, already used by the React, Vue.js, and Angular clients.

## The Approach: Many Short Examples, Then a Case Study

Flutter requires learning many concepts at once (a language, widgets, a lifecycle, asynchronous programming): the course is therefore structured around **25 short examples**, each focused on a single concept. They form a single Flutter project: just one `flutter pub get` command, followed by `flutter run -t lib/<example>/main.dart` to launch one.

| Chapter | Content | Examples |
|---|---|---|
| Getting Started | a Flutter project, `StatelessWidget` / `StatefulWidget`, `setState`, the widget tree, events, all field types, a reducer (sealed classes, `switch`), validation, `Form` and `FormField`, formatting (`intl`) | 01–09 |
| Widgets | parameters, functions as parameters (`ValueChanged`), composition (`child`, builders, generic widgets), lifecycle (`initState`, `didUpdateWidget`, `dispose`), `InheritedWidget`, mixins and animations, confirmation dialog (`showDialog`) | 10–16 |
| Routing | go_router 16: routes, parameters, `ShellRoute` + `NavigationBar`, lazy loading, `redirect`, guards | 17–18 |
| Asynchronous Programming and Shared State | `Future`, `Stream`, `async*`, timers, anti-bounce, stale responses, `FutureBuilder`, `StreamBuilder`, provider, `shared_preferences`, dark theme | 19–20 |
| Internationalization | JSON dictionaries, settings, plurals (`Intl.pluralLogic`), dates, amounts, translated calendar | 21 |
| The server: a black box | setting up the JSON server, its API, 48 `curl` examples, what changes for a mobile client | – |
| Communicating with the Server | the `http` package, the server address (emulator, phone, web), the token cookie on the phone, an API access layer, a model-view pattern (MVVM), server errors attached to fields | 22–25 |

Each example is presented with its complete code, commented line by line, and screenshots of its execution.

## The Server: A Black Box

The server is the NestJS server from previous lessons, whose controllers return **JSON**. This lesson treats it as a **black box**: we set it up, study its API, and query it with `curl`—but we don’t need to read its code (which is provided and commented for the curious).

- All errors have the same format: `{ "statusCode": 409, "cle": "ERRORS.LOGIN_TAKEN", "params": {...}, "champs": {...} }` — translation **keys**, never plain text;
- Authentication via a JWT token in an `httpOnly` cookie: the browser stores it automatically; on a phone, the app stores and sends it back;
- A “test mode” for the CAPTCHA to allow querying the API with `curl` (and generating screenshots via automated tests).

## The Case Study: The RdvMedecins Flutter Client

A complete application for **booking appointments at a doctor’s office**, with **all** of its files (about thirty) listed and commented on.

- **Modern Flutter**: Material 3, Dart 3 (records, filtering, sealed classes, `switch` expressions, extensions), go_router, provider, a layered architecture (data, state, UI).
- **Three roles**: `ADMIN` (manages doctors and clients), `DOCTOR` (books and cancels appointments), `USER` (the patient: books appointments for themselves, manages their account).
- **Privacy**: A patient never receives the names of other patients—the server does not send them.
- **The entire screen state in the URL**: `/agenda?idMedecin=1&jour=2026-10-05&reserver=7`; on a phone, the Back button closes the booking window; on the web, F5 and Back/Next work.
- **Server-side validation**: Forms display errors returned by the API below each field; optimistic locking, duplicate names, login already taken, etc.
- **Session**: Persists between sessions (the cookie is stored on the device), restored on startup (`GET /api/auth/moi`), expiration managed in a single location (401 response).
- **Optimized for mobile**: drawer menu (or fixed menu on large screens), lists instead of tables, password manager, error area above the navigation bar.
- **French / English**, including the calendar and Flutter’s own text.
- **Deployment**: the Android app (APK) and the compiled web version, served by the JSON server itself.

## Repository Contents

```
exemples_flutter/          the 25 short examples (a single Flutter project)
rdvmedecins-nestjs-json/   the RdvMedecins JSON server (the “black box”)
rdvmedecins_flutter/       the Flutter client for the case study
```

The platform-specific folders (`android/`, `web/`...) are generated by `flutter create` (see the course).

## Technologies

Flutter 3.44 · Dart 3.12 · Material 3 · go_router 16 · provider 6 · http 1.5 · shared_preferences 2.5 · flutter_svg 2 · intl · flutter_localizations · flutter_test · server-side: NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Prerequisites

- A basic understanding of object-oriented programming (Java, C#, TypeScript, etc.) and the HTTP protocol. The [Dart](https://stahe.github.io/dart-sept-2026/) course is a good preparation, but the Dart concepts used are explained throughout the examples.
- The Flutter SDK, Visual Studio Code and its Flutter extension, Android Studio (for the Android SDK and emulator) or an Android phone, Chrome; Node.js and a MySQL server (e.g., Laragon on Windows) for the JSON server. Installation instructions are provided in the course appendices.

## Author

This course, its examples, the Flutter client, and the JSON server adaptation were written by **Claude**, the AI from [Anthropic](https://www.anthropic.com) (September 2026), at the request of **Serge Tahé**.
