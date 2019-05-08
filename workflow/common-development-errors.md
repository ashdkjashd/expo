<!--- EN-Revision: 68b1982bf0d37cb8231cc5e64d0de8e92a7d274d -->

Здесь вы найдете список ошибок, с которыми обычно сталкиваются разработчики, использующие Expo. Для каждой ошибки первый маркер содержит объяснение причины возникновения ошибки, а второй - предложения по отладке. Если есть ошибка, которая, по вашему мнению, относится к этой категории, мы приветствуем и призываем вас [создать PR!](Https://github.com/expo/expo/pulls).

### expo command not found

- Либо у вас не установлен `expo-cli`, либо он неправильно настроен в вашем `$PATH`.

- [Установите expo-cli](../introduction/installation.md), если вы еще этого не сделали. В противном случае проверьте, как установить `$PATH` в зависимости от вашей ОС.

### Metro bundler ECONNREFUSED 127.0.0.1:19001

- Ошибка препятствует соединению с вашим локальным сервером разработки.

- Запустите `rm -rf .expo`, чтобы очистить локальное состояние. Проверьте наличие брандмауэров или [прокси](../introduction/troubleshooting-proxies.md), влияющих на сеть, к которой вы в данный момент подключены.

### Module AppRegistry is not a registered callable module (calling runApplication)

- Ошибка в вашем коде препятствует выполнению пакета JavaScript при запуске.

- Попробуйте запустить `expo start --no-dev --minify`, чтобы локально воспроизвести производственный JS-пакет. Если возможно, подключите свое устройство и получите доступ к журналам устройства через Android Studio или Xcode. Журналы устройств содержат гораздо более подробные трассировки стека и информацию. Проверьте, есть ли у вас какие-либо изменения или ошибки в конфигурации Babel.

### npm ERR! No git binary found in $PATH

- Либо у вас не установлен git, либо он неправильно настроен в вашем `$PATH`.

- [Установите git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), если вы еще этого не сделали. В противном случае проверьте, как установить его в вашем `$PATH` в зависимости от вашей ОС.

### XX.X.X is not a valid SDK version

- Версия SDK, которую вы используете, устарела и больше не поддерживается. 

- [Обновите ваш проект](../workflow/upgrading-expo-sdk-walkthrough.md) до поддерживаемой версии SDK. Если вы используете поддерживаемую версию и видите это сообщение, вам необходимо обновить приложение Expo Client. Если вы столкнулись с этой ошибкой в автономном приложении, убедитесь, что вы опубликовали JS-пакет для конкретной версии SDK и канал выпуска для данного бинарного файла с помощью `expo publish`.