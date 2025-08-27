# LiveChat - Notification Server

<div align="center">

![Kotlin](https://img.shields.io/badge/Kotlin-1.9.21-blue?logo=kotlin)
![Ktor](https://img.shields.io/badge/Ktor-2.3.6-important)

</div>

Микросервис на **Kotlin** с использованием фреймворка **Ktor**, выступающий в роли шлюза для отправки Push-уведомлений через Firebase Cloud Messaging (FCM) для Android-клиента LiveChat.

## 🚀 Назначение

Сервер предоставляет простой REST API, который Android-приложение использует для отправки запросов на рассылку push-уведомлений. Он действует как безопасный посредник между клиентом и сервисом FCM, храня критически важные учетные данные сервисного аккаунта Firebase на стороне сервера.

## 🛠️ Технологический стек

*   **Язык:** [Kotlin](https://kotlinlang.org/)
*   **Фреймворк:** [Ktor](https://ktor.io/)
*   **Админ SDK:** [Firebase Admin SDK](https://firebase.google.com/docs/admin/setup)
*   **Логирование:** [SLF4J](http://www.slf4j.org/) + [Logback](https://logback.qos.ch/)

## 📡 API Endpoints

*   `POST /send`
    *   **Назначение:** Отправка уведомления конкретному устройству по его FCM-токену.
    *   **Тело запроса (JSON):**
      ```json
      {
        "to": "fcm_token_here",
        "notification": {
          "title": "Заголовок уведомления",
          "body": "Текст уведомления"
        },
        "data": {
          "chatId": "12345",
          "anyOtherData": "value"
        }
      }
      ```

*   `POST /broadcast`
    *   **Назначение:** (Зарезервировано на будущее) Рассылка уведомлений по топику.

## 📦 Установка и запуск

### 1. Предварительные требования
*   Установите [JDK 17](https://adoptium.net/) или выше.
*   Аккаунт в [Firebase](https://console.firebase.google.com/).

### 2. Клонирование и настройка
1.  **Клонируйте репозиторий:**
    ```bash
    git clone https://github.com/OneBasten/livechat-server.git
    cd livechat-server
    ```

2.  **Получите ключ сервисного аккаунта Firebase:**
    *   В консоли Firebase откройте настройки проекта → «Учетные записи служб».
    *   Нажмите «Создать новый закрытый ключ» для сервисного аккаунта **Node.js**.
    *   Скачанный JSON-файл переименуйте в `service_account_key.json`.

3.  **Разместите ключ в проекте:**
    *   Поместите файл `service_account_key.json` в папку `resources/` вашего проекта.
    *   *Убедитесь, что этот файл добавлен в `.gitignore`!*

### 3. Запуск

**Для разработки:**
```bash
./gradlew run
