# Feature flag выключил кнопку но не маршрут

> **Коротко:** Флаг на кнопке не защищает фичу. Он защищает только кнопку.

## Ситуация
Новый экран оплаты выключили через remote config. Кнопка исчезла. Но push и universal link все еще открывали route напрямую.

В итоге часть пользователей попадала в экран, который команда считала выключенным.

## Что насторожило
- Флаг проверялся в SwiftUI view.
- Router не знал про флаг.
- Deep link resolver не имел fallback.

## Правило
Feature flag должен стоять на входе в поведение:

```swift
func resolvePaymentRoute(id: String) async -> RouteResolution {
    guard await flags.isEnabled(.newPaymentFlow) else {
        return .fallback(message: "Оплата пока недоступна")
    }

    return .open(.payment(id: id))
}
```

Тогда кнопку, push и deep link защищает одно правило.

Связано: [Feature Flags и Remote Config](<../03 Push Deep Links и флаги/Feature Flags и Remote Config.md>), [App Lifecycle Deep Links Navigation](<../03 Push Deep Links и флаги/App Lifecycle Deep Links Navigation.md>), [Push Notifications в продакшене](<../03 Push Deep Links и флаги/Push Notifications в продакшене.md>)
