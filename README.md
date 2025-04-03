REST API для работы с пользователями 
Основная информация 

    Базовый URL : http://localhost:8080
    Порт по умолчанию : 8080
    Формат данных : JSON
    Методы аутентификации : JSON Web Token (JWT) или Basic Auth (в зависимости от реализации)
     

Методы API 
1. Создание пользователя 

Создает нового пользователя. 

    URL : /api/users
    Метод : POST
    Требуемые заголовки :
        Content-Type: application/json
         
    Тело запроса :
    json
     

 
1
2
3
4
⌄
{
    "email": "test@example.com",
    "password": "password123"
}
 
 
Пример запроса :
bash
 
 
1
2
3
curl -X POST http://localhost:8080/api/users \
-H "Content-Type: application/json" \
-d '{"email": "test@example.com", "password": "password123"}'
 
 
Ответ :
json
 

     
    1
    2
    3
    4
    5
    ⌄
    {
        "id": 1,
        "email": "test@example.com",
        "roles": ["ROLE_USER"]
    }
     
     
     

2. Обновление информации пользователя 

Обновляет данные существующего пользователя. 

    URL : /api/users/{id}
    Метод : PUT
    Требуемые заголовки :
        Content-Type: application/json
         
    Тело запроса :
    json
     

 
1
2
3
4
⌄
{
    "email": "new_email@example.com",
    "password": "new_password123"
}
 
 
Пример запроса :
bash
 
 
1
2
3
curl -X PUT http://localhost:8080/api/users/1 \
-H "Content-Type: application/json" \
-d '{"email": "new_email@example.com", "password": "new_password123"}'
 
 
Ответ :
json
 

     
    1
    2
    3
    4
    5
    ⌄
    {
        "id": 1,
        "email": "new_email@example.com",
        "roles": ["ROLE_USER"]
    }
     
     
     

3. Удаление пользователя 

Удаляет пользователя по его ID. 

    URL : /api/users/{id}
    Метод : DELETE
    Пример запроса :
    bash
     

 
1
curl -X DELETE http://localhost:8080/api/users/1
 
 
Ответ :
json
 

     
    1
    2
    3
    ⌄
    {
        "message": "User deleted"
    }
     
     
     

4. Авторизация пользователя 

Осуществляет вход пользователя в систему. 

    URL : /api/login
    Метод : POST
    Требуемые заголовки :
        Content-Type: application/json
         
    Тело запроса :
    json
     

 
1
2
3
4
⌄
{
    "email": "test@example.com",
    "password": "password123"
}
 
 
Пример запроса :
bash
 
 
1
2
3
curl -X POST http://localhost:8080/api/login \
-H "Content-Type: application/json" \
-d '{"email": "test@example.com", "password": "password123"}'
 
 
Ответ :
json
 

     
    1
    2
    3
    ⌄
    {
        "message": "Login successful"
    }
     
     
     

5. Получение информации о пользователе 

Возвращает информацию о пользователе по его ID. 

    URL : /api/users/{id}
    Метод : GET
    Пример запроса :
    bash
     

 
1
curl http://localhost:8080/api/users/1
 
 
Ответ :
json
 

     
    1
    2
    3
    4
    5
    ⌄
    {
        "id": 1,
        "email": "test@example.com",
        "roles": ["ROLE_USER"]
    }
     
     
     

Дополнительная информация 
1. Запуск сервера  

Для запуска сервера используйте команду: 
bash
 
 
1
symfony server:start --port=8080
 
 
2. Порт  

API работает на порту 8080. Если вы хотите изменить порт, укажите его явно: 
bash
 
 
1
symfony server:start --port=<НОМЕР_ПОРТА>
 
 
3. Настройка безопасности  
обрабатывается через конфигурацию в файле config/packages/security.yaml. Для использования JWT или других механизмов аутентификации потребуется дополнительная настройка. 
4. База данных  

Для хранения пользователей используется база данных. Убедитесь, что таблица user создана и содержит необходимые поля (id, email, password, roles). 
5. Ошибки  

    400 Bad Request : Некорректные данные в запросе.
    401 Unauthorized : Пользователь не авторизован.
    404 Not Found : Пользователь с указанным ID не найден.
    500 Internal Server Error : Ошибка на стороне сервера.
     
