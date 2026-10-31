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

    priority : task_priority_enum NOT NULL DEFAULT 'MEDIUM'

    recurrence : recurrence_enum NOT NULL DEFAULT 'NEVER'

    status : task_status_enum NOT NULL DEFAULT 'NEW'

    created_at : TIMESTAMPTZ NOT NULL DEFAULT NOW()

    updated_at : TIMESTAMPTZ NOT NULL DEFAULT NOW()
}

Category ||--o{ Task : "1:M"

@enduml
