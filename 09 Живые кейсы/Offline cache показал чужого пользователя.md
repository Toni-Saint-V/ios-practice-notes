# Offline cache показал чужого пользователя

> **Коротко:** Кеш без привязки к аккаунту однажды покажет не те данные.

## Ситуация
Пользователь вышел из аккаунта и вошел другим. Сеть была слабая, экран быстро поднял данные из локального кеша. На секунду показались старые бронирования прошлого аккаунта.

Даже если потом экран исправился, доверие уже сломано.

## Что насторожило
- Cache key строился только по endpoint.
- Logout чистил token, но не чистил account-bound storage.
- UI не отличал stale cache от fresh network.

## Лучше так
```swift
struct CacheKey: Hashable {
    let userID: String
    let resource: String
}
```

Для shared данных можно отдельный namespace. Для пользовательских данных key без `userID/sessionID` выглядит опасно.

## Проверка
- login A;
- открыть экран и прогреть кеш;
- logout;
- login B без сети;
- экран не должен показать данные A.

Связано: [Offline-first и консистентность данных](<../02 Сеть и данные/Offline-first и консистентность данных.md>), [Security Session Keychain](<../07 Безопасность/Security Session Keychain.md>), [Persistence + caching strategy](<../02 Сеть и данные/Persistence + caching strategy.md>)
