<!--- EN-Revision: 939fa35fc91b0ddfc112866d7d1847f6d21ddbf6 -->

**Отказ от ответственности:** Эта функция правильно работает только в macOS.

Это руководство поможет вам загрузить свои автономные приложения Expo в Apple TestFlight и в Google Play.
Вам понадобится платная учетная запись разработчика для каждой платформы, для которой вы хотите загрузить и опубликовать приложение. Вы можете создать учетную запись разработчика Apple на [сайте разработчика Apple](https://developer.apple.com/account/) и учетную запись разработчика Google Play на [странице регистрации в консоли Google Play](https://play.google.com/apps/publish/signup/).

## 1. Создайте автономное приложение

Чтобы узнать, как создавать двоичные файлы, смотрите [Создание автономных приложений](../building-standalone-apps.md) или [Создание автономных приложений на вашем CI](../turtle-cli.md).

## 2. Начните загрузку

Чтобы загрузить ранее построенное автономное приложение в соответствующий магазин приложений, просто запустите `expo upload:android` или ` expo upload:ios`. Тем не менее, у вас есть несколько вариантов выбора двоичного файла приложения, которое вы хотите загрузить (не забудьте выбрать один из них одновременно):
- `--latest` - выбран по умолчанию, загружает последнюю версию сборки для данной платформы, найденную на серверах Expo
- `--id <id>` - загружает сборку с указанным идентификатором
- `--path <path>` - загружает сборку из локальной файловой системы

## 2.1. Если вы решили загрузить свое приложение для Android в Google Play

**Важно:** Вам необходимо создать учетную запись службы Google и загрузить ее закрытый ключ JSON. После этого вам нужно будет создать приложение в [Google Play Console](https://play.google.com/apps/publish/) и загрузить свое приложение хотя бы один раз вручную.

#### Создание учетной записи службы Google

1. Откройте [Google Play Console](https://play.google.com/apps/publish/).
2. Выберите пункт меню **Settings**, а затем **API access**.
3. Нажмите кнопку **CREATE SERVICE ACCOUNT**. Если вы видите сообщение о том, что доступ API к вашей учетной записи не разрешен, вы должны сначала связать свою учетную запись разработчика Google Play с проектом разработчика Google. На этой странице либо свяжите его с существующим проектом, если он у вас есть, либо нажмите **CREATE NEW PROJECT**, чтобы связать его с новым.
4. Перейдите по ссылке **Google API Console** в диалоговом окне.
    1. Нажмите кнопку **CREATE SERVICE ACCOUNT**
    2. Введите имя этой учетной записи в поле "Service account name". Мы рекомендуем имя, которое поможет вам запомнить, что оно относится к вашей учетной записи консоли Google Play. Также введите идентификатор учетной записи службы и описание по вашему выбору.
    3. Нажмите **Select a role** и выберите **Service Accounts > ServiceAccount User**
    4. Отметьте **Furnish a new private key**
    5. Убедитесь, что в поле "Key type" выбран **JSON**
    6. Нажмите **SAVE**, чтобы закрыть окно
    7. Запишите имя файла JSON-файла, загруженного на ваш компьютер. Это понадобится вам для загрузки приложения позже. Обязательно сохраните этот файл JSON в безопасности, поскольку он обеспечивает доступ API к вашей учетной записи разработчика Google Play.
5. Вернитесь на страницу **API access** на **Google Play Console** и убедитесь, что на ней отображается ваша новая учетная запись службы.
6. Нажмите **Grant Access** для новой учетной записи службы
7. Выберите **Release Manager** из новой учетной записи службы
8. Нажмите **ADD USER**, чтобы закрыть диалоговое окно

#### Загрузка приложения в первый раз вручную

Перед использованием `expo-cli` для загрузки автономных сборок приложения вы должны загрузить приложение вручную хотя бы один раз. [Смотрите инструкцию о том, как это сделать.](https://support.google.com/googleplay/android-developer/answer/113469)

#### Использование expo-cli для загрузки дальнейших сборок вашего приложения

После этих шагов вы можете использовать `expo-cli` для загрузки ваших последующих сборок приложений в Google Play.

Чтобы загрузить приложение Android в Google Play, запустите `expo upload:android`. Вы можете установить следующие параметры при загрузке отдельного приложения для Android:
- `--key <key>` **(обязательно)** - путь к ключу JSON, используемому для аутентификации в Google Play Store (создан на предыдущих шагах)
- `--track <track>` - путь к используемому приложению, выберите из: production, beta, alpha, internal, rollout (по умолчанию: internal)

## 2.2. Если вы решите загрузить свое приложение iOS в TestFlight

### Используя expo-cli

Чтобы загрузить приложение iOS в TestFlight, запустите `expo upload:ios`. Вы можете установить следующие параметры при загрузке отдельного приложения для iOS:
- `--apple-id <apple-id>` **(обязательно)** - ваш логин Apple ID. В качестве альтернативы вы можете установить переменную окружения `EXPO_APPLE_ID`.
- `--apple-id-password <apple-id-password>` **(обязательно)** - ваш пароль Apple ID. В качестве альтернативы вы можете установить переменную окружения `EXPO_APPLE_ID_PASSWORD`.
- `--app-name <app-name>` - отображаемое имя вашего приложения будет использоваться для названия приложения в App Store Connect
- `--sku <sku>` - уникальный идентификатор для вашего приложения, который не отображается в App Store, будет создан, если он не указан
- `--language <language>` - основной язык (например, English, German; запустите `expo upload:ios --help` чтобы увидеть список доступных языков) (по умолчанию: English)

### Загрузка приложения вручную

Чтобы увидеть ваше приложение на Testflight, вам сначала необходимо отправить свой файл .IPA в Apple с помощью Application loader. Чтобы сделать это, есть несколько обязательных шагов, которые вы, возможно, не выполнили ранее, если это ваша первая отправка приложения в Apple:

1. Убедитесь, что вы вошли в iTunes connect хотя бы один раз со своим Apple ID и приняли условия.
2. Войдите в https://appleid.apple.com
3. Сгенерируйте пароль для конкретного приложения, выбрав Accounts > Manage > Generate App Specific Password. Запишите этот пароль, так как он понадобится позже.
4. Запустите XCode, но не загружайте ни один проект
5. В меню XCode в строке меню выберите 'Open Developer Tool', а затем 'Application Loader'
6. После запуска Application Loader войдите в систему, используя свой Apple ID и пароль приложения, сгенерированный на шаге 3
7. Следуйте инструкциям, чтобы принять необходимые условия.
8. Как только вы согласитесь со всеми условиями, дважды щелкните по светло-серой панели в центре (над словами 'Deliver Your App').
9. Следуйте инструкциям, чтобы загрузить IPA в Apple.

Вы можете проверить статус отправки приложения в TestFlight в App Store Connect (http://appstoreconnect.apple.com):

1. Войдите в http://appstoreconnect.apple.com с вашим Apple ID и обычным паролем (НЕ ваш пароль конкретного приложения)
2. Выберите 'My Apps', и вы должны увидеть свое приложение в списке.
3. Нажмите 'TestFlight' из строки меню вверху.
4. Покажутся ваши текущие сборки приложения, которые доступны для тестирования.
5. Чтобы протестировать приложение на своем устройстве, вам необходимо установить приложение TestFlight для iOS из App Store и войти в систему, используя свой Apple ID.
