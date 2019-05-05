<!--- EN-Revision: 9cca37eb755c609396b1964c56ec87c89bf54138 -->

Ниже приведен краткий справочник по всем модулям Bare Workflow.

Также обязательно загляните на страницу Bare Workflow [Hello World](hello-world.md), чтобы помочь с [установкой Unimodule](hello-world.md#Установка-Unimodule) и [использованием react-native-unimodules](hello-world.md#Использование-react-native-unimodules).

## Поддерживаемые Expo API

```js
// Accelerometer
import { Accelerometer } from 'expo-sensors';

// AdMob
import { AdMobBanner, AdMobInterstitial, AdMobRewarded, PublisherBanner } from 'expo-ads-admob';

// Amplitude
import * as Amplitude from 'expo-analytics-amplitude';

// AppAuth
import { AppAuth } from 'expo-app-auth';

// Asset
import { Asset } from 'expo-asset';

// Audio
import { Audio } from 'expo-av';

// AV
import { Audio, Video } from 'expo-av';

// Barcode Scanner
import { BarCodeScanner } from 'expo-barcode-scanner';

// Barometer
import { Barometer } from 'expo-sensors';

// Blur View
import { BlurView } from 'expo-blur';

// Brightness
import * as Brightness from 'expo-brightness';

// Calendar
import * as Calendar from 'expo-calendar';

// Camera
import { Camera } from 'expo-camera';

// Constants
import Constants from 'expo-constants';

// Contacts
import * as Contacts from 'expo-contacts';

// Device Motion
import { DeviceMotion } from 'expo-sensors';

// Document Picker
import * as DocumentPicker from 'expo-document-picker';

// Facebook
import * as Facebook from 'expo-facebook';

// Face Detector
import * as FaceDetector from 'expo-face-detector';

// File System
import * as FileSystem from 'expo-file-system';

// Font
import * as Font from 'expo-font';

// GL View
import { GLView } from 'expo-gl';

// Gyroscope
import { Gyroscope } from 'expo-sensors';

// Haptics
import * as Haptics from 'expo-haptics';

// Image Manipulator
import * as ImageManipulator from 'expo-image-manipulator';

// Image Picker
import * as ImagePicker from 'expo-image-picker';

// Intent Launcher
import * as IntentLauncher from 'expo-intent-launcher';

// Keep Awake
import KeepAwake from 'expo-keep-awake';

// Linear Gradient
import { LinearGradient } from 'expo-linear-gradient';

// Local Authentication
import * as LocalAuthentication from 'expo-local-authentication';

// Localization
import * as Localization from 'expo-localization';

// Location
import * as Location from 'expo-location';

// Magnetometer
import { Magnetometer } from 'expo-sensors';

// Mail Composer
import * as MailComposer from 'expo-mail-composer';

// Media Library
import * as MediaLibrary from 'expo-media-library';

// Pedometer
import { Pedometer } from 'expo-sensors';

// Permissions
import * as Permissions from 'expo-permissions';

// Print
import { Print } from 'expo-print';

// Secure Store
import * as SecureStore from 'expo-secure-store';

// Segment
import * as Segment from 'expo-analytics-segment';

// Sensors
import {
  Accelerometer,
  Barometer,
  Gyroscope,
  Magnetometer,
  MagnetometerUncalibrated,
  Pedometer,
} from 'expo-sensors';

// SMS
import * as SMS from 'expo-sms';

// Speech
import * as Speech from 'expo-speech';

// SQLite
import { SQLite } from 'expo-sqlite';

// Video
import { Video } from 'expo-av';

// Web Browser
import * as WebBrowser from 'expo-web-browser';
```

## Not Yet Supported Expo APIs

- [AR](../sdk/AR.md)
- [AppLoading](../sdk/app-loading.md)
- [AuthSession](../sdk/auth-session.md)
- [BackgroundFetch](../sdk/background-fetch.md)
- [ErrorRecovery](../sdk/error-recovery.md)
- [Linking](../sdk/linking.md)
- [Notifications](../sdk/notifications.md)
- [ScreenOrientation](../sdk/screen-orientation.md)
- [SplashScreen](../sdk/splash-screen.md)
- [StoreReview](../sdk/storereview.md)
- [TaskManager](../sdk/task-manager.md)
- [Updates](../sdk/updates.md)
