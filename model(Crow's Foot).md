# Модель даних в нотації Crow's Foot (ER-діаграма)

```mermaid
erDiagram
    book ||--|{ book_author : "має"
    author ||--o{ book_author : "пише"
    book ||--o{ copy : "має"
    copy ||--o{ borrowing : "видається в"
    reader ||--o{ borrowing : "оформлює"
    librarian ||--o{ borrowing : "обслуговує"

    book {
        SERIAL book_id PK
        TEXT title
        TEXT genre
        TEXT ISBN UK
        INT year_of_publication
        INT pages_count
        TEXT language
    }

    author {
        SERIAL author_id PK
        TEXT author_name
        TEXT country
    }

    book_author {
        INT book_id PK, FK
        INT author_id PK, FK
    }

    copy {
        SERIAL copy_id PK
        INT book_id FK
        TEXT inventory_number UK
        TEXT shelf_location
        TEXT book_condition
        copy_status status
    }

    reader {
        SERIAL reader_id PK
        TEXT reader_name
        TEXT phone_number
        TEXT email UK
        DATE registration_date
        reader_status status
    }

    librarian {
        SERIAL librarian_id PK
        TEXT librarian_name
        TEXT email UK
    }

    borrowing {
        SERIAL borrowing_id PK
        INT copy_id FK
        INT reader_id FK
        INT librarian_id FK
        DATE borrow_date
        DATE due_date
        DATE return_date
        fine_status fine_status
        NUMERIC fine_amount
    }
