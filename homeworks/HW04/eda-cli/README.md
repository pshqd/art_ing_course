## Обновление 2.0

Небольшое HTTP‑API для **базового анализа CSV‑файлов** в рамках Семинара 04 курса «Инженерия ИИ».  
Весь ранее реализованный CLI‑функционал сохранён без изменений.

## Запуск сервиса

```bash
uv run uvicorn eda_cli.api:app --reload --port 8000
```

Сервис поднимается на `http://127.0.0.1:8000`, документация доступна на `/docs`.

## Эндпоинт: POST `/quality-flags-from-csv`

Принимает CSV‑файл и возвращает оценки качества датасета в виде набора булевых флагов и интегрального скора.

Пример ответа:

```json
{
  "ok_for_model": true,
  "quality_score": 0.7444444444444445,
  "message": "Флаги качества датасета.",
  "latency_ms": 12.142042000050424,
  "flags": {
    "too_few_rows": true,
    "too_many_columns": false,
    "too_many_missing": false,
    "has_suspicious_id_duplicates": false
  },
  "dataset_shape": {
    "n_rows": 36,
    "n_cols": 14
  }
}
```

## Эндпоинт: POST `/sample`

Принимает CSV‑файл и параметр `n`, возвращает случайные `n` строк датасета в JSON‑формате.

Пример ответа:

```json
{
  "rows": [
    {
      "user_id": 1020,
      "country": "BY",
      "city": "Gomel",
      "device": "Desktop",
      "channel": "Ads",
      "sessions_last_30d": 5,
      "avg_session_duration_min": 4.1,
      "pages_per_session": 3,
      "purchases_last_30d": 0,
      "revenue_last_30d": 0,
      "churned": 1,
      "signup_year": 2019,
      "plan": "Free",
      "n_support_tickets": 0
    },
    {
      "user_id": 1008,
      "country": "RU",
      "city": "Moscow",
      "device": "Desktop",
      "channel": "Referral",
      "sessions_last_30d": 34,
      "avg_session_duration_min": 15.2,
      "pages_per_session": 7.1,
      "purchases_last_30d": 4,
      "revenue_last_30d": 6200,
      "churned": 0,
      "signup_year": 2020,
      "plan": "Pro",
      "n_support_tickets": 2
    }
  ],
  "n_rows": 2,
  "n_columns": 14,
  "message": "Случайные 2 строк",
  "latency_ms": 4.211709000173869
}
```