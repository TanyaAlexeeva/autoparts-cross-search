# Autoparts Cross-Search API

Микросервис для поиска аналогов (кроссов) автозапчастей и агрегации цен от нескольких поставщиков за один HTTP-запрос.

## О проекте

**Проблема:** менеджер автомагазина вручную ищет аналоги запчастей и сравнивает цены у поставщиков — это долго и приводит к ошибкам.

**Решение:** один GET-запрос → нормализация артикула → поиск кроссов в БД → параллельный опрос поставщиков → единый JSON-ответ.

**Для кого:** интернет-магазины автозапчастей, B2B-платформы, отделы закупок.

## Возможности

- Нормализация артикулов (регистр, спецсимволы, дефисы).
- Поиск аналогов в локальной SQLite-БД.
- Асинхронный опрос 2 поставщиков (REST + CSV).
- Timeout 1.5 сек, устойчивость к падениям поставщиков.
- Swagger-документация из коробки (`/docs`).
- Покрытие тестами (PyTest + Postman).
- Docker + docker-compose.

## Стек

| Слой | Технология |
|------|-----------|
| Язык | Python 3.11 |
| API | FastAPI + Uvicorn |
| БД | SQLite + SQLAlchemy |
| Асинхронность | asyncio + httpx |
| Валидация | Pydantic v2 |
| Тесты | PyTest, Postman |
| Контейнеры | Docker, docker-compose |
| CI | GitHub Actions |

## Быстрый старт

### Локально

```bash
git clone https://github.com/TanyaAlexeeva/autoparts-cross-search.git
cd autoparts-cross-search

python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

pip install -r requirements.txt

python scripts/seed_db.py

uvicorn mock_supplier1.main:app --port 8001
uvicorn app.main:app --reload --port 8000
```

### Docker

```bash
docker-compose up --build
```

## Пример запроса

```
GET /api/v1/search?article=90919-01253&brand=Toyota
```

## Документация

- [Техническое задание](docs/TECH_SPEC.md)
- Swagger: http://localhost:8000/docs

## Автор

Алексеева Татьяна

GitHub: @TanyaAlexeeva

## Лицензия

MIT
