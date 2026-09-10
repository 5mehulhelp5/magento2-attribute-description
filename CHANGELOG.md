# Changelog

## [Unreleased] — fork SISL (2026-09)
- **Forward-compat composer**: zamiast wąskich pinów wersji modułów rdzenia
  (`magento/module-store: 100.2.*|101.0.*|101.1.*`, `module-eav: 101.0.*|102.0.*|102.1.*`,
  `module-catalog: 102.0.*|103.0.*|104.0.*`, `php: ^7.1||^8.0`) moduł wymaga teraz
  `php: ~8.1.0 || … || ~8.5.0` i `magento/framework: >=103.0.4 <104`. Oryginał instalował się na
  2.4.9, ale rozsypałby się na 2.4.10+ przy kolejnym podbiciu wersji modułów.
- Zgodność z Magento **2.4.9 / PHP 8.4** potwierdzona (di:compile + test round-trip zapisu i
  odczytu opisu atrybutu przez ResourceModel na żywej bazie).
- Bez zmian w logice — obserwator, plugin i model działają jak w oryginale.

## Oryginał (dmatthew/magento2-attribute-description)
- Repozytorium **zarchiwizowane** (ostatni commit 2022). Wąskie zależności wersyjne, brak wsparcia dla nowszych wydań.
