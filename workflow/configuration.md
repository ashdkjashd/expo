<!--- EN-Revision: b8b0a3abf088690dabc42f57a4852b3357452c3a -->

`app.json` - это ваше место для настройки частей вашего приложения, которые не принадлежат к коду. Он находится в корне вашего проекта рядом с вашим `package.json`. И выглядит примерно так:

```javascript
{
  "expo": {
    "name": "My app",
    "slug": "my-app",
    "sdkVersion": "UNVERSIONED",
    "privacy": "public"
  }
}
```

`app.json` ранее назывался `exp.json` но для согласованности с [Create React Native App](https://github.com/react-community/create-react-native-app) объединены под одним файлом. Если вы конвертируете свое приложение из `exp.json` в `app.json`, все, что вам нужно сделать, это добавить ключ `" expo "` в корень `app.json`, как родителя всех остальных ключи.

Большая часть конфигурации из `app.json` доступна во время выполнения из вашего кода JavaScript через [`Constants.manifest`](../sdk/constants.md#expoconstantsmanifest). Конфиденциальная информация, такая как секретные ключи, удаляется. Смотите `"extra"` ключ ниже для получения информации о том, как передавать произвольные данные конфигурации в ваше приложение.

## ExpoKit

Хотя некоторые свойства, определенные в `app.json`, могут быть применены во время выполнения, другие требуют изменения собственных файлов конфигурации сборки. Для проектов ExpoKit мы применяем эти настройки только один раз, во время создания собственных проектов (т.е. когда вы запускаете `expo eject`).

Это означает, что для существующих проектов ExpoKit **изменение определенных свойств в `app.json` не даст желаемого эффекта**. Вместо этого вы должны изменить соответствующие собственные файлы конфигурации. В большинстве случаев мы предоставили здесь краткое описание файлов или настроек, которые необходимо изменить, но вы также можете обратиться к документации Apple и Android для получения дополнительной информации.

## Свойства

Ниже приведен список свойств, доступных для вас под ключом `"expo"` в файле `app.json`:

### `"name"`

**Обязательное**. Название вашего приложения в том виде, в котором оно отображается как в Expo, так и на домашнем экране в виде отдельного приложения.

> **ExpoKit**: чтобы изменить имя вашего приложения, отредактируйте поле "Display Name" в Xcode и строку `app_name` в `android/app/src/main/res/values/strings.xml`.

### `"description"`

Краткое описание о вашем приложении и почему оно великолепно.

### `"slug"`

**Обязательное**. Дружественное имя для публикации. Например: `my-app-name` будет ссылаться на проект `expo.io/@your-username/my-app-name`.

### `"privacy"`

Либо `public`, либо `unlisted`. Если не указан, по умолчанию используется `unlisted`. В будущем будет поддерживаться `private`. `unlisted` скрывает опыт от результатов поиска.
Допустимые значения: `public`,` unlisted`

### `"sdkVersion"`

**Обязательное**. Expo sdkVersion для запуска проекта. Должно соответствовать версии, указанной в вашем package.json.

### `"version"`

Версия вашего приложения; используйте любую схему управления версиями, которая вам нравится.

> **ExpoKit**: Чтобы изменить версию вашего приложения, отредактируйте поле "Version" в Xcode и строку `versionName` в `android/app/build.gradle`.

### `"platforms"`

Платформы, которые ваш проект явно поддерживает. Если не указано, по умолчанию `["ios", "android"]`.

### `"githubUrl"`

Если вы хотите поделиться исходным кодом своего приложения на Github, введите здесь URL-адрес хранилища, и он будет связан со страницей вашего проекта Expo.

### `"orientation"`

Зафиксируйте ваше приложение в определенной ориентации с помощью `Portrait` или `Landscape`. По умолчанию нет блокировки.
Допустимые значения: 'default', 'portrait', 'landscape'

### `"primaryColor"`

На Android это будет определять цвет вашего приложения в многозадачном режиме. В настоящее время это не используется на iOS, но может быть использовано в других целях в будущем.

Строка шестнадцатеричного цвета длиной 6 символов, например: "#000000"

### `"icon"`

Локальный путь или удаленный URL к изображению, используемому для значка вашего приложения. Мы рекомендуем использовать файл 1024x1024 png. Этот значок появится на главном экране и в приложении Expo.

> **ExpoKit**: Чтобы изменить значок вашего приложения, отредактируйте или замените файлы в `ios/<ИМЯ ПРОЕКТА>/Assets.xcassets/AppIcon.appiconset` (мы рекомендуем использовать Xcode) и `android/app/src/main/res/mipmap-<Разрешение>`. Обязательно следуйте инструкциям для каждой платформы ([iOS](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/app-icon/), [Android 7.1 и ниже](https://material.io/design/iconography/#icon-treatments) и [Android 8+](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive)) и предоставьте новый значок в каждом существующем размере.

### `"appKey"`

По умолчанию Expo ищет приложение, зарегистрированное в AppRegistry, как `main`. Если вы хотите изменить это, вы можете указать имя в этом свойстве.

### `"androidShowExponentNotificationInShellApp"`

Добавляет уведомление в ваше автономное приложение с кнопкой обновления и отладочной информацией.

### `"scheme"`

**Только автономные приложения**. Схема URL для ссылки в ваше приложение. Например, если мы установим это значение в `'demo'`, тогда URL-адреса demo:// откроют ваше приложение при нажатии. Строка, начинающаяся с буквы, за которой следует любая комбинация букв, цифр, "+", "." or "-"

> **ExpoKit**: Чтобы изменить схему вашего приложения, замените все вхождения старой схемы в `Info.plist`, `AndroidManifest.xml` и `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java`.

### `"entryPoint"`

Относительный путь к вашему основному файлу JavaScript.

### `"extra"`

Любые дополнительные поля, которые вы хотите передать своему опыту. Значения доступны через `Constants.manifest.extra` ([подробнее](../sdk/constants.md#expoconstantsmanifest))

### `"rnCliPath"`

### `"packagerOpts"`

### `"ignoreNodeModulesValidation"`

### `"nodeModulesPath"`

### `"facebookAppId"`

Используется для всех библиотек Facebook. Установите идентификатор приложения Facebook на странице https://developers.facebook.com.

> **ExpoKit**: To change this field, edit `Info.plist`.

### `"facebookDisplayName"`

Используется для родного входа в Facebook.

> **ExpoKit**: To change this field, edit `Info.plist`.

### `"facebookScheme"`

Используется для родного входа в Facebook. Начинается с 'fb' и сопровождается строкой цифр, например, 'fb1234567890'. Вы можете найти свою схему по адресу https://developers.facebook.com/docs/facebook-login/ios в разделе 'Configuring Your info.plist'.

> **ExpoKit**: Чтобы изменить это поле, отредактируйте `Info.plist`.

### `"locales"`

Предоставлять переопределения по локали для системных диалоговых окон, таких как уведомления о разрешениях

> **ExpoKit**: To add or change language and localization information in your iOS app, you need to use Xcode.

### `"assetBundlePatterns"`

Массив строк файлов, которые указывают на ресурсы, которые будут связаны в вашем двоичном файле автономного приложения. Подробнее читайте в [Руководстве по автономной поддержке](../guides/offline-support.md)

### `"androidStatusBar"`

Конфигурация для панели состояния Android.

```javascript
{
  "androidStatusBar": {
    /*
      Настройка значков строки состояния, чтобы был светлый или темный цвет.
      Допустимые значения: "light-content", "dark-content".
    */
    "barStyle": STRING,

    /*
      Конфигурация для панели состояния Android.
      Строка шестнадцатеричного цвета длиной 6 символов, например: "# 000000"
    */
    "backgroundColor": STRING
  }
}
```

### `"splash"`

Конфигурация загрузки и заставки для автономных приложений.

```javascript
{
  "splash": {
    /*
      Цвет для заполнения фона экрана загрузки
      Строка шестнадцатеричного цвета длиной 6 символов, например: "# 000000"
    */
    "backgroundColor": STRING,

    /*
      Определяет, как "image" будет отображаться на экране загрузки заставки.
      Должен быть одним из "cover" или "contain", по умолчанию `contain`.
      Допустимые значения: "cover", "contain"
    */
    "resizeMode": STRING,

    /*
      Локальный путь или удаленный URL к изображению.
      Заполнит фон экрана загрузки/заставки.
      Размер изображения и соотношение сторон зависят от вас. Должно быть .png.
    */
    "image": STRING
  }
}

```

> **ExpoKit**: Чтобы изменить заставку вашего iOS-приложения, используйте Xcode для редактирования `LaunchScreen.xib`. Для Android отредактируйте или замените файлы в `android/app/src/main/res/drawable-<RESOLUTION>`; чтобы изменить цвет фона, отредактируйте `android/app/src/main/res/values/colors.xml`; и чтобы изменить resizeMode, установите `SHOW_LOADING_VIEW_IN_SHELL_APP` в `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java` (`true` для `"contain"`, `false` для `"cover"`).

### `"notification"`

Конфигурация для удаленных (push) уведомлений.

```javascript
{
  "notification": {
    /*
      Локальный путь или удаленный URL к изображению для использования в качестве значка для push-уведомлений.
      96x96 png с оттенками серого с прозрачностью.
    */
    "icon": STRING,

    /*
      Цвет оттенка для изображения push-уведомлений, когда оно появляется в области уведомлений.
      Строка шестнадцатеричного цвета длиной 6 символов, например: "# 000000"
    */
    "color": STRING,

    /*
      Показывать каждое push-уведомление по отдельности "default" или сворачивать в одно "collapse".
      Допустимые значения: "default", "collapse"
    */
    "androidMode": STRING,

    /*
      Если для "androidMode" установлено значение "collapse", этот заголовок используется для свернутого уведомления.
      Например: "#{unread_notifications} новых взаимодействий"
    */
    "androidCollapsedTitle": STRING
  }
}
```

> **ExpoKit**: Чтобы изменить значок уведомления, отредактируйте или замените файлы `shell_notification_icon.png` в `android/app/src/main/res/mipmap-<RESOLUTION>`. В iOS значки уведомлений совпадают со значком приложения. Все остальные свойства устанавливаются во время выполнения.

### `"hooks"`

Конфигурация для запуска скриптов для подключения к процессу публикации

```javascript
{
  "hooks": {
    "postPublish": STRING
  }
}
```

### `"updates"`

Настройка того, как и когда приложение должно запрашивать обновления OTA JavaScript

```javascript
{
  "updates": {
    /*
      Если установлено значение false, ваше автономное приложение никогда не будет загружать какой-либо код.
      И будет использовать только код, связанный локально на устройстве.
      В этом случае все обновления для вашего приложения должны быть отправлены через Apple.
      По умолчанию true.

      Обратите внимание, что это не будет работать из коробки с проектами ExpoKit.
    */
    "enabled": BOOLEAN,

    /*
      По умолчанию Expo будет проверять наличие обновлений при каждой загрузке приложения.
      Установите для этого параметра значение `'ON_ERROR_RECOVERY'`, чтобы отключить автоматическую проверку, если не происходит восстановление после ошибки.

      Должно быть или `ON_LOAD` или `ON_ERROR_RECOVERY`.
    */
    "checkAutomatically": STRING,

    /*
      Как долго (в мс) разрешать получение OTA-обновлений, прежде чем использовать кешированную версию приложения.

      По умолчанию 30000 (30 секунд). Должно быть между 0 и 300000 (5 минут).
    */
    "fallbackToCacheTimeout": NUMBER
  }
}

```

> **ExpoKit**: Чтобы изменить значение `enabled`, отредактируйте `ios/<PROJECT-NAME>/Supporting/EXShell.plist` и `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java`. Все остальные свойства устанавливаются во время выполнения.

### `"ios"`

**Только автономные приложения**. Конфигурация отдельного приложения для iOS

```javascript
{
  "ios": {
    /*
      Идентификатор пакета для вашего автономного приложения для iOS.
      Вы делаете это, но он должен быть уникальным в App Store.

      stackoverflow.com/questions/11347470/what-does-bundle-identifier-mean-in-the-ios-project.

      iOS-идентификатор идентификатора пакета уникальное имя для вашего приложения.
      Например, host.exp.exponent, где exp.host - наш домен
      и Expo это наше приложение.

      ExpoKit: используйте Xcode, чтобы задать это.
    */
    "bundleIdentifier": STRING,

    /*
      Номер сборки для вашего автономного приложения для iOS. Должно быть строка,
      которая соответствует формату Apple для CFBundleVersion.

      developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/20001431-102364.

      ExpoKit: используйте Xcode, чтобы задать это.
    */
    "buildNumber": STRING,

    /*
      Локальный путь или удаленный URL-адрес изображения, чтобы использовать его для значка приложения 
      в iOS. Если указано, это переопределяет ключ "icon" верхнего уровня.

      Используйте значок 1024x1024, который соответствует указаниям интерфейса Apple для значков, включая цветовой профиль и прозрачность.

      Экспо сгенерирует другие необходимые размеры.
      Этот значок появится на главном экране и в приложении Expo.
    */
    "icon": STRING,

    /*
      URL-адрес вашего приложения в Apple App Store, если вы его там развернули.
      Это используется для ссылки на страницу вашего магазина со страницы проекта Expo, если ваше приложение является публичным.
    */
    "appStoreUrl": STRING,

    /*
      Поддерживает ли ваше автономное приложение для iOS размеры экрана планшета.
      По умолчанию `false`.

      ExpoKit: используйте Xcode, чтобы задать это.
    */
    "supportsTablet": BOOLEAN,

    /*
      Если это правда, означает, что ваше автономное приложение для iOS не поддерживает телефоны.
      Ваше приложение будет поддерживать только планшеты.

      ExpoKit: используйте Xcode, чтобы задать это.
    */
    "isTabletOnly": BOOLEAN,

    /*
      Словарь произвольной конфигурации для добавления в собственный Info.plist вашего автономного приложения. Применяется до всех других конкретных Expo-конфигураций.

      Никакая другая проверка не выполняется, поэтому используйте ее на свой страх и риск отклонения из App Store.
    */
    "infoPlist": OBJECT,

    /*
      Массив, который содержит связанные домены для автономного приложения. Смотрите документацию Apple для конфигурации: https://developer.apple.com/documentation/uikit/core_app/allowing_apps_and_websites_to_link_to_your_content/enabling_universal_links
      Записи должны иметь префикс "www."

      ExpoKit: используйте Xcode, чтобы задать это.
    */
    "associatedDomains": ARRAY,

    /*
      Логическое значение, указывающее, использует ли приложение хранилище iCloud для DocumentPicker.
      Смотрите документацию DocumentPicker для деталей.

      ExpoKit: используйте Xcode, чтобы задать это.
    */
    "usesIcloudStorage": BOOLEAN,

    /*
      Дополнительная конфигурация модуля для добавления в собственный Info.plist вашего приложения.

      Для приложений ExpoKit просто добавьте их в файл Info.plist напрямую.
    */
    "config": {
      /*
        Branch (https://branch.io/) ключ для подключения служб ссылок Branch.
      */
      "branch": {
        /*
          Ключ вашего Branch API
        */
        "apiKey": STRING
      },

      /*
        Устанавливает для `ITSAppUsesNonExemptEncryption` в Info.plist автономного ipa указанное логическое значение.
      */
      "usesNonExemptEncryption": BOOLEAN,

      /*
        Ключ Google Maps iOS SDK для вашего автономного приложения.

        developers.google.com/maps/documentation/ios-sdk/start
      */
      "googleMapsApiKey": STRING,

      /*
        Ключи Google SDK для входа в iOS для вашего автономного приложения.

        developers.google.com/identity/sign-in/ios/start-integrating
      */
      "googleSignIn": {
        /*
          Схема URL зарезервированного идентификатора клиента.
          Может быть найден в GoogeService-Info.plist.
        */
        "reservedClientId": STRING
      }
    },

    "splash": {
      /*
        Цвет для заполнения фона экрана загрузки. 6-ти строчная шестнадцатеричная цветная строка, например: "# 000000"
      */
      "backgroundColor": STRING,

      /*
        Определяет, как "image" будет отображаться на экране загрузки заставки.
        Должно быть или "cover" или "contain", по умолчанию "contain".
        Допустимые значения: "cover", "contain"
      */
      "resizeMode": STRING,

      /*
        Локальный путь или удаленный URL к изображению, чтобы заполнить фон экрана загрузки.
        Размер изображения и соотношение сторон зависят от вас.
        Должно быть .png.
      */
      "image": STRING,

      /*
        Локальный путь или удаленный URL к изображению, чтобы заполнить фон экрана загрузки.
        Размер изображения и соотношение сторон зависят от вас.
        Должно быть .png.
      */
      "tabletImage": STRING
    }
  }
}

```

### `"android"`

**Только автономные приложения**. Конфигурация автономного приложения для Android

```javascript
{
  "android": {
    /*
      Название пакета для вашего автономного приложения для Android.
      Вы делаете это, но он должен быть уникальным в магазине Play.

      stackoverflow.com/questions/6273892/android-package-name-convention

      Обратное DNS-обозначение уникальное имя для вашего приложения.
      Например, host.exp.exponent, где exp.host - наш домен, а Expo - наше приложение.
      Имя может содержать только строчные и прописные буквы (a-z, A-Z),
      цифры (0-9) и подчеркивание (_). Каждый компонент имени должен начинаться
      со строчной буквы.

      ExpoKit: это устанавливается в `android/app/build.gradle` так же, как и ваш
      Файл AndroidManifest.xml (несколько мест).
    */
    "package": STRING,

    /*
      Номер версии требуемой Google Play.
      Увеличение на единицу для каждого выпуска.
      Должно быть целым числом.
      developer.android.com/studio/publish/versioning.html

      ExpoKit: устанавливается в `android/app/build.gradle`.
    */
    "versionCode": NUMBER,

    /*
      Локальный путь или удаленный URL к изображению, которое будет использоваться для значка вашего приложения на Android.
      Если указано, это переопределяет ключ "icon" верхнего уровня.

      Мы рекомендуем использовать файл 1024x1024 png.
      Прозрачность рекомендуется для магазина Google Play.
      Этот значок появится на главном экране и в приложении Expo.
    */
    "icon": STRING,

    /*
      Настройки для значка адаптивного запуска на Android.
      https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive

      ExpoKit: значки сохраняются в `android/app/src/main/res/mipmap-<RESOLUTION>-v26`
      и "backgroundColor" устанавливается в `android/app/src/main/res/values/colors.xml`.
    */
    "adaptiveIcon": {
      /*
        Локальный путь или удаленный URL к изображению, используемое, как
        передний план значка вашего приложения на Android.

        Мы рекомендуем вам использовать файл 1024x1024 png,
        оставляя по крайней мере внешнюю 1/6 прозрачной с каждой стороны.
        Если указано, это переопределяет верхний уровень "icon" и "android.icon" ключи.
        Этот значок появится на главном экране.
      */
      "foregroundImage": STRING,

      /*
        Цвет для использования в качестве фона для адаптивного значка вашего приложения на Android.
        По умолчанию белый (#FFFFFF).

        Не имеет эффекта, если "foregroundImage" не указано.
      */
      "backgroundColor": STRING,

      /*
        Локальный путь или удаленный URL к фоновому изображению для
        фона вашего приложения на Android.

        Если указано, это переопределяет ключ "backgroundColor".
        Должен иметь те же размеры, что и "foregroundImage", и не действует, если
        "foregroundImage" не указано.
      */
      "backgroundImage": STRING
    },

    /*
      URL-адрес вашего приложения в Google Play Store, если вы его там развернули.
      Это используется для ссылки на страницу вашего магазина со страницы проекта Expo, если ваше приложение является публичным.
    */
    "playStoreUrl": STRING,

    /*
      Список дополнительных разрешений, которые автономное приложение будет запрашивать при установке, 
      а также минимум, необходимый для работы приложения Expo.

      Чтобы использовать ВСЕ разрешения, поддерживаемые Expo, не указывайте ключ "permissions".

      Чтобы использовать ТОЛЬКО следующие минимально необходимые разрешения и ни одно из дополнений, поддерживаемых 
      Expo, установите для "permissions" значение []. Минимальные необходимые разрешения не требуют 
      Политики конфиденциальности при загрузке в Google Play Store и являются:

      •	получение данные из интернета
      •	просмотр сетевых подключений
      •	полный доступ к сети
      •	изменение настройки звука
      •	рисование поверх других приложений
      •	предотвращение устройства от сна

      Чтобы использовать минимально необходимые разрешения ДОЛЖНО с определенными дополнительными разрешениями, 
      укажите эти дополнения в "permissions", например,

      ["CAMERA", "RECORD_AUDIO"]

      ExpoKit: Чтобы изменить разрешения для запросов вашего приложения, вам нужно отредактировать 
      AndroidManifest.xml вручную. Чтобы приложение не запрашивало одно из 
      разрешений, перечисленных ниже, вам необходимо явно добавить его в `AndroidManifest.xml` 
      вместе с тегом `tools:node="remove"`.
    */
    "permissions": [
      "ACCESS_COARSE_LOCATION",
      "ACCESS_FINE_LOCATION",
      "CAMERA",
      "MANAGE_DOCUMENTS",
      "READ_CONTACTS",
      "READ_CALENDAR",
      "WRITE_CALENDAR",
      "READ_EXTERNAL_STORAGE",
      "READ_PHONE_STATE",
      "RECORD_AUDIO",
      "USE_FINGERPRINT",
      "VIBRATE",
      "WAKE_LOCK",
      "WRITE_EXTERNAL_STORAGE",
      "com.anddoes.launcher.permission.UPDATE_COUNT",
      "com.android.launcher.permission.INSTALL_SHORTCUT",
      "com.google.android.c2dm.permission.RECEIVE",
      "com.google.android.gms.permission.ACTIVITY_RECOGNITION",
      "com.google.android.providers.gsf.permission.READ_GSERVICES",
      "com.htc.launcher.permission.READ_SETTINGS",
      "com.htc.launcher.permission.UPDATE_SHORTCUT",
      "com.majeur.launcher.permission.UPDATE_BADGE",
      "com.sec.android.provider.badge.permission.READ",
      "com.sec.android.provider.badge.permission.WRITE",
      "com.sonyericsson.home.permission.BROADCAST_BADGE"
    ],

    /*
      Расположение файла google-services.json для настройки Firebase. 
      Включение этого ключа автоматически включает FCM в вашем автономном приложении.


      Для приложений ExpoKit добавьте или отредактируйте файл непосредственно в `android/app/google-services.json`.
      Чтобы включить FCM, отредактируйте значение `FCM_ENABLED` в
      `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java`.
    */
    "googleServicesFile": STRING,

    /*
      Дополнительная конфигурация модуля, которая будет добавлена в собственный AndroidManifest.xml вашего приложения.

      Для приложений ExpoKit просто добавьте их непосредственно в файл AndroidManifest.xml.
    */
    "config": {
      /*
        Branch (https://branch.io/) ключ для подключения служб ссылок Branch.
      */
      "branch": {
        /*
          Ключ вашего Branch API
        */
        "apiKey": STRING
      },

      /*
        Ключ Google Developers Fabric для подключения Crashlytics и других сервисов.
        get.fabric.io/
      */
      "fabric": {
        /*
          Ваш ключ Fabric API
        */
        "apiKey": STRING,

        /*
          Ваш секретный ключ Fabric
        */
        "buildSecret": STRING
      },

      /*
        Ключ Google Maps Android SDK для вашего автономного приложения.
        developers.google.com/maps/documentation/android-api/signup
      */
      "googleMaps": {
        /*
          Ваш ключ Google Maps Android SDK API
        */
        "apiKey": STRING
      }

      /*
        Google SDK Android-ключи для вашего автономного приложения.
        developers.google.com/identity/sign-in/android/start-integrating
      */
      "googleSignIn": {
        /*
          Ключ API Android.
          Может быть найден в разделе учетных данных консоли разработчика
          или в "google-services.json"
        */
        "apiKey": STRING,

        /*
          Хэш SHA-1 сертификата подписи, используемого для сборки apk без разделителя `:`.
          Можно найти в "google-services.json".
          developers.google.com/android/guides/client-auth
        */
        "certificateHash": STRING
      }
    },

    /*
      Конфигурация для загрузки и заставки для отдельных приложений Android.
    */
    "splash": {
      /*
        Цвет для заполнения фона экрана загрузки
        Строка шестнадцатеричного цвета длиной 6 символов, например: "# 000000"
      */
      "backgroundColor": STRING,

      /*
        Определяет, как "image" будет отображаться на экране загрузки заставки.
        Должно быть или "cover" или "contain", по умолчанию "contain".
        Допустимые значения: "cover", "contain"
      */
      "resizeMode": STRING,

      /*
        Локальный путь или удаленный URL к изображению, чтобы заполнить фон экрана загрузки в режиме 'cover'.
        Размер изображения и соотношение сторон зависят от вас.
        Обратите особое внимание на размер каждого изображения.
        Посмотреть здесь: https://docs.expo.io/versions/latest/guides/splash-screens.html#differences-between-environments-android
        Должно быть .png
        Для получения дополнительной информации смотрите https://developer.android.com/training/multiscreen/screendensities
      */
      "mdpi": STRING,   // натуральное изображение (базовый уровень)
      "hdpi": STRING,   // масштаб 1.5x
      "xhdpi": STRING,  // масштаб 2x
      "xxhdpi": STRING, // масштаб 3x
      "xxxhdpi": STRING // масштаб 4x
    },

    /*
      Конфигурация для настройки пользовательских фильтров намерений в манифесте Android.
      В следующем примере показано, как настроить глубокие ссылки. Когда
      пользователь нажимает на ссылку, соответствующую *.myapp.io, ему будет показано 
      диалоговое окно с вопросом, должна ли ссылка обрабатываться вашим приложением или 
      веб-браузером.

      Атрибут данных может быть объектом или массивом объектов.
      Объект может иметь следующие ключи для указания атрибутов URL-адресов, сопоставляемых фильтром:

      - scheme (строка): схема URL, например, "HTTPS"
      - host (строка): хост, например "myapp.io"
      - port (строка): порт, например "3000"
      - path (строка): точный путь для URL-адресов, которым должен соответствовать фильтр, например, "/records"
      - pathPattern (строка): регулярное выражение для путей, которые должны соответствовать фильтру, например, "*"
      - pathPrefix (строка): префикс для путей, которым должен соответствовать фильтр, например "/records/" будет соответствовать "/records/123"
      - mimeType (строка): тип MIME для URL, которые должны соответствовать фильтру

      Смотрите документацию Android для более подробной информации о соответствии фильтра намерений:

      developer.android.com/guide/components/intents-filters

      Вы также можете использовать фильтр намерений, чтобы установить приложение в качестве обработчика 
      ссылок по умолчанию (без отображения пользователю диалогового окна с параметрами). Чтобы сделать это, вы 
      должны установить "autoVerify": true для объекта фильтра ниже, а затем 
      настроить свой сервер на обслуживание файла JSON, подтверждающего, что вы являетесь владельцем 
      домена. Подробности смотрите в документации Android:

      developer.android.com/training/app-links

      Чтобы добавить или отредактировать фильтры намерений в проекте ExpoKit, отредактируйте файл AndroidManifest.xml напрямую.
    */
    "intentFilters": [
      {
        "action": "VIEW",
        "data": {
          "scheme": "https",
          "host": "*.myapp.io"
        },
        "category": [
          "BROWSABLE",
          "DEFAULT"
        ]
      }
    ]
  }
}
```
