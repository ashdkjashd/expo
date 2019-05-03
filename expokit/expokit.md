<!--- EN-Revision: 32be97c111ed15cfc42ae32b3508e652db32790d -->

ExpoKit - это библиотека Objective-C и Java, которая позволяет использовать платформу Expo с 
собственным проектом iOS/Android.

## Прежде чем читать это руководство

Чтобы создать проект ExpoKit:

1.  Создайте проект pure-JS с Expo CLI (также будут работать проекты, созданные с помощью exp, XDE или create-react-native-app)
2.  Затем используйте [`expo eject`](eject.md), чтобы добавить ExpoKit (выберите опцию "ExpoKit").

Обязательно выполните эти шаги, прежде чем продолжить это руководство. В оставшейся части руководства предполагается, что вы создали проект ExpoKit.

## Настройка вашего проекта

К этому моменту у вас должно быть приложение JS, которое дополнительно содержит каталоги `ios` и `android`.

### 1. Проверьте JS-зависимости

- `package.json` вашего проекта должен содержать зависимость `react-native`, указывающую на форк React Native от Expo. Это уже должно быть настроено для вас.
- Ваши JS-зависимости уже должны быть установлены (через `npm install` или `yarn`).

### 2. Запустите проект с Expo CLI

Выполните `expo start` из каталога проекта.

Этот шаг гарантирует, что упаковщик React Native работает и обслуживает пакет JS вашего приложения для разработки. Оставьте его запущенным и продолжайте выполнять следующие шаги.

### 3. iOS: Настройка, сборка и запуск

Этот шаг гарантирует, что собственный проект iOS правильно настроен и готов к разработке.

