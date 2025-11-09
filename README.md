# JVAPI — простой User API
**Студент:** Моцак И.Д.  
**Группа:** ДБИ-402РСОБ

## Описание проекта
Проект — минимальный REST‑API на FastAPI для управления пользователями. В качестве хранилища используется SQLite (файл `users.db`).

## Структура проекта 
```
JVAPI/
 └ JVAPI/
    └ app/
       ├ main.py        # FastAPI приложение (эндпоинты)
       ├ db.py          # (если есть) работа с БД
       ├ models.py      # SQLAlchemy модели (в этом проекте определён User)
       └ schemas.py     # Pydantic схемы для входа/выхода
```
> В архиве также присутствует виртуальное окружение (Scripts/)

## Сущности
**User**
- `Id` — integer, PK, autoincrement
- `Login` — text, unique
- `PassHash` — text (хранится хэш пароля)

База создаётся автоматически при первом запуске (таблица `User`).

## Запуск проекта 
1. Клонируйте / распакуйте проект и перейдите в корень с `JVAPI/JVAPI`.
2. Рекомендуется создать виртуальное окружение и установить зависимости:
```bash
python -m venv venv
# Linux / macOS
source venv/bin/activate
# Windows (PowerShell)
venv\Scripts\Activate.ps1
pip install fastapi uvicorn
```
> В архиве уже есть папка `Scripts/` 

3. Запустите сервер:
```bash
# из папки, где находится app (где main.py)
uvicorn app.main:app --reload --port 8000
```
4. Откройте в браузере: `http://127.0.0.1:8000/docs` — автоматически сгенерированная документация Swagger UI.

## Основные эндпоинты 
- `GET /users` — получить список всех пользователей.
- `PUT /user/{id}` — обновить пользователя (требует тело с полями `Login` и `PassHash`).
- `DELETE /user/{id}` — удалить пользователя по id.

### Примеры запросов (curl)
Получить всех пользователей:
```bash
curl http://127.0.0.1:8000/users
```

Обновить пользователя id=1 (пример):
```bash
curl -X PUT "http://127.0.0.1:8000/user/1" -H "Content-Type: application/json" -d '{"Login":"newlogin","PassHash":"newpassword"}'
```

Удалить пользователя id=1:
```bash
curl -X DELETE "http://127.0.0.1:8000/user/1"
```
