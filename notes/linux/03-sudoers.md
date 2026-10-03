# 03 — /etc/sudoers и granular permissions

## Цель
Настроить ограниченный sudo-доступ для роли plc_operator:
разрешить только перезапуск конкретного сервиса.

## Команды
sudo visudo

## Правило
plc_operator ALL=(ALL) /usr/bin/systemctl restart modbus-simulator

## Ошибка и решение
Забыл скобки вокруг второго ALL:
  plc_operator ALL=ALL /usr/bin/systemctl ...   ← syntax error
Исправлено на:
  plc_operator ALL=(ALL) /usr/bin/systemctl ...

visudo поймал ошибку до сохранения — защита от поломки sudo
для всей системы (в отличие от редактирования файла напрямую).

## OT-контекст
Оператор смены получает право перезапускать только сервис
симулятора Modbus, без доступа к остальной системе.
