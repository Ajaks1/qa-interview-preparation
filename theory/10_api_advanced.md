## 10. Тестирование API (углублённо)

### 10.1. Основные концепции API
- **Типы API**: REST, SOAP, GraphQL, gRPC  
- **HTTP методы**: GET (чтение), POST (создание), PUT/PATCH (обновление), DELETE (удаление)  
- **Форматы данных**: JSON, XML, FormData  
- **Коды состояния**: 2xx (успех), 4xx (ошибка клиента), 5xx (ошибка сервера)

### 10.2. Инструменты тестирования
| Категория       | Популярные решения                 |
|-----------------|-----------------------------------|
| Ручное тестирование | Postman, Insomnia, Curl         |
| Автоматизация   | RestAssured, Karate, PyTest      |
| Нагрузочное тестирование | JMeter, k6, Locust          |
| Документирование | Swagger, OpenAPI, Stoplight     |

### 10.3. Валидация ответов
- **JSON Schema** - проверка структуры JSON-ответов  
- **XSD** - валидация XML-документов  
- **Контрактное тестирование** - Pact, OpenAPI  
- **Парсинг ответов**: JSONPath, XPath

### Примеры:
```json
{
  "type": "object",
  "properties": {
    "id": {"type": "integer"},
    "name": {"type": "string"}
  },
  "required": ["id"]
}
```
```xpath
//users/user[age>30]/name
```

### 10.4. Тестирование безопасности
1. **Основные угрозы**:
   - Недостатки аутентификации  
   - Инъекции (SQL, NoSQL)  
   - Небезопасное хранение данных  

2. **Методы проверки**:
   - Анализ токенов доступа  
   - Фаззинг параметров  
   - Проверка CORS-политик
  
```bash
curl -H "Authorization: Bearer invalid_token" https://api.example.com/data
```

### 10.5. Нагрузочное тестирование
**Ключевые аспекты**:
- Планирование сценариев нагрузки  
- Анализ метрик (RPS, latency, error rate)  
- Выявление узких мест  

**Типы тестов**:
- Smoke test  
- Stress test  
- Soak test

```groovy
// JMeter test plan structure
Thread Group {
    HTTP Request {
        Server: api.example.com
        Path: /v1/products
    }
}
```

### 10.6. Интеграция с CI/CD
- Запуск тестов в пайплайнах  
- Артефакты тестирования  
- Уведомления о результатах

```yaml
# GitHub Actions example
- name: Run API tests
  run: |
    pytest tests/api/ --junitxml=report.xml
    newman run collection.json
```

### 10.7. Best Practices
1. **Организация тестов**:
   - Модульная структура  
   - Параметризация данных  
   - Чистые тестовые данные  

2. **Документирование**:
   - Спецификации API  
   - Примеры запросов  
   - Матрица тестирования  

---

📌 _Следующий файл: [11. Тестирование производительности](11_performance_testing.md)_
