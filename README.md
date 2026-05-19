# DealCheck Pro 🏠

A Flutter mobile application for real estate investors to analyze property deals, track investment metrics, and manage their portfolio — with Firebase authentication, Firestore database, PDF report generation, and live currency conversion.

---

## Features

- **Authentication** — Email/password sign-up & login via Firebase Auth, with secure password validation and change passcode screen.
- **Property Deal Analysis** — Analyze deals across multiple investment strategies (e.g., Buy & Hold, Fix & Flip, BRRRR). Each property gets a deal rating: *Strong Deal*, *Borderline*, or *Weak Deal*.
- **Multi-Currency Support** — Live exchange rates from ExchangeRate API. Converts USD amounts to PKR, AED, GBP, EUR, and CAD.
- **PDF Reports** — Generate and download professional property analysis reports as PDFs using the `pdf` and `printing` packages.
- **Firestore Portfolio** — All properties are stored per-user in Cloud Firestore and synced in real time.
- **Property Search** — Search and filter saved properties by strategy.
- **Notifications Screen** — In-app notification history.
- **User Profile** — Save name, phone, email, and location. Manage personal info from the profile screen.
- **Subscription & Billing Screen** — UI for plan management.
- **Dark Theme** — Custom dark UI (`#051424` background, `#00E676` green accent, Inter font).

---

## Project Structure

```
lib/
├── main.dart                   # App entry point, Firebase init, theme setup
├── firebase_options.dart       # Auto-generated Firebase config (FlutterFire CLI)
├── screen1.dart                # Login & Sign-Up screen
├── screen2.dart                # Property input / deal analysis screen
├── screen3.dart                # Home / dashboard screen
├── screen4.dart                # Property detail screen
├── screen5.dart                # (Extended analysis / results screen)
├── searchscreen.dart           # Search & filter properties
├── notificationscreen.dart     # Notifications
├── profilescreen.dart          # User profile
├── personal_info_screen.dart   # Edit personal info
├── change_passcode_screen.dart # Change password
├── subscription_screen.dart    # Subscription & billing
├── property_model.dart         # Property data model
├── firestore_service.dart      # Firestore CRUD + user profile helpers
├── api_service.dart            # Exchange rate API integration
└── pdf_service.dart            # PDF report generation
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| Auth | Firebase Authentication |
| Database | Cloud Firestore |
| Exchange Rates | ExchangeRate API (free tier) |
| PDF | `pdf` + `printing` packages |
| HTTP | `http` package |
| Font | Inter (Google Fonts) |

---

## Prerequisites

Before running the app, make sure you have:

- [Flutter SDK](https://docs.flutter.dev/get-started/install) (3.x or later)
- [Android Studio](https://developer.android.com/studio) with Flutter & Dart plugins
- A Firebase project (already configured — see `firebase_options.dart`)
- A device or emulator running Android 6.0+ (API 23+)

---

## Firebase Setup

This project is already connected to Firebase project **`dealcheckpro-6af77`**. The `firebase_options.dart` file is pre-configured.

If you fork this project and want to use your own Firebase:

1. Create a new Firebase project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Authentication** → Email/Password
3. Enable **Cloud Firestore** and set rules
4. Run `flutterfire configure` to regenerate `firebase_options.dart`
5. Download `google-services.json` and place it in `android/app/`

---

## Dependencies (pubspec.yaml)

Add these to your `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter

  # Firebase
  firebase_core: ^3.x.x
  firebase_auth: ^5.x.x
  cloud_firestore: ^5.x.x

  # Networking
  http: ^1.x.x

  # PDF
  pdf: ^3.x.x
  printing: ^5.x.x

  # Fonts
  google_fonts: ^6.x.x
```

Run:

```bash
flutter pub get
```

---

## How to Add This to Your Flutter Project in Android Studio

### Step 1 — Create or Open Your Flutter Project

Open Android Studio → **File → Open** your existing Flutter project, or create a new one via **File → New → New Flutter Project**.

### Step 2 — Place the `lib/` Files

1. Extract the `lib.zip` file on your computer.
2. In Android Studio's **Project** panel (left sidebar), make sure you are in **Project** view (not Android view).
3. Locate the `lib/` folder in your project root.
4. **Copy all `.dart` files** from the extracted `lib/` folder into your project's `lib/` folder.
   - You can drag and drop them directly in Android Studio's Project panel, or
   - Use your file explorer to paste them into `<your_project>/lib/`

> ⚠️ If your project already has a `main.dart`, the new `main.dart` will replace it. Back up yours first if needed.

### Step 3 — Add `google-services.json`

1. Go to your Firebase Console → Project Settings → Your Android app.
2. Download `google-services.json`.
3. Place it inside `android/app/` in your project.

### Step 4 — Update `android/build.gradle`

In `android/build.gradle` (project level), add inside `dependencies {}`:

```groovy
classpath 'com.google.gms:google-services:4.4.1'
```

### Step 5 — Update `android/app/build.gradle`

At the bottom of `android/app/build.gradle`, add:

```groovy
apply plugin: 'com.google.gms.google-services'
```

Also make sure `minSdkVersion` is at least **23**:

```groovy
android {
    defaultConfig {
        minSdkVersion 23
    }
}
```

### Step 6 — Add Dependencies to `pubspec.yaml`

Open `pubspec.yaml` and add all required packages listed in the **Dependencies** section above. Then in the Android Studio terminal run:

```bash
flutter pub get
```

### Step 7 — Run the App

Connect a device or start an emulator, then click the **Run ▶** button in Android Studio, or run in terminal:

```bash
flutter run
```

---

## Firestore Data Structure

```
users/
  {uid}/
    name: string
    phone: string
    email: string
    location: string
    updatedAt: string (ISO 8601)

    properties/
      {propertyId}/
        strategy: string
        dealRating: string   ("Strong Deal" | "Borderline" | "Weak Deal")
        createdAt: timestamp
        ... (all deal fields)
```

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `google-services.json` missing error | Download from Firebase Console → Project Settings and place in `android/app/` |
| `minSdkVersion` error | Set `minSdkVersion 23` in `android/app/build.gradle` |
| `firebase_options.dart` not found | Make sure the file is in `lib/` (it's included in the zip) |
| Exchange rates not loading | Check internet permission in `AndroidManifest.xml`: `<uses-permission android:name="android.permission.INTERNET"/>` |
| PDF not generating | Make sure `pdf` and `printing` packages are in `pubspec.yaml` and `flutter pub get` was run |

---

## Internet Permission

Make sure your `android/app/src/main/AndroidManifest.xml` has:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

---

## License

This project is proprietary. All rights reserved.
