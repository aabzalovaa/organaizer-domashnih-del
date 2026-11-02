@startuml

actor User

participant "Marketplace Frontend" as Frontend

participant "API Gateway" as Gateway

participant "Organizer Task Service" as TaskService

database "Organizer DB" as Database

User -> Frontend: Изменить статус задачи

activate Frontend

Frontend -> Gateway: PATCH /tasks/{taskId}/status

activate Gateway

Gateway -> Gateway: Проверить JWT-токен

activate Gateway

Gateway --> Gateway: Токен валиден

deactivate Gateway

Gateway -> TaskService: PATCH /tasks/{taskId}/status + userId

activate TaskService

TaskService -> Database: Обновить статус задачи

activate Database

Database --> TaskService: Обновленная задача / задача не найдена

deactivate Database

alt Задача найдена

TaskService --> Gateway: Обновленная задача

deactivate TaskService

Gateway --> Frontend: Обновленная задача

deactivate Gateway

Frontend --> User: Отобразить обновленный статус

deactivate Frontend

else Задача не найдена

TaskService --> Gateway: Задача не найдена

deactivate TaskService

Gateway --> Frontend: Ошибка изменения статуса

deactivate Gateway

Frontend --> User: Сообщение об ошибке

deactivate Frontend

end

@enduml
