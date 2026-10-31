@startuml

!define Table(name,desc) entity name as "desc" << (T,#FFAAAA) >>

title Task Service

Table(Category, "Category (Категории)") {

    category_id : INT PK
    --

    name : VARCHAR(100) NOT NULL UNIQUE
}

Table(Task, "Task (Задачи)") {

    task_id : UUID PK
    --

    user_id : UUID NOT NULL <<External>>

    title : VARCHAR(200) NOT NULL

    category_id : INT FK NOT NULL

    due_at : TIMESTAMPTZ NOT NULL

    priority : ENUM(LOW, MEDIUM, HIGH)
               NOT NULL
               DEFAULT MEDIUM

    recurrence : ENUM(NEVER, DAILY, WEEKLY, MONTHLY, YEARLY)
                 NOT NULL
                 DEFAULT NEVER

    status : ENUM(NEW, DONE, CANCELLED)
             NOT NULL
             DEFAULT NEW

    created_at : TIMESTAMPTZ NOT NULL DEFAULT NOW()

    updated_at : TIMESTAMPTZ NOT NULL DEFAULT NOW()
}

Category ||--o{ Task : "1:M"


@enduml
