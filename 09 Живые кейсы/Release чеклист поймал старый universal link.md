# Release чеклист поймал старый universal link

> **Коротко:** Старые ссылки из писем и пушей живут дольше, чем кажется.

## Ситуация
Перед релизом прогнали новые deep links, все ок. Старый universal link из письма двухмесячной давности открыл пустой экран: path распарсился, но resolver больше не находил нужный объект.

Это не crash, но для пользователя выглядит как сломанное приложение.

## Что добавить в чеклист
- старый link из письма;
- link на удаленный объект;
- link под другим аккаунтом;
- link на выключенную флагом фичу;
- link после logout/login;
- link из killed state.

## Нормальный fallback
Не молчаливый home, а понятное состояние:

> «Эта ссылка больше не открывается. Возможно, объект удален или доступ изменился.»

И рядом действие: открыть список, поддержку или обновить данные.

Связано: [Release checklist для iOS](<../04 Тесты CI и релиз/Release checklist для iOS.md>), [App Lifecycle Deep Links Navigation](<../03 Push Deep Links и флаги/App Lifecycle Deep Links Navigation.md>), [Feature Flags и Remote Config](<../03 Push Deep Links и флаги/Feature Flags и Remote Config.md>)
