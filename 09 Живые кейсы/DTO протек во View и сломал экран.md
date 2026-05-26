# DTO протек во View и сломал экран

> **Коротко:** Когда view знает формат backend, UI начинает чинить API прямо в разметке.

## Ситуация
Backend добавил новый статус `payment_pending_review`. Экран бронирования показывал пустое место вместо статуса. Декодинг не упал, но UI не знал, что делать.

Проблема была не только в новом статусе. View напрямую работала с DTO и строковыми статусами.

## Что насторожило
- `switch dto.status` внутри SwiftUI.
- Форматирование цены рядом с layout.
- Fallback для пустого названия отеля в `Text(...)`.

## Как чинить
```swift
enum BookingStatusViewState {
    case draft
    case paid
    case cancelled
    case unsupported(title: String)
}

struct BookingViewState {
    let title: String
    let status: BookingStatusViewState
    let priceText: String
}
```

View должна получать состояние, которое можно прямо показать. Все странности API лучше обработать до UI.

Связано: [DTO mapping и domain models](<../05 Архитектура и границы/DTO mapping и domain models.md>), [SwiftUI state identity effects](<../01 SwiftUI и UI/SwiftUI state identity effects.md>), [Networking слой без сюрпризов](<../02 Сеть и данные/Networking слой без сюрпризов.md>)
