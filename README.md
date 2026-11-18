# Time Tracker — OAuth homepage and Privacy Policy

Готовый статический сайт для публичной страницы расширения Chrome **Time Tracker**, в цветах `#06070B`, `#F1BC00`, `#F4F5F8`.

## Страницы

| URL относительно корня сайта | Назначение |
|---|---|
| `/` | Homepage на английском (для Google OAuth verification) |
| `/privacy/` | Privacy Policy на английском |
| `/ru/` | Главная на русском |
| `/ru/privacy/` | Политика на русском |

Сайт не требует сборки, React или npm. В нём нет сторонних JS/CSS, web analytics или рекламных пикселей.

## ВАЖНО — перед публикацией

1. **Обязательно замените `SUPPORT_EMAIL_PLACEHOLDER`** на настоящий email для обращений пользователей. Он встречается в четырех HTML-файлах, в футере и тексте политики. Пример команды для поиска: `grep -R 'SUPPORT_EMAIL_PLACEHOLDER' .`.
2. Прочитайте обе версии Privacy Policy и сравните их с **фактическим** кодом публикуемой версии расширения. Текст подготовлен на основании текущей прямой синхронизации через Google Sheets API, хранения данных в `chrome.storage.local` и авторизации через Chrome Identity API. Если используются аналитика, серверное хранилище, дополнительные API, платёжные сервисы или иные обработчики данных — **обновите политику до публикации**.
3. Убедитесь, что кнопка удаления сессий, доступ к подключённой таблице и отключение аккаунта соответствуют описанию.
4. При необходимости укажите юридическое имя/организацию разработчика. Политика не является юридической экспертизой.
5. Не отправляйте этот сайт на проверку Google с оставленным placeholder: Google требует реальную, специфичную для приложения политику, а не шаблон.

## Публикация через GitHub Pages

### Вариант A: отдельный репозиторий (проще)

1. Создайте публичный репозиторий, например `time-tracker-site`.
2. Скопируйте **содержимое** этой папки в корень репозитория: `index.html`, `privacy/`, `ru/`, `assets/`, `README.md`.
3. Push в ветку `main`.
4. На GitHub: **Settings → Pages → Build and deployment → Deploy from a branch → main → / (root) → Save**.
5. Главная будет доступна примерно как `https://USERNAME.github.io/time-tracker-site/`, а политика — `https://USERNAME.github.io/time-tracker-site/privacy/`.
6. Проверьте обе страницы, включая мобильный браузер. Все ссылки и CSS являются относительными и работают под подпутём репозитория.

### Вариант B: собственный домен (рекомендуется для Google verification)

Для OAuth verification Google требует страницу на подтверждённом домене под вашим контролем. Надёжнее использовать **собственный домен**, например `tracker.yourdomain.com`, а не полагаться на адрес на общем домене `github.io`.

1. В **Settings → Pages → Custom domain** укажите свой домен или поддомен.
2. Настройте DNS (обычно CNAME для поддомена на `USERNAME.github.io`; следуйте инструкциям GitHub для конкретного домена).
3. Включите **Enforce HTTPS**, когда сертификат будет доступен.
4. Добавьте домен в [Google Search Console](https://search.google.com/search-console) и подтвердите владение им (лучше DNS TXT).
5. В **Google Auth Platform → Branding** добавьте домен в `Authorized domains`, укажите `Application home page` и `Application privacy policy link` на том же домене.
6. В **Google Auth Platform → Verification Center** завершите настройки верификации чувствительного scope `https://www.googleapis.com/auth/spreadsheets`.

Пример окончательных URL (замените на собственные):

- Homepage: `https://tracker.yourdomain.com/`
- Privacy: `https://tracker.yourdomain.com/privacy/`

**Важно:** переход `Audience → In production` устраняет режим только-тестировщиков, но не означает автоматически успешную проверку Google. Для широкого доступа со scope `spreadsheets` потребуется OAuth verification. Отдельная ошибка `bad client id` решается соответствием OAuth Client/Extension ID и не зависит от сайта.

## Быстрая локальная проверка

```sh
cd time-tracker-oauth-site
python3 -m http.server 8080
```

Откройте `http://localhost:8080/` и `http://localhost:8080/privacy/`.

## Источники требований

- [Google: OAuth app verification requirements](https://support.google.com/cloud/answer/13464321?hl=en)
- [Google: App Privacy Policy](https://support.google.com/cloud/answer/13806988?hl=en)
- [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy)
- [Chrome Web Store Limited Use](https://developer.chrome.com/docs/webstore/program-policies/limited-use)
- [GitHub Docs — Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
