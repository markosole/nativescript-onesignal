# NativeScript-OneSignal
A Nativescript plugin that wraps the iOS and Android OneSignal Push Notifications SDK.

## Contributors

[OneSignal-iOS-SDK](https://github.com/OneSignal/OneSignal-iOS-SDK)

[OneSignal-Android-SDK](https://github.com/OneSignal/OneSignal-Android-SDK)

## Supported Platforms
- iOS 9+ incl 14.2
- Android

## Installation
```bash
tns plugin add nativescript-onesignal
```

### iOS

Enable background notifications and add Push Cotifications in Xcode project.

### Android

Does not need any configuration.

## Usage
### JavaScript and TypeScript

```typescript
var TnsOneSignal = require('nativescript-onesignal').TnsOneSignal
```

### iOS

`TnsOneSignal` is the native iOS `OneSignal` class.

In your `app.js`:

```JavaScript

var TnsOneSignal = require('nativescript-onesignal').TnsOneSignal

if (application.ios) {
        const MyDelegate = (function (_super) {
            __extends(MyDelegate, _super);
            function MyDelegate() {
                _super.apply(this, arguments);
            }
            MyDelegate.prototype.applicationDidFinishLaunchingWithOptions = function (application, launchOptions) {

                console.log("Application data: " + application);
                try {
                    console.log('Onesignal starts here:', TnsOneSignal);
                    TnsOneSignal.initWithLaunchOptions({ kOSSettingsKeyAutoPrompt: true, kOSSettingsKeyInAppLaunchURL: true, kOSSettingsKeyInFocusDisplayOption: 2, kOSSettingsKeyProvidesAppNotificationSettings: true });
                    TnsOneSignal.setAppId("xxxxxxx-xxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxxxxxxxx");

                    // It is important to call this for any user response. Default iOS option (allow and deny) will be provided.
                    TnsOneSignal.promptForPushNotificationsWithUserResponse(funCallback());
                    function funCallback(permission) {
                        console.log("Permission selection callback:" + permission);
                    }

                } catch (error) {
                    console.log("Error: ", error)
                }
                return true;
            };
            MyDelegate.prototype.applicationDidBecomeActive = function (application) {
                console.log("Application is activated: " + application);
            };
            MyDelegate.ObjCProtocols = [UIApplicationDelegate];

            return MyDelegate;
        })(UIResponder);

        application.ios.delegate = MyDelegate;
    }
```

### Android

`TnsOneSignal` is the native Android `com.onesignal.OneSignal` class.

In your `main.ts`:

```typescript
import * as application from 'application';
var TnsOneSignal = require('nativescript-onesignal').TnsOneSignal

if (application.android) {
	application.on(application.launchEvent, function(args: application.ApplicationEventData) {

		try {

			console.dump('TnsOneSignal', TnsOneSignal)
			TnsOneSignal.startInit(application.android.context).init()

		} catch (error) {
			console.error('error', error)
		}

	})
}
```

## API Reference
[iOS API Reference](https://documentation.onesignal.com/docs/ios-sdk-api)

[Android API Reference](https://documentation.onesignal.com/docs/android-sdk-api)

## Typescript Typings

[iOS](https://github.com/roblav96/nativescript-onesignal/blob/master/typings/OneSignal.ios.d.ts)

Android - In the works...

## Demo
```bash
npm run setup
# iOS
npm run demo.ios
# Android
npm run demo.android
```











