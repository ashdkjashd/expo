<!--- EN-Revision: 1daa1d1b562142ae8108d69b1fdb81d17a408d97 -->


React Native включает в себя несколько очень полезных инструментов для разработки: удаленную отладку JavaScript в Chrome, динамическую перезагрузку, горячую перезагрузку и инспектор элементов, похожий на любимый инспектор, который вы используете в Chrome. Он также выполняет множество проверок во время работы вашего приложения, чтобы предупредить вас, если вы используете устаревшее свойство или если вы забыли передать обязательное свойство, например, в компонент.

![Скриншоты режима разработки в действии](https://docs.expo.io/static/images/development-mode.png)

**Это обходится дорого: ваше приложение работает медленнее в режиме разработки.** Вы можете включать и выключать его из Expo Dev Tools и Expo CLI. Когда вы включите его, просто закройте и снова откройте приложение, чтобы изменения вступили в силу. **Каждый раз, когда вы тестируете производительность своего приложения, обязательно отключите режим разработки**.

## Переключение режима разработки в Expo Dev Tools

Чтобы включить режим разработки, убедитесь, что переключатель "Рабочий режим" выключен:

![](https://docs.expo.io/static/images/toggle-development-mode-2.png)

## Переключение режима разработки в Expo CLI

В терминале с вашим проектом, запущенным в Expo CLI, нажмите `p`, чтобы переключить режим производства.

## Отображение меню разработчика

В режиме разработки, в зависимости от настроек клиента Expo, вы либо встряхнете свое устройство, либо нажмете двумя пальцами, чтобы открыть меню разработчика. При использовании эмулятора, используйте клавиши ⌘+D для iOS и Ctrl+M для Android.
