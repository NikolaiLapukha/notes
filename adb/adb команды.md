- `adb devices` - список устройств подключенных 
- `adb shell pm list packages` - список установленных приложений
	`adb shell pm list packages | grep "ключевое_слово"` - поиск приложения по названию
	`adb shell pm list packages -s` - список системных приложений
- `adb uninstall имя.пакета` - удаление приложений
	`adb shell pm uninstall --user 0 имя.пакета` - удаление системных приложений
	