# 🛡 AmneziaWG Config Analyzer
Лёгкий инструмент для анализа конфигураций AmneziaWG / WireGuard.
Проверяет параметры обфускации, устойчивость к DPI, валидность CPS-пакетов
и даёт конкретные рекомендации как усилить защиту.

Работает полностью в браузере — без серверов и передачи данных.

<p align="center">
  <img src="pic1.png" width="900">
</p>



---

🌐 Онлайн-тест

👉  [Открыть AmneziaWG Analyzer](https://pumbax.github.io/awg-analyzer/)

---

Что нового в v2

- ✅ Глубокий разбор I1-I5 — проверка что CPS начинается с `<b 0x...>`, лимит `<r>` < 1000, детект устаревшего `<c>`
- ✅ Детект 7 протоколов CPS — TLS, DTLS, QUIC v1/v2, SIP, DNS, HTTP, STUN
- ✅ Уровни обфускации — Базовый / +I1 / +I1-I5 полный CPS chain
- ✅ Раздел "Что это за конфиг" — простым языком
- ✅ Раздел "Как усилить" — пошаговый upgrade path с готовыми командами
- ✅ Severity для fixes — CRIT / HIGH / MED / LOW
- ✅ H1-H4 квадранты uint32 — проверка непересечения диапазонов
- ✅ AWG 2.0 лимиты — S2 ≤ 1188, S4 ≤ 32, Jmax < MTU
- ✅ Endpoint = IP (не домен — deadlock на Keenetic)

---

Возможности

- 🔍 Автоопределение версии
  
  - WireGuard
  - AWG 1.0
  - AWG 1.5
  - AWG 2.0 (+ детект уровня обфускации)

- 🧠 Анализ параметров
  
  - Junk packets ("Jc", "Jmin", "Jmax")
  - Handshake padding ("S1–S4")
  - Magic headers ("H1–H4") — в т.ч. диапазоны по квадрантам
  - CPS mimicry ("I1–I5") — разбор каждого тега
  - Endpoint, MTU, DNS, AllowedIPs, Keepalive

- 🧬 Глубокий разбор CPS
  
  - Первый тег должен быть `<b 0x...>` (иначе handshake ломается)
  - `<r N>` строго ≤ 999 байт
  - Детект протокола по hex (TLS, QUIC, DTLS, SIP, DNS, HTTP, STUN)
  - Валидация первого байта под протокол
  - Устаревший тег `<c>` → ErrorCode 1000

- 📊 Оценка безопасности
  
  - Security Score
  - Stealth Score
  - DPI Detection Risk (LOW / MEDIUM / HIGH)
  - Camouflage — качество мимикрии под протокол

- 💡 Рекомендации в два уровня
  
  - 🔧 Что срочно исправить (по severity):
    - CRIT — ломает работу
    - HIGH — снижает защиту
    - MED — DNS leak, узкий Jmin/Jmax
    - LOW — оптимизация
  
  - 🚀 Как усилить защиту (пошаговый upgrade path):
    - Переход WireGuard → AWG
    - Обновление AWG 1.x → 2.0
    - Добавление I1 (базовый CPS)
    - Добавление I2-I5 (полный CPS chain)
    - Смена порта, MTU, H1-H4 диапазонов

---

Безопасность

Analyzer выполняет все вычисления локально.

- нет API-запросов
- нет отправки конфигураций
- нет внешних скриптов
- нет аналитики

Ваши PrivateKey и VPN-конфиги остаются в браузере.

---

Использование

1. Откройте анализатор
2. Вставьте ".conf" файл
3. Нажмите Analyze

или просто перетащите файл на страницу.

Ctrl + Enter → быстрый анализ

---

Для кого

- пользователи AmneziaWG
- администраторы WireGuard
- тестирование DPI обхода
- аудит VPN-конфигураций
- проверка валидности CPS перед использованием

---

Связанные проекты

- [awg2-toolza](https://github.com/pumbaX/awg-multi-script) — менеджер AmneziaWG 2.0 сервера с CPS-генератором
- [AmneziaWG Architect](https://architect.vai-rice.space/) — веб-генератор обфускации

---
## 💰 Поддержать

**Boosty:** https://boosty.to/awgtoolza/donate

| Сеть | Адрес |
|---|---|
| USDT TRC20 | `TN2rQAsGNHQr8wnneKRD14UMX629D2Ca5q` |
| USDT ERC20 | `0x721845234eeC44e0a9BaE78402965828C1bc6c57` |
| USDT TON | `UQCwj-RY2a4BH7sIDDeLb77XRaPDq0mb1FVwyC4UaOGbLMYy` |
| TON | `UQCdQtJO4CF0Lyeb93X2zdeWeAcDJ-ieBC3AaL7LIqWfMBg3` |

---

License

MIT
