# Управление питанием платы и raspberry pi

## Что получаем в итоге
- Включение и выключение принтера с кнопки на передней панели
- Настраиваемая световая индикация
- На кнопке включения 3.3V вместо 220V
- Управление принтером через Wi-Fi (ssh)
- Octoprint/Repetier/...

## Необходимые дополнительные компоненты
- блок питания 5V DC или понижайка 24V/5V DC
- Raspberry Pi
- релейный модуль обычный или SSR (бесшумный)
- светодиодная лента WS2812B

## Логика работы

### Включение:
1. включение 220V AC или нажатие кнопки на передней панели -> включения блока питания 5V DC -> загрузка Raspberry Pi 
2. активация выхода GPIO 17 -> включения релейного модуля -> включения модуля Autopower -> включение блока питания 24V DC -> включение платы Lerdge
3. запуск сценария neo_start.py для создания светового эффекта
4. запуск OctoPrint

### Выключение:
1. завершение OctoPrint
2. отпрака по UART команды выключения (M81) плате Lerdge -> выключение платы Lerdge -> выключение модуля Autopower -> выключение блока питания 24V DC
3. запуск сценария neo_off для создания светового эффекта
4. выполнение команды выключения Raspberry Pi