# Crash-free зеленый а flow сломан

> **Коротко:** Самый неприятный баг — приложение не падает, но пользователь не может закончить сценарий.

## Ситуация
После релиза выросли жалобы на оплату. Crash-free rate был нормальный. В crash dashboard ничего интересного.

Потом нашли: route оплаты часто падал в fallback из-за 403 после изменения backend-правил. Fallback показывал общий текст и не логировался как проблема сценария.

## Что насторожило
- Смотрели только crashes.
- Не было `payment_open_result`.
- Fallback не имел reason code.
- Backend 403 не связывался с mobile flow id.

## Что нужно видеть
| Сигнал | Зачем |
|---|---|
| `flow_id` | собрать цепочку |
| `route` | понять вход |
| `request_id` | найти backend-лог |
| `result` | success/fallback/failure |
| `reason` | почему сценарий не завершился |

## Вывод
Стабильность продукта — это не только отсутствие падений. Критичные flow должны иметь свой success/fallback/failure rate.

Связано: [Crash-free не равно stable](<../04 Тесты CI и релиз/Crash-free не равно stable.md>), [Observability для iOS](<../06 Производительность и наблюдаемость/Observability для iOS.md>), [Release checklist для iOS](<../04 Тесты CI и релиз/Release checklist для iOS.md>)
