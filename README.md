# CapsSwitch

Простой Swift проект для macOS разработки.

## Описание

Это базовый Swift проект, созданный как стартовая точка для разработки приложений на macOS. Проект включает в себя минимальную структуру и настройки для быстрого начала работы.

## Структура проекта

```
caps-switch/
├── Sources/
│   └── main.swift          # Основной файл приложения
├── Package.swift           # Манифест Swift Package Manager
├── .gitignore             # Игнорируемые Git файлы
├── .vscode/               # Настройки VS Code
│   └── tasks.json         # Задачи для сборки и запуска
└── README.md              # Этот файл
```

## Требования

- macOS 11.0 или выше
- Swift 5.8 или выше
- Xcode Command Line Tools

## Установка инструментов разработки

```bash
# Установка Xcode Command Line Tools (если еще не установлены)
xcode-select --install
```

## Сборка и запуск

### Через терминал:

```bash
# Сборка проекта
swiftc Sources/main.swift -o caps-switch

# Запуск
./caps-switch
```

### Через VS Code:

1. Откройте палитру команд (Cmd+Shift+P)
2. Выберите "Tasks: Run Task"
3. Выберите одну из задач:
   - "Build Swift Project" - для сборки
   - "Run Swift Project" - для сборки и запуска

## Разработка

Основной код находится в файле `Sources/main.swift`. Вы можете:

1. Редактировать код в VS Code
2. Использовать встроенные задачи для сборки и запуска
3. Добавлять новые Swift файлы в папку `Sources/`

## Добавление зависимостей

Для добавления внешних библиотек отредактируйте `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/apple/swift-argument-parser.git", from: "1.0.0")
],
targets: [
    .executableTarget(
        name: "CapsSwitch",
        dependencies: [
            .product(name: "ArgumentParser", package: "swift-argument-parser")
        ]
    )
]
```

## Дополнительные ресурсы

- [Swift.org](https://swift.org/) - Официальный сайт Swift
- [Swift Package Manager](https://swift.org/package-manager/) - Документация по SPM
- [Swift на macOS](https://developer.apple.com/swift/) - Apple Developer

## Лицензия

Этот проект создан для обучения и может свободно использоваться.