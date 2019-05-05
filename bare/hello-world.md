<!--- EN-Revision: a07ccb71d1ecf341853101246f37ac2056c45c17 -->

Чтобы начать работу с пустым проектом React Native, запустите `expo init` и выберите один из пустых шаблонов. Мы будем использовать минимальный шаблон здесь. В этом руководстве предполагается, что у вас установлен и работает Xcode и/или Android Studio.

```bash
# Если у вас еще нет expo-cli, установите его
npm i -g expo-cli
# Если у вас еще нет react-native-cli, установите его
npm i -g react-native-cli
# Это ярлык, чтобы пропустить пользовательский интерфейс для выбора шаблона
expo init --template bare-minimum
```

Далее давайте запустим проект. Перейдите в каталог вашего проекта и запустите `react-native run-ios` или `react-native run-android` &mdash; Ура! Ваш проект работает.

## Использование react-native-unimodules

Проекты голых шаблонов поставляются с установленным и настроенным `react-native-unimodules`. Этот пакет предоставляет вам доступ к некоторым обычно полезным API, таким как `Asset`,` Constants`, `FileSystem` и `Permissions`. Вы можете импортировать их из `react-native-unimodules` следующим образом:

```js
import { Asset, Constants, FileSystem, Permissions } from 'react-native-unimodules';
```

## Установка Unimodule

Мы собираемся установить [`expo-web-browser`](https://github.com/expo/expo/tree/master/packages/expo-web-browser), это небольшой полезный пакет для показа модальных веб-браузер, использующий соответствующие нативные API на каждой платформе.

```bash
npm install expo-web-browser
```

Откройте `App.js` и добавьте кнопку, которая при нажатии открывает веб-браузер. Вот код для вас.

```js
import * as React from 'react';
import { Button, View } from 'react-native';
import * as WebBrowser from 'expo-web-browser';

export default class App extends React.Component {
  render() {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Button
          title="Открыть веб-браузер"
          onPress={() => {
            WebBrowser.openBrowserAsync('https://expo.io');
          }}
        />
      </View>
    );
  }
}
```

Это пока не будет работать, потому что мы не связали нативный код, который его поддерживает. Для этого нам нужно следовать инструкциям в [`expo-web-browser` README](https://github.com/expo/expo/tree/master/packages/expo-web-browser) для его настройки для iOS и Android. Давай сделаем это.

### Конфигурация iOS

Сторона iOS самая простая, поэтому давайте сделаем это сначала. Голые проекты инициализируются с помощью [Cocoapods](https://cocoapods.org/), менеджера зависимостей для проектов iOS. Если у вас еще не установлен Cocoapods, [установите его](https://guides.cocoapods.org/using/getting-started.html). Теперь давайте запустим `pod install` в каталоге `ios`. Теперь вы можете снова запустить `react-native run-ios` из корня проекта, и он должен работать как положено!

### Конфигурация Android

Вам не нужно ничего делать, просто запустите проект с помощью `react-native run-android`. Как только приложение будет собрано, нажмите кнопку "Открыть веб-браузер" и посмотрите, как браузер открывается. Успех! Счастливые времена.

## Что теперь?

Большинство API-интерфейсов Expo доступны в голых проектах React Native и могут быть установлены с использованием процесса, очень похожего на описанный выше. Перейдите к разделу `API Reference` и следуйте инструкциям по установке, указанным там, затем прочитайте документацию по API и наслаждайтесь. Удачи в создании вашего приложения!
