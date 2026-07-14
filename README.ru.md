# Anobisoft Terminal Environment

![Shell](https://img.shields.io/badge/shell-zsh%20%7C%20bash-4acc13?style=flat-square&logo=gnu-bash&logoColor=white)
![OS Compatible](https://img.shields.io/badge/os-macOS%20%7C%20Linux-000000?style=flat-square&logo=apple&logoColor=white)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/Anobisoft/.scripts?style=flat-square&color=blue)
![License](https://img.shields.io/badge/license-MIT-orange?style=flat-square)

Автоматизированная система развертывания и синхронизации минималистичного, высокопроизводительного рабочего окружения на базе **Zsh** и утилит **GNU**. Полностью совместима с **macOS** и популярными дистрибутивами **Linux** (Debian/Ubuntu, Fedora, Arch).

## Основные возможности

*   **GNU Toolchain на macOS:** Автоматическая замена стандартных утилит BSD (`sed`, `awk`, `grep`, `find` и др.) на актуальные версии GNU без принудительного использования префикса `g`.
*   **Динамический промпт-движок (`.prompt`):** Автоматическое обновление времени и статуса Git-репозитория в реальном времени (каждую секунду) без зависаний терминала.
*   **Изоляция потоков (`.functions`):** Функция `hlstderr` для автоматического перехвата, очистки сервисных префиксов и окрашивания потока `STDERR` в ярко-красный цвет.
*   **Профилирование сети (`.curl_templates`):** Набор готовых шаблонов JSON-заголовков и утилит замера таймингов сетевых запросов (DNS-резолв, коннект, старт передачи, общее время).
*   **Системная оптимизация macOS (`config_macOS`):** Автоматическая интеграция ISO-формата дат в логи Xcode, очистка хвостовых пробелов при сохранении кода и блокировка генерации мусорных файлов `.DS_Store` на внешних и сетевых дисках.
*   **Контроль стилей (`.editorconfig`):** Универсальные правила форматирования (Unix-переносы строк `LF`, 4 пробела для табов) с нативной поддержкой в Xcode 16+ и VS Code.

## Структура репозитория

```text
├── .install            # Главный интерактивный скрипт установки окружения (скрыт от случайного запуска)
├── .anobirc            # Ядро инициализации среды (подключается в ~/.zshrc)
├── .alias              # Системные сокращения и утилиты очистки кэша Xcode
├── .functions          # Кастомные функции обработки потоков ввода/вывода
├── .prompt             # Скрипт конфигурации реактивной строки приглашения
├── .curl_templates     # Заготовки и профилировщики сетевых cURL-запросов
├── .vimrc              # Минималистичный конфигурационный файл редактора Vim
├── .editorconfig       # Глобальные правила форматирования кода для IDE
└── once/
    ├── config_macOS    # Скрипт применения твиков системы и Xcode
    └── config_git      # Скрипт глобальной конфигурации параметров Git
```

## Быстрый старт (Установка)

Скрипт развертывания намеренно скрыт, чтобы предотвратить случайный повторный запуск поверх существующего окружения. Для установки по стандартному пути (`~/.scripts`) удаленно из GitHub выполните следующую команду:

```bash
bash <(\curl -sSL https://raw.githubusercontent.com/Anobisoft/.scripts/main/.install) "\$HOME/.scripts"
```

### Кастомный путь установки
Если вы хотите установить скрипты в альтернативную директорию, измените путь в конце аргументов команды:
```bash
bash <(\curl -sSL https://raw.githubusercontent.com/Anobisoft/.scripts/main/.install) "/ваша/кастомная/папка"
```

По окончании работы скрипта примените изменения вручную:
```bash
source ~/.zshrc
```

## Использование ключевых компонентов

### 1. Подсветка ошибок `hlstderr`
Для фильтрации и подсвечивания ошибок любой системной утилиты оберните её вызов в функцию `hlstderr`:
```bash
hlstderr cat /nonexistent/file
```

### 2. Профилирование API `curlog` / `curlapi`
Выполняет запрос с выводом подробной карты таймингов прохождения пакетов по сети:
```bash
# Обычный запрос к JSON API с замером скорости
curlog https://example.com

# Запрос с автоматической динамической авторизацией через \$HEADER_TOKEN
export HEADER_TOKEN="Bearer your_token_here"
curlapi https://example.com
```

### 3. Очистка среды Xcode `xclear` / `killxcode`
*   `xclear` — последовательно и безопасно сносит `DerivedData`, кэш компилятора `Clang` и внутренние кэши Xcode. Использует логический предохранитель для остановки цепочки в случае сбоя.
*   `killxcode` — принудительно собирает PID всех процессов, связанных с Xcode и симуляторами, и уничтожает их пачкой по сигналу `SIGKILL -9` (эффективно против «зомби-процессов»).

## Настройка VS Code

Для того чтобы VS Code корректно применял правила `.editorconfig` и подсвечивал синтаксис файлов конфигурации без расширений, добавьте в настройки вашего проекта (`.vscode/settings.json`) следующие ассоциации:

```json
{
    "files.associations": {
        ".install": "shellscript",
        ".functions": "shellscript",
        ".anobirc": "shellscript",
        ".prompt": "shellscript",
        ".alias": "shellscript",
        ".curl_templates": "shellscript"
    },
    "[shellscript]": {
        "editor.fontFamily": "'JetBrainsMono Nerd Font', 'JetBrains Mono', monospace",
        "editor.fontLigatures": true,
        "editor.fontSize": 13
    }
}
```
*(Для корректного форматирования требуется наличие установленного расширения **EditorConfig for VS Code**).*
