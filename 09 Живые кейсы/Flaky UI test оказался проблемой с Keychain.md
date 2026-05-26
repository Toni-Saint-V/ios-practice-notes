# Flaky UI test оказался проблемой с Keychain

> **Коротко:** Тест падал «иногда», потому что приложение стартовало не с чистой сессии.

## Ситуация
UI-тест авторизации проходил локально и падал на CI. Иногда приложение открывалось сразу внутри аккаунта, хотя тест ожидал экран логина.

Причина оказалась скучной: keychain не чистился между запусками, а `UserDefaults` сбрасывали. Визуально вроде все чисто, но token жил дольше теста.

## Что насторожило
- В `setUp` чистили только user defaults.
- App launch не имел явного `UITEST_MODE`.
- Тест зависел от предыдущего состояния симулятора.

## Фикс
```swift
if ProcessInfo.processInfo.arguments.contains("-uiTestMode") {
    try? keychain.clearAll()
    UserDefaults.standard.removePersistentDomain(
        forName: Bundle.main.bundleIdentifier ?? ""
    )
}
```

Лучше вынести это в тестовый bootstrap, чтобы не размазывать cleanup по тестам.

## Проверка
- Запустить один тест 10 раз подряд.
- Запустить весь suite в другом порядке.
- Запустить на свежем симуляторе.
- Запустить после ручной авторизации.

Связано: [CI для iOS без лотереи](<../04 Тесты CI и релиз/CI для iOS без лотереи.md>), [Unit UI Tests для сложных iOS флоу](<../04 Тесты CI и релиз/Unit UI Tests для сложных iOS флоу.md>), [Security Session Keychain](<../07 Безопасность/Security Session Keychain.md>)
