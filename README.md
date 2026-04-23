# VK Mini App - магазин игровых услуг

Небольшой, но рабочий VK Mini App для продажи игровых услуг и валюты.  
Проект развивается в продакшене, с живой аудиторией 15000 человек и реальными заказами.

## Что умеет

- создание и сопровождение заказов внутри приложения
- чат по заказу между покупателем и исполнителем
- роли с разными правами: `buyer`, `performer`, `admin`
- биржа заказов для исполнителей
- админ-панель: список заказов, управление пользователями, базовая статистика, KPI
- пуш уведомления во ВКонтакте и интеграция оплаты (Yagoda)

## Технологии

- **Backend:** Go
- **Frontend:** React + VKUI (Vite)
- **Database:** PostgreSQL (Supabase)

## Как устроен проект

- `cmd/server` - точка входа backend
- `internal/db` - работа с БД и бизнес-операции
- `internal/handler` - HTTP-обработчики API
- `internal/broadcast` - модуль массовой и авто-рассылки
- `web` - frontend VK Mini App

## Модуль "Рассылка"

Модуль вынесен в отдельный слой (`scheduler + service + repository`) и работает как самостоятельная подсистема.

Что реализовано:

- импорт базы получателей из `.txt` (один `vk_id` на строку)
- авто-создание/обновление сообщества по `group_id` при импорте
- шаблоны сообщений
- авторассылки по интервалу
- включение/выключение задач
- история запусков (`sent / failed / deactivated`)
- авто-деактивация получателей при фатальных ошибках VK

Основные API:

- `POST /admin/broadcast/import`
- `POST /admin/broadcast/templates`
- `GET /admin/broadcast/templates`
- `POST /admin/broadcast/jobs`
- `GET /admin/broadcast/jobs`
- `PATCH /admin/broadcast/jobs/enabled`
- `GET /admin/broadcast/runs`

Проект активный, ссылка https://vk.com/app54502621
