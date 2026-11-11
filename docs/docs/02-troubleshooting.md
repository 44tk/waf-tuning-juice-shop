# Решение технических проблем (Troubleshooting)

В ходе работы возник ряд архитектурных и синтаксических проблем, которые были устранены.

## 1. Ограничения PCRE (PCRE Limits Exceeded)
На запросах с большим телом (128KB) ModSecurity прерывал обработку с ошибкой `Execution error - PCRE limits exceeded (-47)`, возвращая 403 на легитимные запросы.
**Решение:** В глобальном конфиге `modsecurity.conf` лимиты были увеличены:
```apache
SecPcreMatchLimit 1000000
SecPcreMatchLimitRecursion 1000000
