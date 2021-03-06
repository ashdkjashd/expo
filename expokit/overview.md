<!--- EN-Revision: d34e021e75d3f2d2e3ac68a8959b9bd34ba45b1a -->

ExpoKit - это библиотека Objective-C и Java, которая позволяет вам использовать платформу Expo и ваш существующий проект Expo как часть более крупного стандартного собственного проекта, который вы обычно создаете с помощью Xcode, Android Studio или `react-native init`.

Поскольку Expo уже предоставляет возможность [отображать собственные двоичные файлы для App Store](../distribution/building-standalone-apps/), большинству разработчиков Expo не нужно использовать ExpoKit. В некоторых случаях проекты должны использовать сторонний собственный код Objective-C или Java, который не включен в базовый пакет Expo SDK. ExpoKit предоставляет эту возможность.

Эта документация обсуждается:

- [Извлечение](eject.md) вашего обычного (JS) Expo проекта в JS-и-нативный проект ExpoKit
- [Изменение рабочего процесса](expokit.md) для использования собственного нативного кода с ExpoKit
- Другие [расширенные темы ExpoKit](advanced-expokit-topics.md)
