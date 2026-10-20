# circleci-lab

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/xsirk/circleci-lab/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/xsirk/circleci-lab/tree/main)

Лабораторная работа №4 по курсу «Разработка и анализ требований» — автоматизация доставки проекта с помощью CircleCI.

## Состав

- `app.py` — функции `add`, `subtract`, `multiply`, `divide`
- `test_app.py` — тесты на pytest
- `requirements.txt` — зависимости (pytest, black)
- `.circleci/config.yml` — конфигурация пайплайна

## Пайплайн

Workflow `build-and-test` запускает два job параллельно:

| Job | Что делает |
|---|---|
| `test` | устанавливает зависимости, запускает `pytest`, сохраняет результаты тестов (JUnit) |
| `lint` | устанавливает зависимости, проверяет форматирование `black --check .` |

Зависимости pip кэшируются по контрольной сумме `requirements.txt` (`restore_cache` / `save_cache`), поэтому повторные сборки идут быстрее. Пайплайн успешен, только если прошли все тесты и проверка стиля.

## Локальный запуск

```bash
pip install -r requirements.txt
pytest -v
black --check .
```
