## 🛠️ Быстрый старт

### 1. Установка
```bash
make install
make setup
```

### 2. Настройка окружения
```bash
# Скопируйте env в .env
cp env .env

# Отредактируйте .env файл
BASE_URL=https://virtualtours.qbd.ae/map
HEADLESS=true
```

### 3. Запуск тестов
```bash
# Все тесты
make test

# UI тесты
make test-ui

# API тесты
make test-api
```

## 🔧 Основные команды

| Команда | Описание |
|---------|----------|
| `make test` | Запустить все тесты |
| `make test-ui` | Запустить UI тесты |
| `make test-api` | Запустить API тесты |
| `make report` | Сгенерировать отчет |
| `make clean` | Очистить временные файлы |

## 🌍 Команды для разных окружений

| Команда | Описание |
|---------|----------|
| `make test-dev` | Тесты на DEV окружении |
| `make test-prod` | Тесты на PROD окружении |
| `make test-ui-dev` | UI тесты на DEV окружении |
| `make test-ui-prod` | UI тесты на PROD окружении |

