## 13. DevOps для QA

### 13.1. Основные концепции DevOps
- **Культура**: Collaboration между Dev, QA и Ops
- **Автоматизация**: CI/CD пайплайны
- **Мониторинг**: Логи и метрики в production
- **Infrastructure as Code**: Управление окружением через код

### 13.2. CI/CD системы

| Инструмент       | Особенности                          | Использование в QA                  |
|------------------|--------------------------------------|--------------------------------------|
| **Jenkins**      | Гибкость, плагины                    | Запуск автотестов, генерация отчётов |
| **GitLab CI**    | Интеграция с Git, простота YAML      | End-to-end тестирование              |
| **GitHub Actions**| Готовые workflow, marketplace        | Запуск тестов при пул-реквесте       |
| **CircleCI**     | Быстрая настройка, облачный вариант  | Мобильное тестирование               |

#### Пример GitLab CI
```yaml
stages:
  - test

e2e_tests:
  stage: test
  image: cypress/base:12
  script:
    - npm install
    - npx cypress run
  artifacts:
    when: always
    paths:
      - cypress/screenshots/
      - cypress/videos/
```

### 13.3. Контейнеризация

#### Docker
- Изоляция зависимостей тестов
- Быстрое развёртывание тестовых сред
- Пример использования: Запуск Selenium-тестов в контейнере

#### Kubernetes
- Оркестрация тестовых окружений
- Масштабирование нагрузочного тестирования
- Service Mesh для тестирования микросервисов

#### Пример Dockerfile
```dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["pytest", "tests/"]
```

### 13.4. Инфраструктура как код (IaC)
- **Terraform**: Развёртывание тестовых стендов
- **Ansible**: Настройка тестовых окружений
- **Pulumi**: Программируемая инфраструктура

#### Пример Terraform
```hcl
resource "aws_instance" "test_env" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "QA-Test-Environment"
  }
}
```

### 13.5. Мониторинг и логирование
- **Prometheus + Grafana**: Мониторинг метрик тестирования
- **ELK Stack**: Анализ логов тестов
- **Sentry**: Отслеживание ошибок в тестовых прогонах

### 13.6. Полезные практики
1. **Тестирование инфраструктуры**:
   - Security scanning контейнеров
   - Проверка конфигураций Kubernetes

2. **Оптимизация пайплайнов**:
   - Параллельный запуск тестов
   - Кеширование зависимостей

3. **Тестовые данные**:
   - Управление через API
   - Автоматическая очистка

---

📌 _Следующий файл: [14. Тестирование безопасности](14_security.md)_
