# Flutter Firebase Setup

In this guide, you will connect your Flutter project with the Firebase project created in the previous step.

---

# Prerequisites

Before proceeding, ensure that:

- Firebase Project has been created.
- Android App has been registered.
- `google-services.json` has been downloaded.
- Flutter SDK is installed.
- Android Studio is installed.

---

# Step 1: Open Your Flutter Project

Open your project in Android Studio or VS Code and verify it runs successfully before making any changes.

```bash
flutter run
```

---

# Step 2: Place google-services.json

Copy the `google-services.json` file downloaded in the previous guide into:

```
android/app/
```

Your folder structure should look like this:

```
android/
└── app/
    ├── google-services.json   ← place it here
    ├── build.gradle
    └── src/
```

> **Important:** Do not rename the file. It must be exactly `google-services.json`.

---

# Step 3: Update Project-Level build.gradle

Open the **project-level** Gradle file:

```
android/build.gradle
```

Inside the `buildscript` block, add the Google Services classpath under `dependencies`:

```gradle
buildscript {
    repositories {
        google()
        mavenCentral()
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:8.1.0'

        // Add this line
        classpath 'com.google.gms:google-services:4.4.1'
    }
}
```

Example:

![Project-level build.gradle](images/08-build-gradle-project.png)

---

# Step 4: Update App-Level build.gradle

Open the **app-level** Gradle file:

```
android/app/build.gradle
```

At the very **bottom** of the file, apply the Google Services plugin:

```gradle
apply plugin: 'com.google.gms.google-services'
```

Example:

![App-level build.gradle](images/09-build-gradle-app.png)

---

# Step 5: Install Firebase Packages

Open:

```
pubspec.yaml
```

Add the required packages under `dependencies`:

```yaml
dependencies:
  flutter:
    sdk: flutter

  firebase_core: ^3.6.0
```

If you plan to use Push Notifications, also add:

```yaml
  firebase_messaging: ^15.1.3
```

Example:

![pubspec.yaml](images/07-pubspec-yaml.png)

---

# Step 6: Download Dependencies

Run:

```bash
flutter pub get
```

Expected output:

```
Resolving dependencies...
Got dependencies!
```

Example:

![flutter pub get](images/11-pub-get.png)

---

# Step 7: Initialize Firebase in main.dart

Open:

```
lib/main.dart
```

Add the Firebase Core import at the top:

```dart
import 'package:firebase_core/firebase_core.dart';
```

Update the `main()` function to initialize Firebase before running the app:

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Firebase.initializeApp();

  runApp(const MyApp());
}
```

> **Note:** `WidgetsFlutterBinding.ensureInitialized()` must be called before `Firebase.initializeApp()`, otherwise the app will crash on launch.

Example:

![main.dart](images/10-main-dart.png)

---

# Step 8: Run the Application

Run:

```bash
flutter run
```

If everything is configured correctly, your application should launch without errors.

Example:

![Run App](images/12-run-app.png)

---

# Project Structure

Your project should now look like this:

```
lib/
└── main.dart

android/
├── build.gradle              ← Google Services classpath added
└── app/
    ├── google-services.json  ← Firebase config file
    └── build.gradle          ← Google Services plugin applied
```

---

# Firebase Integration Completed

Congratulations! Your Flutter application is now connected to Firebase.

You have successfully:

- Placed `google-services.json` in the correct location
- Applied the Google Services Gradle plugin
- Installed Firebase packages via `pubspec.yaml`
- Initialized Firebase in `main.dart`
- Verified the connection by running the app

---

# Next Step

Continue to **03-FCM.md** to integrate Firebase Cloud Messaging (Push Notifications) into your Flutter application.
