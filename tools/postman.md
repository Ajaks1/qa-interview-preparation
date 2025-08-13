# Postman

## Что это и зачем он нужен?
**Postman** — десктопное приложение для ручного и автоматизированного тестирования API (REST и SOAP).  
С его помощью можно отправлять HTTP-запросы, просматривать ответы, писать автоматические проверки и запускать тесты в пакетном режиме.

Postman используют для:
- Проверки работы API без написания кода.
- Поиска и документирования ошибок.
- Автоматизации тестов API.
- Интеграции тестов в CI/CD.

---

## Интерфейс
При первом запуске Postman ты увидишь:

- **Sidebar (слева)** — коллекции, окружения, история запросов.
- **Builder** — область создания запроса.
- **Params** — добавление query-параметров.
- **Headers** — заголовки запроса.
- **Body** — тело запроса (JSON, XML, form-data, x-www-form-urlencoded, raw, binary).
- **Tests** — написание проверок для ответа.
- **Pre-request Script** — скрипты, выполняемые до запроса.
- **Console** — логирование и отладка.

---

## Создание запроса
1. Выбери метод (GET, POST, PUT, DELETE и т.д.).
2. Введи URL API.
3. При необходимости добавь **Params** — они автоматически подставятся в URL.
4. Укажи **Headers**:
    - Content-Type — тип данных (application/json, application/xml и т.д.).
    - Authorization — для токенов доступа.
5. Если метод поддерживает тело запроса (**Body**):
    - Выбери формат (чаще всего raw + JSON).
    - Вставь JSON или другой формат данных.

---

## Ответ на запрос
После отправки Postman отобразит:
- **Status** — HTTP-код ответа (200, 404, 500 и т.д.).
- **Time** — время ответа.
- **Size** — размер данных.
- **Headers** — заголовки ответа.
- **Body** — данные в JSON, XML, HTML или другом формате.
- **Cookies** — куки, установленные сервером.

---

## Переменные и окружения
Postman поддерживает:
- **Global variables** — доступны везде.
- **Environment variables** — для конкретного окружения (dev, test, prod).
- **Collection variables** — для всех запросов в коллекции.
- **Local variables** — внутри одного запроса.

Пример использования:
GET {{base_url}}/users/{{user_id}}

Значения переменных задаются через **Manage Environments**.

---

## Pre-request Script
Скрипты, выполняемые **до отправки запроса**.  
Их используют для генерации случайных данных, установки токенов или подготовки параметров.

Пример:
pm.environment.set("randomEmail", `user_${Date.now()}@test.com`);

---

## Tests (проверки)
Пишутся на JavaScript в разделе **Tests**.

Примеры:
pm.test("Статус 200", () => {
    pm.response.to.have.status(200);
});

pm.test("Время ответа меньше 500мс", () => {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

const jsonData = pm.response.json();
pm.test("Есть поле 'data'", () => {
    pm.expect(jsonData).to.have.property("data");
});

---

## Работа с данными между запросами
Часто нужно передавать значения из одного запроса в другой (например, токен авторизации):

// В тестах запроса логина
const jsonData = pm.response.json();
pm.environment.set("token", jsonData.token);

В следующем запросе:
Authorization: Bearer {{token}}

---

## Авторизация в Postman
Postman поддерживает несколько типов авторизации:

### Bearer Token
1. Вкладка Authorization.
2. Type: Bearer Token.
3. В поле Token вставь значение токена.
4. Можно использовать переменную: {{token}}.

### Basic Auth
1. Вкладка Authorization.
2. Type: Basic Auth.
3. Введи username и password.
4. Данные будут автоматически закодированы в Base64.

### OAuth 2.0
1. Вкладка Authorization.
2. Type: OAuth 2.0.
3. Укажи параметры авторизации (Auth URL, Access Token URL, Client ID, Client Secret и т.д.).
4. Нажми Get New Access Token.
5. При необходимости сохрани токен в переменной окружения.

---

## Автоматизация с Newman
Newman — консольная утилита для запуска коллекций Postman.

Пример запуска:
newman run collection.json -e environment.json

С отчётом:
newman run collection.json -r html --reporter-html-export report.html

---

## Лайфхаки
- Храни токены и пароли в переменных окружения.
- Для массовых проверок используй Collection Runner с CSV/JSON.
- Можно тестировать SOAP — отправь POST с XML в body.
- Используй console.log для отладки.

---

## Частые ошибки
- Проверка только статус-кода без валидации тела.
- Использование глобальных переменных вместо окружений.
- Неочищенные переменные, из-за которых тесты падают.
- Забытые заголовки Content-Type.

---

🔗 [Следующая статья: Newman и интеграция с CI/CD](newman_ci_cd.md)
