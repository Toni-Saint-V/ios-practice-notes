# Actor не спас от старой сессии

> **Коротко:** Actor защищает от одновременного доступа, но не понимает, какие данные уже устарели.

## Ситуация
После logout/login иногда появлялись данные старого пользователя. Storage был actor, гонок доступа не было. Но старый запрос завершался позже и аккуратно записывал старый профиль в actor.

Код был потокобезопасный, но доменно неправильный.

## Что насторожило
- После `await` не проверялся session id.
- Actor принимал запись без владельца данных.
- Logout не отменял in-flight задачи.

## Защита
```swift
let sessionID = currentSession.id
let profile = try await api.loadProfile()

guard sessionID == currentSession.id else {
    return
}

await profileStore.save(profile, sessionID: sessionID)
```

Еще лучше, если store сам проверяет session id и не принимает чужую запись.

## Вывод
Потокобезопасность — не то же самое, что корректность состояния.

Связано: [Structured Concurrency под нагрузкой](<../08 Concurrency/Structured Concurrency под нагрузкой.md>), [Security Session Keychain](<../07 Безопасность/Security Session Keychain.md>), [Actors и Sendable](<../08 Concurrency/Actors и Sendable.md>)
