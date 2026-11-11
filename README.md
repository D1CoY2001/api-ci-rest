# api-ci-rest

[![Java CI with Gradle](https://github.com/D1CoY2001/api-ci-rest/actions/workflows/gradle.yml/badge.svg)](https://github.com/D1CoY2001/api-ci-rest/actions/workflows/gradle.yml)

Проект для задач №1–2 (настройка CI и проверка JSON Schema) на базе учебного сервиса `app-mbank.jar`.

## Требования

- Java 11+
- Git

## Запуск

1. Запустите учебный сервис (SUT) в отдельном терминале из корня проекта:

   ```bash
   java -jar ./artifacts/app-mbank.jar
   ```

   Сервис будет доступен по адресу `http://localhost:9999`.

   > На Windows с турецкой локалью при необходимости используйте:
   > `java -Duser.language=en -Duser.country=US -jar ./artifacts/app-mbank.jar`

2. Запустите тесты:

   - Linux/macOS/Git Bash:
     ```bash
     ./gradlew test
     ```
   - Windows (cmd/PowerShell):
     ```bat
     gradlew.bat test
     ```

## Проверки

- Автотесты REST Assured проверяют ответы сервиса `GET /api/v1/demo/accounts`.
- `src/test/resources/accounts.schema.json` — JSON Schema для валидации ответа (включая ограничение `currency`: `RUB` или `USD`).
- Тест `MobileBankApiTestV4` выполняет проверку соответствия ответа схеме через `matchesJsonSchemaInClasspath("accounts.schema.json")`.

## CI (GitHub Actions)

Workflow `.github/workflows/gradle.yml` запускается на `push` и `pull_request`: поднимает SUT в фоне, ожидает готовности порта `9999`, запускает тесты и сохраняет отчёты тестов и лог SUT как артефакты (в том числе при сбое).
