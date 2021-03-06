<!--- EN-Revision: 101fce3a8cdf1de0ea67e089d7a174f92db89cd8 -->

Это руководство углубляется в несколько тем [ExpoKit](expokit.md), которые не являются критическими 
прямо из коробки, но которые вы можете встретить в будущем. Если вы не знакомы с 
ExpoKit, вы можете сначала прочитать [руководство по ExpoKit](expokit.md).

## Пере-извлечение

Можно вручную "пере-извлечь" проект, например, если вы хотите вернуться в состояние "только JS", или если вы хотите многократно удалять в целях тестирования. Поскольку ваш проект больше не будет извлечен, вы больше не сможете использовать собственный нативный код.

> **Предупреждение:** Следующие инструкции навсегда удаляют родной код iOS и Android из вашего проекта, включая любые внесенные вами изменения. Мы настоятельно рекомендуем внести ваши изменения в систему контроля версий, прежде чем пытаться это сделать.

Чтобы пере-извлеть:

- Удалите каталоги `ios` и `android` из своего проекта.
- Удалите ключи `isDetached` и `detach` из вашего проекта `app.json`.

Теперь вы можете использовать свой проект как обычный проект Expo (без ExpoKit).

## Проверка пакетов (только для iOS)

Когда мы предоставляем ваш JS по беспроводной связи вашему проекту ExpoKit, мы включаем подпись, чтобы 
ваш проект мог проверить, что JS действительно пришел с наших серверов.

По умолчанию в проектах, использующих ExpoKit, эта функция отключена на iOS и включена на 
Android. Мы рекомендуем вам включить его на iOS, чтобы ваш код был проверен для всех ваших 
пользователей.

Чтобы включить проверку кода в вашем собственном проекте с ExpoKit:

- Выполните одно из этих двух требований (вам нужно только одно):

  - Использовать идентификатор пакета без wildcard знаков при подготовке приложения (рекомендуется)
  - Включите **Keychain Sharing** в настройках проекта XCode в разделе **Capabilities**. (быстрее 
  настроить)

- В `ios/your-project/Supporting/EXShell.plist`, установите `isManifestVerificationBypassed` на
  `NO` (или полностью удалите этот ключ).

## Настройка URL JS

В процессе разработки ваш проект ExpoKit запросит вашу локальную сборку у Expo CLI. Вы можете увидеть эту конфигурацию в `EXBuildConstants.plist` (iOS) или `ExponentBuildConstants` (Android). Вам не нужно редактировать его, потому что он пишется автоматически, когда вы обслуживаете проект.

В процессе производства ваш проект ExpoKit будет запрашивать опубликованный вами пакет JS. Это настраивается в файлах `EXShell.plist` (iOS) и `MainActivity.java` (Android). Если вы хотите указать пользовательское поведение в iOS, вы также можете установить свойство `[ExpoKit sharedInstance].publishedManifestUrlOverride`.

## Изменение схемы Deep Link

Если у вас нет `scheme` указанной в app.json во время извлечения, Expo автоматически сгенерирует для вас случайную схему. Если вы хотите переключиться на другую схему после извлечения, есть несколько мест, где вам нужно найти вхождение вашей старой схемы и заменить ее новой:

1.  `app.json` (поле `"scheme"`)
2.  `ios/<your-project-name>/Supporting/Info.plist` (при первом появлении `CFBundleURLSchemes`)
3.  `android/app/src/main/AndroidManifest.xml` (в линии, которая выглядит как `<data android:scheme="<your-scheme-here>"/>`, под `MainActivity`, или `LauncherActivity` для старых проектов)
4.  `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java` (переменная `SHELL_APP_SCHEME`)

## Включение дополнительных Expo модулей на iOS

Чтобы включить FaceDetector, ARKit или Payments в вашем приложении для iOS, смотрите [Универсальные модули и ExpoKit](universal-modules-and-expokit.md).

## Использование DocumentPicker

В проектах iOS Expokit для правильной работы модуля DocumentPicker требуется разрешение iCloud. Если у вашего приложения его еще нет, вы можете добавить его, открыв проект в Xcode и выполнив следующие действия:

- В проекте перейдите на вкладку `Capabilities`
- Установите переключатель iCloud в положение "включено".
- Установите флажок `iCloud Documents`.

Если все работает правильно, ваш экран должен выглядеть так:

![](https://docs.expo.io/static/images/icloud-entitlement.png)

## Использование Google Maps

Если вы интегрируете Google Карты в приложение ExpoKit с компонентом MapView, вам может потребоваться выполнить дополнительные инструкции, чтобы предоставить свой ключ API Карт Google. Смотрите [Документацию MapView](../sdk/map-view.md).