- Убедитесь, что у вас установлена последняя версия Xcode.
- Если у вас его еще нет, установите [CocoaPods](https://cocoapods.org), который является встроенным менеджером зависимостей для iOS.
- Запустите `pod install` из каталога вашего проекта `ios`.
- Откройте файл `xcworkspace` вашего проекта в Xcode.
- Используйте XCode для сборки, установки и запуска проекта на вашем тестовом устройстве или симуляторе. (это произойдет по умолчанию, если вы нажмете большую кнопку "Play" в Xcode.)

После запуска приложение iOS должно автоматически запросить комплект JS из проекта, который вы обслуживаете из Expo CLI.

### 4. Android: сборка и запуск

Откройте каталог `android` в Android Studio, затем соберите и запустите проект на устройстве Android или в эмуляторе.

При открытии проекта Android Studio может предложить вам обновить версию Gradle или других инструментов сборки, но не делайте этого, поскольку вы можете получить неожиданные результаты. ExpoKit всегда поставляется с последними поддерживаемыми версиями всех инструментов сборки.

Если вы предпочитаете использовать командную строку, вы можете запустить `./gradlew installDevKernelDebug` из каталога `android`, чтобы собрать проект и установить его на работающем устройстве/эмуляторе.

После запуска проекта Android он должен автоматически запросить ваш URL-адрес для разработки из Expo CLI. Вы можете разрабатывать свой проект как обычно отсюда.

## Продолжение разработки

Каждый раз, когда вы хотите разрабатывать, убедитесь, что JS вашего проекта обслуживается Expo CLI (шаг 2), затем запустите собственный код из Xcode или Android Studio соответственно.

Ваш проект ExpoKit настроен на загрузку опубликованного URL-адреса вашего приложения при его создании для выпуска. Поэтому, когда вы хотите выпустить его, не забывайте публиковать, как в любом обычном (не ExpoKit) проекте.

## Изменение родных зависимостей

### iOS

Ваш проект ExpoKit управляет своими зависимостями с помощью [CocoaPods](https://cocoapods.org).

Многие библиотеки в экосистеме React Native содержат инструкции по запуску `react-native link`. Они поддерживаются с ExpoKit для iOS.

- Если библиотека поддерживает CocoaPods (имеет файл .podspec), просто следуйте обычным инструкциям и запустите `react-native link`.
- Если библиотека не поддерживает CocoaPods, в `react-native link` может не включаться заголовочные файлы библиотеки. Если вы столкнулись с проблемами сборки, находящими заголовки `<React/*>`, вам может потребоваться вручную добавить `Pods/Headers/Public` в конфигурацию **Header Search Paths** для вашей собственной зависимости в Xcode. Если вы не знакомы с Xcode, поищите в справке Xcode "configure build settings", чтобы понять, как они работают. **Header Search Paths** - это один из таких параметров сборки. Цель, которую вы хотите сконфигурировать - это цель, созданная с помощью `react-native link` внутри вашего проекта XCode. Вы хотите определить относительный путь от вашей библиотеки к `Pods/Headers/Public`.

### Android

Многие библиотеки в экосистеме React Native содержат инструкции по запуску `react-native link`. Они поддерживаются с ExpoKit для Android.

## Обновление ExpoKit

Цикл выпуска ExpoKit соответствует циклу выпуска Expo SDK. Когда выходит новая версия Expo SDK, в примечаниях к выпуску содержатся инструкции по обновлению для обычной части вашего проекта, предназначенной только для JS. Кроме того, вам необходимо обновить собственный код ExpoKit.

> **Примечание:** Пожалуйста, убедитесь, что вы уже обновили свои зависимости JS, прежде чем приступить к выполнению следующих инструкций. Кроме того, могут существовать критические изменения в зависимости от версии, которые здесь не рассматриваются.

### iOS

- Откройте `ios/Podfile` в своем проекте и обновите тег `ExpoKit`, чтобы он указывал на [release](https://github.com/expo/expo/releases), соответствующий вашей версии SDK. Запустите `pod update`, затем `pod install`.
- Откройте в своем проекте `ios/your-project/Supporting/EXSDKVersions.plist` и измените все значения на новую версию SDK.

При обновлении с SDK 31 или ниже вам нужно будет провести рефакторинг вашего класса `AppDelegate`, поскольку мы переместили его связанную с Expo часть в отдельный класс `EXStandaloneAppDelegate `, принадлежащий `ExpoKit`, чтобы максимально упростить будущие процессы обновления. Начиная с SDK 32, ваш класс `AppDelegate` должен иметь подкласс `EXStandaloneAppDelegate`.

Если вы никогда не вносили никаких изменений в ваши файлы `AppDelegate`, сгенерированные в Expo, вы можете просто заменить их новыми файлами шаблонов:

- [AppDelegate.h](https://github.com/expo/expo/blob/master/exponent-view-template/ios/exponent-view-template/AppDelegate.h)
- [AppDelegate.m](https://github.com/expo/expo/blob/master/exponent-view-template/ios/exponent-view-template/AppDelegate.m)

Если вы переопределяете любые методы `AppDelegate` для добавления настраиваемого поведения, вам необходимо либо реорганизовать свой `AppDelegate` для подкласса `EXStandaloneAppDelegate` и при необходимости вызвать методы `super`, либо начать с файлов нового шаблона выше и добавить свою собственную логику (обязательно сохраняйте вызовы `super` методов).

При обновлении с SDK 30 или ниже вам также необходимо изменить `platform: ios, '9.0'` на `platform: ios, '10.0'` в `ios/Podfile`.

### Android

- Перейдите на https://expo.io/--/api/v2/versions и найдите ключ `expokitNpmPackage` в разделе `sdkVersions.[NEW SDK VERSION]`.
- Обновите вашу версию expokit в `package.json` до версии в `expokitNpmPackage` и установите yarn/npm.
- При обновлении до SDK 31 или ниже перейдите к `MainActivity.java` и замените `Arrays.asList("[OLD SDK VERSION]")` на `Arrays.asList("[NEW SDK VERSION]")`. При обновлении до SDK 32 или выше просто удалите весь метод `public List<String> sdkVersions()` из `MainActivity.java`.
- Перейдите в `android/app/build.gradle` и замените `compile('host.exp.exponent:expoview:[OLD SDK VERSION]@aar') {` на `compile('host.exp.exponent:expoview:[NEW SDK VERSION]@aar') {`.

При обновлении с SDK31 или ниже:

1. добавьте следующие строки в `android/app/build.gradle`:
    ```groovy
    api 'host.exp.exponent:expo-app-loader-provider:1.0.0'
    api 'host.exp.exponent:expo-core:2.0.0'
    api 'host.exp.exponent:expo-constants-interface:2.0.0'
    api 'host.exp.exponent:expo-constants:2.0.0'
    api 'host.exp.exponent:expo-errors:1.0.0'
    api 'host.exp.exponent:expo-file-system-interface:2.0.0'
    api 'host.exp.exponent:expo-file-system:2.0.0'
    api 'host.exp.exponent:expo-image-loader-interface:2.0.0'
    api 'host.exp.exponent:expo-permissions:2.0.0'
    api 'host.exp.exponent:expo-permissions-interface:2.0.0'
    api 'host.exp.exponent:expo-sensors-interface:2.0.0'
    api 'host.exp.exponent:expo-react-native-adapter:2.0.0'
    api 'host.exp.exponent:expo-task-manager:1.0.0'
    api 'host.exp.exponent:expo-task-manager-interface:1.0.0'

    // Дополнительные универсальные модули, могут быть удалены
    // вместе со ссылками в MainActivity
    api 'host.exp.exponent:expo-ads-admob:2.0.0'
    api 'host.exp.exponent:expo-app-auth:2.0.0'
    api 'host.exp.exponent:expo-analytics-segment:2.0.0'
    api 'host.exp.exponent:expo-barcode-scanner-interface:2.0.0'
    api 'host.exp.exponent:expo-barcode-scanner:2.0.0'
    api 'host.exp.exponent:expo-camera-interface:2.0.0'
    api 'host.exp.exponent:expo-camera:2.0.0'
    api 'host.exp.exponent:expo-contacts:2.0.0'
    api 'host.exp.exponent:expo-face-detector:2.0.0'
    api 'host.exp.exponent:expo-face-detector-interface:2.0.0'
    api 'host.exp.exponent:expo-font:2.0.0'
    api 'host.exp.exponent:expo-gl-cpp:2.0.0'
    api 'host.exp.exponent:expo-gl:2.0.0'
    api 'host.exp.exponent:expo-google-sign-in:2.0.0'
    api 'host.exp.exponent:expo-local-authentication:2.0.0'
    api 'host.exp.exponent:expo-localization:2.0.0'
    api 'host.exp.exponent:expo-location:2.0.0'
    api 'host.exp.exponent:expo-media-library:2.0.0'
    api 'host.exp.exponent:expo-print:2.0.0'
    api 'host.exp.exponent:expo-sensors:2.0.0'
    api 'host.exp.exponent:expo-sms:2.0.0'
    api 'host.exp.exponent:expo-background-fetch:1.0.0'
    ```
2. Убедитесь, что в файле `MainActivity.java` метод `expoPackages` выглядит следующим образом:
    ```java
    @Override
    public List<Package> expoPackages() {
      return ((MainApplication) getApplication()).getExpoPackages();
    }
    ```
3. В `MainApplication.java`, замените
    ```java
    public class MainApplication extends ExpoApplication {
    ```
    на
    ```java
    public class MainApplication extends ExpoApplication implements AppLoaderPackagesProviderInterface<ReactPackage> {
    ```
4. Добавьте следующие строки в `MainApplication.java`:
    ```java
    import org.unimodules.core.interfaces.Package;
    import expo.loaders.provider.interfaces.AppLoaderPackagesProviderInterface;
    import expo.modules.ads.admob.AdMobPackage;
    import expo.modules.analytics.segment.SegmentPackage;
    import expo.modules.appauth.AppAuthPackage;
    import expo.modules.backgroundfetch.BackgroundFetchPackage;
    import expo.modules.barcodescanner.BarCodeScannerPackage;
    import expo.modules.camera.CameraPackage;
    import expo.modules.constants.ConstantsPackage;
    import expo.modules.contacts.ContactsPackage;
    import expo.modules.facedetector.FaceDetectorPackage;
    import expo.modules.filesystem.FileSystemPackage;
    import expo.modules.font.FontLoaderPackage;
    import expo.modules.gl.GLPackage;
    import expo.modules.google.signin.GoogleSignInPackage;
    import expo.modules.localauthentication.LocalAuthenticationPackage;
    import expo.modules.localization.LocalizationPackage;
    import expo.modules.location.LocationPackage;
    import expo.modules.medialibrary.MediaLibraryPackage;
    import expo.modules.permissions.PermissionsPackage;
    import expo.modules.print.PrintPackage;
    import expo.modules.sensors.SensorsPackage;
    import expo.modules.sms.SMSPackage;
    import expo.modules.taskManager.TaskManagerPackage;

    ...

    public List<Package> getExpoPackages() {
      return Arrays.<Package>asList(
          new CameraPackage(),
          new ConstantsPackage(),
          new SensorsPackage(),
          new FileSystemPackage(),
          new FaceDetectorPackage(),
          new GLPackage(),
          new GoogleSignInPackage(),
          new PermissionsPackage(),
          new SMSPackage(),
          new PrintPackage(),
          new ConstantsPackage(),
          new MediaLibraryPackage(),
          new SegmentPackage(),
          new FontLoaderPackage(),
          new LocationPackage(),
          new ContactsPackage(),
          new BarCodeScannerPackage(),
          new AdMobPackage(),
          new LocalAuthenticationPackage(),
          new LocalizationPackage(),
          new AppAuthPackage(),
          new TaskManagerPackage(),
          new BackgroundFetchPackage()
      );
    }
    ```

При обновлении с SDK 30 или ниже удалите следующие строки из `android/app/build.gradle`:
```groovy
implementation 'com.squareup.okhttp3:okhttp:3.4.1'
implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.4.1'
implementation 'com.squareup.okhttp3:okhttp-ws:3.4.1'
```

При обновлении с SDK 28 или ниже вам также необходимо выполнить следующие инструкции:

- Измените все экземпляры `android\\detach-scripts` и `android/detach-scripts` на `node_modules\\expokit\\detach-scripts` и `node_modules/expokit/detach-scripts` соответственно в `android/app/expo.gradle`.
- И `maven { url "$rootDir/../node_modules/expokit/maven" }` на `allprojects.repositories` в `android/build.gradle`.
- В `android/app/build.gradle`, замените
```groovy
compile('host.exp.exponent:expoview:[SDK VERSION]@aar') {
  transitive = true
}
```
на
```groovy
compile('host.exp.exponent:expoview:[SDK VERSION]@aar') {
  transitive = true
  exclude group: 'com.squareup.okhttp3', module: 'okhttp'
  exclude group: 'com.squareup.okhttp3', module: 'okhttp-urlconnection'
}
```
