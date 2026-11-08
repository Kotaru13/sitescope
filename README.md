# SiteScope: проект пересдачи по дисциплине «Технология разработки программного обеспечения»

Студент: Иванен М.А., группа РПО-2.

## Требования
- Python 3.11+, зависимости: `pip install -r requirements.txt`
- Docker (для Elasticsearch), ~2 ГБ свободной RAM
- Elasticsearch 8.15.0 (одноузловой режим)

## Запуск (порядок получения результатов)
```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python src/generate_data.py          # data/catalog.jsonl, data/relevance.json (seed=42)
docker compose up -d                 # Elasticsearch на 127.0.0.1:9200
python src/index_data.py             # индекс sitescope-pages, results/index_info.json
python src/search_queries.py         # queries/*.json, results/search_results.json
python src/benchmark.py              # results/benchmark_*.csv, benchmark_plot.png
python src/availability.py           # results/downtime_budgets.csv, incident_report.csv, downtime_budget.png
python src/bathtub.py                # results/bathtub_curve.png
pytest -q                            # тесты (часть про Elasticsearch не требует запущенного сервиса)
```

