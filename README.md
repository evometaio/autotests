# 🚀 Autotests - Простая архитектура с POM

Автоматизированное тестирование веб-приложений с использованием Playwright, pytest, Allure и Page Object Model (POM).

## 🏗️ Архитектура

```
autotests/
├── conftest.py              # Основные фикстуры и настройки
├── pages/                   # Page Object Model (POM)
│   ├── __init__.py
│   ├── base_page.py         # Базовый класс для всех страниц
│   └── home_page.py         # Главная страница
├── utils/
│   └── logger.py            # Логирование
├── tests/                    # Тесты
├── Makefile                  # Простые команды
├── requirements.txt          # Минимальные зависимости
├── .env                      # Переменные окружения
└── .github/workflows/        # CI/CD pipeline
    └── cicd.yml             # Автоматизация тестирования
```

## 🛠️ Быстрый старт

### 1. Установка
```bash
make install
make setup
```

### 2. Настройка окружения
```bash
# Скопируйте env.example в .env
cp env.example .env

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

## 📝 Примеры использования

### Тест с использованием POM
```python
def test_homepage_loads(page, base_url):
    home_page = HomePage(page, base_url)
    home_page.open_homepage()
    home_page.check_map_visible()
```

### Тест с базовым URL
```python
def test_page_url(page, base_url):
    page.goto(base_url)
    assert page.url == base_url
```

### Тест с генерацией данных
```python
def test_with_fake_data(fake):
    name = fake.name()
    email = fake.email()
    # Логика теста
```

### Тест с определением окружения
```python
def test_environment_specific(page, current_environment, dev_base_url, prod_base_url):
    if current_environment == "dev":
        url = dev_base_url
    else:
        url = prod_base_url
    
    page.goto(url)
    # Логика теста
```

## ⚙️ Конфигурация

### Переменные окружения (.env)
```bash
# Способ 1: Одна переменная для текущего окружения
BASE_URL=https://virtualtours.qbd.ae/map

# Способ 2: Отдельные переменные для каждого окружения (рекомендуется)
DEV_BASE_URL=https://qube-dev-next.evometa.io/map
PROD_BASE_URL=https://virtualtours.qbd.ae/map

# Настройки браузера
HEADLESS=true
```

### Переключение окружений
```bash
# Через переменные окружения
BASE_URL=https://qube-dev-next.evometa.io/map make test
BASE_URL=https://virtualtours.qbd.ae/map make test

# Через команды make
make test-dev    # тесты на DEV
make test-prod   # тесты на PROD
```

## 📊 Отчеты

```bash
# Генерация отчета
make report

# Запуск сервера с отчетом
make serve
```

Отчет доступен по адресу: http://localhost:8080

## 🚀 CI/CD Pipeline

Проект использует GitHub Actions для автоматизации:

- **Автоматические тесты** при каждом push
- **Генерация Allure отчетов** с историей
- **Деплой на GitHub Pages** для просмотра отчетов
- **Уведомления в Telegram** о результатах тестов
- **Сохранение истории** тестирования

Файл конфигурации: `.github/workflows/cicd.yml`

## 🎉 Преимущества

- **🚀 Простота:** Простая архитектура без избыточности
- **📱 POM:** Правильный Page Object Model
- **🌍 Окружения:** Легкое переключение между DEV/PROD
- **⚡ Производительность:** Нет лишних абстракций
- **🧹 Поддержка:** Легко понимать и изменять
- **📚 Обучение:** Быстро освоить для новых разработчиков
- **🔧 Гибкость:** Все настройки в .env файле
- **🤖 Автоматизация:** CI/CD pipeline для непрерывного тестирования

## 🎯 Ключевые принципы

- **✅ POM:** Правильный Page Object Model
- **✅ Простота:** Без избыточной сложности
- **✅ Фикстуры:** Основные настройки в conftest.py
- **✅ Конфигурация:** Переменные в .env файле
- **✅ Структура:** Четкое разделение ответственности
- **✅ Окружения:** Легкое переключение между DEV/PROD
- **✅ CI/CD:** Автоматизация тестирования

## 🏗️ Page Object Model

### BasePage
```python
class BasePage:
    def __init__(self, page: Page, base_url: str = None)
    def open(self, path: str = "")
    def wait_for_element(self, selector: str, timeout: int = 10000)
    def click(self, selector: str, timeout: int = 10000)
    def fill(self, selector: str, text: str, timeout: int = 10000)
    def get_text(self, selector: str, timeout: int = 10000)
    def is_visible(self, selector: str, timeout: int = 10000)
    def expect_visible(self, selector: str, timeout: int = 10000)
    def wait_for_page_load(self)
```

### HomePage
```python
class HomePage(BasePage):
    def open_homepage(self)
    def check_map_visible(self)
    def check_header_visible(self)
    def check_navigation_visible(self)
    def check_footer_visible(self)
    def check_all_elements(self)
```

---

**Версия:** 6.2.0 (С POM, окружениями и CI/CD)  
**Последнее обновление:** 2024
