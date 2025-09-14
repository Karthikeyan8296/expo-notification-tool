# Welcome to your Expo notification app - testing on Notification Tool 👋

website - [`expo.dev/notification`](https://expo.dev/notifications)

This is an [Expo](https://expo.dev) project created with [`create-expo-app`](https://www.npmjs.com/package/create-expo-app).

## Get started

1. Install dependencies

   ```bash
   npm install
   ```

2. Start the app

   ```bash
   npx expo start
   ```

In the output, you'll find options to open the app in a

- [development build](https://docs.expo.dev/develop/development-builds/introduction/)
- [Android emulator](https://docs.expo.dev/workflow/android-studio-emulator/)
- [iOS simulator](https://docs.expo.dev/workflow/ios-simulator/)
- [Expo Go](https://expo.dev/go), a limited sandbox for trying out app development with Expo


Working: its basically an app that push notification with expo notification tool!

the user approve the notification on app

logs and print the push token on app

that token is pasted on expo push notification tool website

Send the notification

app/index.tsx - code for the notification approval and getting the notification token

`eas whoami` : login status

`eas init` : to get project it

`npx expo install expo-dev-client` : install dev client

`eas build --platform android --profile development` : take an dev build, after that install the app, now if u run the server it will automatically runs in developement build mode

<img width="715" height="407" alt="image" src="https://github.com/user-attachments/assets/9ed37a3d-b00f-47ab-9bd7-9d84c299c3ab" />

doc: [`https://docs.expo.dev/tutorial/eas/android-development-build/`](https://docs.expo.dev/develop/development-builds/create-a-build/)

After that we need to configure the FCM:
Create Firebase project

Go to Firebase Console

1. Add a new project → add Android app.
   
Enter the package name (com.karthikandroid.exponotificationtool → must match your app.json / app.config.js).

2. Download google-services.json
   
Firebase will give you a google-services.json file.

3. Place it in your project under:
   
android/app/google-services.json

In your app.json add:
```
{
  "expo": {
    "android": {
      "package": "com.karthikandroid.exponotificationtool",
      "googleServicesFile": "./android/app/google-services.json"
    },
    "extra": {
      "eas": {
        "projectId": "YOUR_EAS_PROJECT_ID"
      }
    }
  }
}
```
   OR
   
Place it in your Expo project root (same level as app.json).

Example:
```
expo-notification-tool/
├── app.json
├── App.js
├── google-services.json 
```
Link it in app.json:
```
{
  "expo": {
    "android": {
      "package": "com.karthikandroid.exponotificationtool",
      "googleServicesFile": "./google-services.json"
    }
  }
}
```

After this, Obtain Google Service Account Keys using FCM V1 and paste it on Credentials of your expo project

Project - service account - generate private key - download that and paste it on Credentials on expo.dev

doc: `https://docs.expo.dev/push-notifications/fcm-credentials/`

All done for this, now we can send the notification on expo notication tool, the dev build app will recieve the notification

we have linked our expo project with FCM and if we trigger the notification with token, it sends the request to FCM and then FCM sends that to our App!!!

this is implemented on Android Only!
⚠️Remember: Push notifications only work on real iPhones, not iOS Simulator.


Steps Left for iOS Notifications

1. Go to Expo Dev Dashboard → your project → Credentials → iOS → Push Notifications Key

2. Upload your .p8 file.

3. Enter Key ID and Team ID (from Apple Dev account).

4. Rebuild your iOS app with EAS
```
eas build -p ios
```

(or take a Dev Build if you just want to test).
```
eas build --platform ios --profile development
```

Install on a real iPhone (⚠️ push won’t work in iOS simulator).

5. Run your app → request notification permission → get Expo Push Token → test with Expo Notification Tool.

🎉🎉🎉
