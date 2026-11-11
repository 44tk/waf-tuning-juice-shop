# WAF Tuning & Security Assessment: OWASP Juice Shop

Данный репозиторий содержит результаты практической работы по настройке, тестированию и обходу WAF (Web Application Firewall) на базе **ModSecurity v2.9.12** и **OWASP CRS v3.3.8**.

**Целевое приложение:** OWASP Juice Shop (уязвимое SPA-приложение).
**Среда:** Apache 2.4.66 (Ubuntu).

## 🎯 Цели проекта
1. Провести базовый аудит WAF с помощью автоматических сканеров (GoTestWAF, WAF-Bypass).
2. Устранить ложные срабатывания (False Positives) на легитимный трафик.
3. Повысить уровень обнаружения атак (True Positive) за счет включения строгих правил и разработки кастомных сигнатур (Virtual Patching).

## 📊 Результаты (GoTestWAF)

| Метрика | Baseline (PL1) | Итог (PL2 + Custom Rules) |
| :--- | :--- | :--- |
| **Overall Score** | 54.65% | **97.02%** |
| **True Positive (Detection)**| 43.70% | **88.05%** |
| **True Negative (No FP)** | 32.60% | **100.00%** |
| **WAF-Bypass (FP Rate)** | - | **0.09%** |

## 🛠️ Ключевые этапы работы
1. **Анализ ложных срабатываний (FP):** Выявление правил CRS, блокирующих легитимные тексты (RCE, SQLi, XSS). Настройка исключений через `REQUEST_BODY` и `t:urlDecodeUni`.
2. **Устранение обходов (FN):** Написание кастомных правил для блокировки Log4j, Base64-инъекций и SSTI.
3. **Тюнинг ядра:** Увеличение лимитов PCRE и настройка заголовков безопасности (HSTS, X-Frame-Options).
4. **Валидация:** Кросс-проверка с помощью OWASP ZAP, Inoue и WAF-Bypass.

## 📂 Навигация
*   [📚 Методология тестирования](docs/01-methodology.md)
*   [🔧 Решение технических проблем (Troubleshooting)](docs/02-troubleshooting.md)
*   [🛡️ Кастомные правила (Virtual Patching)](docs/03-virtual-patching.md)
*   [⚙️ Итоговый конфиг ModSecurity](configs/custom-exclusions.conf)
