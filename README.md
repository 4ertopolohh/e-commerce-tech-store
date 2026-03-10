# E-Commerce Tech Store

Учебный fullstack-проект интернет-магазина техники с витриной товаров, страницей товара, каталогом, REST API и набором практических задач на фронтенде.

## О проекте

Проект состоит из двух частей:

- `frontend` — React + TypeScript + Vite приложение с многостраничным интерфейсом.
- `backend` — Django + Django REST Framework API с SQLite-базой и админ-панелью.

Основной сценарий: пользователь открывает витрину, выбирает категорию, переходит в каталог, открывает карточку товара и получает полное описание товара из API.

## Что реализовано

### Пользовательская часть (Frontend)

- Главная страница:
  - баннеры и промо-блоки;
  - список категорий из API (`/api/categories/`);
  - мини-каталог с вкладками `New Arrival`, `Bestseller`, `Featured Products`;
  - блок скидок (случайная выборка товаров).
- Каталог:
  - получение товаров из API (`/api/products/`);
  - фильтрация по выбранной категории;
  - сортировка по цене (по возрастанию/убыванию);
  - пагинация.
- Страница товара:
  - загрузка полной информации по товару (`/api/products/<id>/`);
  - выбор цвета и конфигурации памяти;
  - галерея изображений + modal preview;
  - характеристики, условия покупки, секция подробного описания.
- Навигация и UX:
  - хлебные крошки на основе истории навигации (sessionStorage);
  - избранное в карточках (localStorage).

### Практические блоки (страница `/tasks`)

- Случайный цвет: генерация цвета и изменение размеров блока.
- Оформление заказа:
  - валидация ФИО, телефона, email;
  - выбор точки доставки на карте Yandex Maps.
- Таблица товаров:
  - загрузка из локального JSON;
  - фильтрация по диапазону цен;
  - обработка невалидного ввода.
- График загрузки процессора:
  - отрисовка линии с периодическим обновлением;
  - расчет процента ошибок запросов;
  - сейчас используется mock-данные.
- Мини-таблица (Excel-подобная):
  - добавление/удаление строк и столбцов;
  - сохранение содержимого в localStorage.
- Счетчик просмотров:
  - запрос на backend (`/api/visits/`);
  - хранение счетчика в сессии Django.

### Backend / API

- Категории:
  - `GET /api/categories/` — список категорий с иконками.
- Товары:
  - `GET /api/products/` — упрощенный список товаров для каталогов.
  - `POST /api/products/` — создание товара.
  - `GET /api/products/<id>/` — детальная карточка товара.
  - `PUT /api/products/<id>/` — обновление товара.
  - `DELETE /api/products/<id>/` — удаление товара.
- Счетчик:
  - `GET /api/visits/` — счетчик посещений текущей сессии.
- Админ-панель:
  - управление категориями/товарами и связанными сущностями через `/admin/`.

## Технологии

### Frontend

- React 19
- TypeScript
- Vite
- React Router
- SCSS
- Swiper
- Chart.js + react-chartjs-2

### Backend

- Python 3.13+
- Django 6
- Django REST Framework
- SQLite
- Pillow

## Структура проекта

```text
e-commerce-tech-store/
  backend/    # Django API, модели, миграции, media, SQLite
  frontend/   # React-приложение
  docs/       # Документация проекта
```

## Быстрый старт

### 1) Backend

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install Django djangorestframework Pillow
python manage.py migrate
python manage.py runserver 127.0.0.1:8000
```

Backend будет доступен на `http://127.0.0.1:8000`.

### 2) Frontend

В новом терминале:

```powershell
cd frontend
npm ci
npm run dev
```

Frontend будет доступен на `http://127.0.0.1:5173`.

Vite проксирует `/api` на `http://127.0.0.1:8000`, поэтому frontend и backend запускаются раздельно.

## Production-сборка фронтенда

```powershell
cd frontend
npm run build
npm run preview
```

## Полезно знать

- В репозитории уже есть `backend/db.sqlite3` и `backend/media`, поэтому проект стартует с готовыми данными.
- В `index.html` подключен скрипт Yandex Maps API для блока оформления заказа.
- Для backend пока нет `requirements.txt`, зависимости указаны в инструкции запуска выше.

