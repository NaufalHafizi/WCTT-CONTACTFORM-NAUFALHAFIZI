# Naufal Hafizi

## Getting Started

1. Before you start with anything, please install Flutter in your laptop. Refer [here](https://flutter.dev/docs/get-started/install).
2. Set up an editor. Refer [here](https://flutter.dev/docs/get-started/editor?tab=vscode).
3. Install fvm. Refer [here](https://fvm.app).
- Check `flutterSdkVersion` in `.fvm > fvm_config.json`, and copy the flutter sdk version.
- In terminal, run the following commands in order:
```
fvm install (insert flutter sdk version here)
fvm use (insert flutter sdk version here)
```
- From hereon, add the `fvm` prefix before all flutter terminal commands. Example: `fvm flutter clean`, `fvm flutter pub get`.

## Getx Info

1. Package detail - https://www.youtube.com/watch?v=V0oxG3tWiwk
2. State Management - https://www.youtube.com/watch?v=CNpXbeI_slw&t=644s - Rebuild only specific widget instead of rebuilding whole page
3. Localization - https://www.youtube.com/watch?v=FMAH04VTerk&t=305s
4. Route Management - https://www.youtube.com/watch?v=RaqPIoJSTtI&t=572s - No need context anymore
5. Light/Dark Mode - https://www.youtube.com/watch?v=ar-Ps-_LuWE - better than we rebuilding whole app to get the color again
6. Getx rebounce/interval, avoid DDOS, user spamming and repetitive API call
7. Getx Storage - https://www.youtube.com/watch?v=ViXfhl4dA3w - but since we already have sharedpreferences. I think should be okay. but this one much simpler
8. Middleware - https://www.youtube.com/watch?v=Ism-kh-PXP8

**NOTE**

1. Remember to dispose every controller you declared

## Run The Project

To run this project, you'll have to follow the steps below:

1. Open this project using any IDE (recommend: Visual Studio Code)
2. Connect to a device (iOS / Android) or run Simulator / Emulator
3. Run command below in project terminal for each environment

    Production: 
        `fvm flutter run --flavor production -t lib/main-production.dart --no-sound-null-safety`
        
    Staging: 
        `fvm flutter run --flavor staging -t lib/main-staging.dart --no-sound-null-safety`
        
    Development
        `fvm flutter run --flavor development -t lib/main-development.dart--no-sound-null-safety `

## Setting up Flutter Flavorizr

You will need to run flutter_flavorizr in the following scenarios:
1. When updating app application/bundle id
2. When replacing the existing google-services.json/info.plist file

In `pubspec.yaml`, update the flavor configurations as required. 

After updating app application/bundle ids, run the following command:
`fvm flutter pub run flutter_flavorizr -p ios:xcconfig,ios:buildTargets,ios:schema,ios:plist,android:buildGradle`

After replacing existing google-services.json/info.plist file, run the following command:
`fvm flutter pub run flutter_flavorizr -p google:firebase`
        
Alternatively, you may run both commands both application/bundle ids and firebase config files have been updated.

## Setting up app icons

1. In the project root folder, look out for the files `flutter_launcher_icons-development.yaml`, `flutter_launcher_icons-staging.yaml` and `flutter_launcher_icons-production.yaml`.
2. For each different flavor, check the .yaml and take note of the file paths in `image_path_ios` and `image_path_android`. Locate these files and replace them with the new app icon. 
3. After the app icons have been replaced, run the following commands in the terminal one-by-one:
```
fvm flutter pub run flutter_launcher_icons:main -f flutter_launcher_icons-production.yaml
fvm flutter pub run flutter_launcher_icons:main -f flutter_launcher_icons-staging.yaml
fvm flutter pub run flutter_launcher_icons:main -f flutter_launcher_icons-development.yaml
```

*TODO: Check if it's required to run all 3 commands to update the launcher icons for all 3 flavors, cause ATM it seems like just running one of these commands is enough to replace the icons for all flavors*

## Build Archive (iOS)

Reference: [here](https://flutter.dev/docs/deployment/ios)

For each flavor, repeat the following steps one by one:
1. Run this command in the project terminal (take note of the flavor):
```
fvm flutter build ios --flavor development -t lib/main-development.dart --no-sound-null-safety
fvm flutter build ios --flavor staging -t lib/main-staging.dart --no-sound-null-safety
flutter build ios --flavor production -t lib/main.dart --no-sound-null-safety
```
2. After the building process is complete, open XCode and check that the app version and build have the correct number
3. Change the active scheme to the flavor that is being archived, and make sure to select `Any iOS Device (armv7)` like in the screenshot below
![Xcode Archiving](readme_screenshots/xcode_archiving.png)
4. Proceed to Product > Archive as normal process

**Note!**: Make sure to not change any of the settings manually (e.g. project name, bundle id) or it will cause the configs that have been set up by flavorizr to break!

## Build APK (Android)

Reference: [here](https://flutter.dev/docs/deployment/android)

1. Update the key store path inside android > key.properties (get your local keystore path by dragging the file in Terminal

2. Run this command in project terminal one by one:

```
fvm flutter build apk --flavor production -t lib/main.dart --no-sound-null-safety
fvm flutter build apk --flavor staging -t lib/main-staging.dart --no-sound-null-safety
fvm flutter build apk --flavor development -t lib/main-development.dart --no-sound-null-safety
```

3. Generated APK will be inside <app dir>/build/app/outputs/bundle/release

## Build App Bundle (Android)

As per Play Store's new requirements, new apps are required to be uploaded in app bundle format. 
Follow the steps from the **Build APK (Android)** section, but instead run this command:
```
fvm flutter build appbundle --release --flavor production -t lib/main-production.dart --no-sound-null-safety
```

The generated app bundle will be stored inside <app dir>/build/app/outputs/.

## Other useful commands

1. To run JSON Serializable: `fvm flutter packages pub run build_runner build --delete-conflicting-outputs`


## Contributions

By [Naufal Hafizi](https://naufalhafizi.com/) 2022
