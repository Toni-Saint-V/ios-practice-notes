# iOS заметки: практика, поломки, решения

Рабочая карта по iOS-разработке: SwiftUI, design system, сеть, WebSocket, push, тесты, concurrency, хранение, релизы и реальные поломки. Структура простая: маршруты, основные темы и живые кейсы.

## Как читать
Не читай сверху вниз. Выбери проблему и открой 3–4 заметки подряд, потом один живой кейс.

- Экран показывает старые данные: [SwiftUI state identity effects](<01 SwiftUI и UI/SwiftUI state identity effects.md>) → [Structured Concurrency под нагрузкой](<08 Concurrency/Structured Concurrency под нагрузкой.md>) → [Unit/UI Tests](<04 Тесты CI и релиз/Unit UI Tests для сложных iOS флоу.md>)
- Сеть ведет себя непредсказуемо: [Networking слой без сюрпризов](<02 Сеть и данные/Networking слой без сюрпризов.md>) → [Offline-first](<02 Сеть и данные/Offline-first и консистентность данных.md>) → [WebSocket](<02 Сеть и данные/WebSocket в продакшене.md>)
- Приложение открывается из пуша или deep link: [Push Notifications](<03 Push Deep Links и флаги/Push Notifications в продакшене.md>) → [App Lifecycle Deep Links Navigation](<03 Push Deep Links и флаги/App Lifecycle Deep Links Navigation.md>) → [Feature Flags](<03 Push Deep Links и флаги/Feature Flags и Remote Config.md>)
- UI расползается: [Design System](<01 SwiftUI и UI/Design System для iOS продукта.md>) → [Accessibility](<01 SwiftUI и UI/Accessibility в реальном iOS продукте.md>) → [Модульность без театра](<05 Архитектура и границы/Модульность без театра.md>)
- Релиз вроде зеленый, но доверия нет: [CI без лотереи](<04 Тесты CI и релиз/CI для iOS без лотереи.md>) → [Crash-free не равно stable](<04 Тесты CI и релиз/Crash-free не равно stable.md>) → [Release checklist](<04 Тесты CI и релиз/Release checklist для iOS.md>)

## Быстрый вход
- [Как читать](<00 Навигация/Как читать.md>)
- [iOS карта тем](<00 Навигация/iOS карта тем.md>)
- [Живые кейсы](<09 Живые кейсы/Живые кейсы.md>)

## Основные темы
- [SwiftUI state identity effects](<01 SwiftUI и UI/SwiftUI state identity effects.md>)
- [Design System для iOS продукта](<01 SwiftUI и UI/Design System для iOS продукта.md>)
- [Networking слой без сюрпризов](<02 Сеть и данные/Networking слой без сюрпризов.md>)
- [WebSocket в продакшене](<02 Сеть и данные/WebSocket в продакшене.md>)
- [Push Notifications в продакшене](<03 Push Deep Links и флаги/Push Notifications в продакшене.md>)
- [Unit UI Tests для сложных iOS флоу](<04 Тесты CI и релиз/Unit UI Tests для сложных iOS флоу.md>)
- [Structured Concurrency под нагрузкой](<08 Concurrency/Structured Concurrency под нагрузкой.md>)
- [Offline-first и консистентность данных](<02 Сеть и данные/Offline-first и консистентность данных.md>)
- [Observability для iOS](<06 Производительность и наблюдаемость/Observability для iOS.md>)
- [Security Session Keychain](<07 Безопасность/Security Session Keychain.md>)

## Живые кейсы
- [Пуш открыл приложение раньше навигации](<09 Живые кейсы/Пуш открыл приложение раньше навигации.md>)
- [Поздний ответ поиска перетер новый экран](<09 Живые кейсы/Поздний ответ поиска перетер новый экран.md>)
- [WebSocket зеленый, но данные старые](<09 Живые кейсы/WebSocket зеленый но данные старые.md>)
- [Flaky UI test оказался проблемой с Keychain](<09 Живые кейсы/Flaky UI test оказался проблемой с Keychain.md>)
- [Crash-free зеленый, а flow сломан](<09 Живые кейсы/Crash-free зеленый а flow сломан.md>)

## Проверка себя
После каждой темы задай себе три вопроса:

1. Где это может сломаться в реальном приложении?
2. Какой тест поймает эту поломку?
3. Что должно быть видно в логах, чтобы не гадать по симптомам?
