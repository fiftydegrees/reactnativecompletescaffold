# React Native up-to-date scaffold project

## _Current React / React Native version: 16.9.0/0.61.5_

This repository hosts a up-to-date React Native project with common libraries and behaviors, such as:

- [React Navigation](https://github.com/react-navigation/react-navigation) to handle routing
- [RNFirebase (Invertase)](https://invertase.io/oss/react-native-firebase/) (includes Firebase Analytics and Messaging) to handle analytics and push notifications
- [react-native-config](https://github.com/luggit/react-native-config) to handle multiple environments
- [React Native FontAwesome](https://github.com/FortAwesome/react-native-fontawesome) to create beautiful UI
- [Axios](https://github.com/axios/axios) to handle HTTP requests
- [MomentJS](https://github.com/moment/moment) to properly handle datime-related issues
- [Fastlane](https://fastlane.tools/) to handle automated builds and CI/CD

## Getting Started

Clone the repository for each new project.

### Basics

Ensure you have the following installed (with latest stable versions available):

- NodeJS / npm
- Xcode and related software development tools
- Android SDK and any Android emulator (or any alternative such as [Genymotion](https://www.genymotion.com/))

Install dependencies via `yarn install` (or `npm install`).

### First Launch

You can run the empty project on iOS and Android with the following commands:

```
$> npm run ios-dev
$> npm run android-dev
```

### Rename project

This is a pain in the ass to rename project files, structure and directories, so I advise not to rename every build files but instead only update package/bundle identifier and app display name.

#### Change package/bundle identifier

Default is `com.rnscaffold`. You can change it by following the steps described in this [StackOverflow answer](https://stackoverflow.com/a/44481467/1809893).

#### Change app display name

##### iOS

Open `ios/rnscaffold/Info.plist` and edit the value associated with `CFBundleDisplayName`.

##### Android

Open `android/app/src/main/res/values/strings.xml` and change the `app_name` string value (default is `RN Scaffold`).

#### Apply changes

Delete the app from the target simulator and re-run `npm run ios-dev` or `npm run android-dev`.

## How To

### React Navigation

The scaffold is completely empty, there's a single view as entry point. You can add your own routing using the included React Navigation library; documentation can be found [here](https://reactnavigation.org/docs/en/getting-started.html).

### Firebase Setup

If you plan to use any of Firebase products, the following steps are mandatory.

#### iOS

Create the Firebase app and add the generated `GoogleService-Info.plist` downloaded ([instructions here](https://invertase.io/oss/react-native-firebase/quick-start/ios-firebase-credentials)).

Open `ios/rnscaffold/AppDelegate.m` and uncomment the following lines:

```
if ([FIRApp defaultApp] == nil) {
  [FIRApp configure];
}
```

_Do not uncomment without adding the config file, this would lead to a mysterious crash on launch._

#### Android

Create the Firebase app and add the generated `google-services.json` downloaded ([instructions here](https://invertase.io/oss/react-native-firebase/quick-start/android-firebase-credentials)).

#### Default Integrations

The scaffold includes Analytics and Messaging integrations. Feel free to add any additional depending on your needs, refer to the library documentation (section _Quick start_ then check if there is any platform-specific configuration step).

### react-native-config usage

This library allows to handle multiple environments. Official documentation can be found [here](https://github.com/luggit/react-native-config).

#### Usage

The scaffold comes with built-in environments: dev, staging and production, and associated npm scripts. You can switch environment using the following:

```
npm run {ios/android}-{dev/staging/production}
```

To use values, simply import the library:

```
import env from  'react-native-config';
<Text>Current env. is: {env.ENVIRONMENT}</Text>
```

You can find an example in `App.js`.

#### Customize

You can edit values in `.env` (development), `.env.staging` (staging) and `.env.production` (production) environment. Default is a single value `ENVIRONMENT` containing the environment name.

#### Switch environment

Each time you want to switch environment, you need to re-run the app from scratch (such as `npm run ios-dev`), not just restart the packager.

### Fastlane Setup

## Troubleshoots

**[iOS] Error 65**
This error can occur in many different situations. The most common fix you would better try first is to completely remove build folder `ios/build`, then re-run `npm run ios-dev`.

**The app crashes on launch without any additional log.**
This may occur when Firebase tries to instantiate but cannot find configuration files. Refer to the related section and check whether config files are loaded as expected.
