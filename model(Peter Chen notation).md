# Модель даних нотацією Чена (ER-діаграма)

```mermaid
flowchart TD
    classDef entity fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#000
    classDef rel fill:#fff3e0,stroke:#ef6c00,stroke-width:2px,color:#000
    classDef attr fill:#f5f5f5,stroke:#616161,stroke-width:1px,color:#000

    %% Сутності
    BOOK[book]:::entity
    AUTHOR[author]:::entity
    BOOK_AUTHOR[book_author]:::entity
    COPY[copy]:::entity
    READER[reader]:::entity
    LIBRARIAN[librarian]:::entity
    BORROWING[borrowing]:::entity

    %% Зв'язки
    REL_BBA{має}:::rel
    REL_ABA{пише}:::rel
    REL_BC{має примірник}:::rel
    REL_CB{видається в}:::rel
    REL_RB{оформлює}:::rel
    REL_LB{обслуговує}:::rel

    %% Кардинальність зв'язків
    BOOK ---|1| REL_BBA
    REL_BBA ---|N| BOOK_AUTHOR

    AUTHOR ---|1| REL_ABA
    REL_ABA ---|N| BOOK_AUTHOR

    BOOK ---|1| REL_BC
    REL_BC ---|N| COPY

    COPY ---|1| REL_CB
    REL_CB ---|N| BORROWING

    READER ---|1| REL_RB
    REL_RB ---|N| BORROWING

    LIBRARIAN ---|1| REL_LB
    REL_LB ---|N| BORROWING

    %% Атрибути book_author (Пунктирне підкреслення)
    ba_bid(["<abbr title='PK'>book_id</abbr>"]):::attr --- BOOK_AUTHOR
    ba_aid(["<abbr title='PK'>author_id</abbr>"]):::attr --- BOOK_AUTHOR

    %% Атрибути book
    b_id([<u>book_id</u>]):::attr --- BOOK
    b_title([title]):::attr --- BOOK
    b_genre([genre]):::attr --- BOOK
    b_isbn([ISBN]):::attr --- BOOK
    b_year([year_of_publication]):::attr --- BOOK
    b_pages([pages_count]):::attr --- BOOK
    b_lang([language]):::attr --- BOOK

    %% Атрибути author
    a_id([<u>author_id</u>]):::attr --- AUTHOR
    a_name([author_name]):::attr --- AUTHOR
    a_country([country]):::attr --- AUTHOR

    %% Атрибути copy
    c_id([<u>copy_id</u>]):::attr --- COPY
    c_inv([inventory_number]):::attr --- COPY
    c_shelf([shelf_location]):::attr --- COPY
    c_cond([book_condition]):::attr --- COPY
    c_stat([status]):::attr --- COPY

    %% Атрибути reader
    r_id([<u>reader_id</u>]):::attr --- READER
    r_name([reader_name]):::attr --- READER
    r_phone([phone_number]):::attr --- READER
    r_email([email]):::attr --- READER
    r_reg([registration_date]):::attr --- READER
    r_stat([status]):::attr --- READER

    %% Атрибути librarian
    l_id([<u>librarian_id</u>]):::attr --- LIBRARIAN
    l_name([librarian_name]):::attr --- LIBRARIAN
    l_email([email]):::attr --- LIBRARIAN

    %% Атрибути borrowing
    br_id([<u>borrowing_id</u>]):::attr --- BORROWING
    br_bdate([borrow_date]):::attr --- BORROWING
    br_ddate([due_date]):::attr --- BORROWING
    br_rdate([return_date]):::attr --- BORROWING
    br_fstat([fine_status]):::attr --- BORROWING
    br_famt([fine_amount]):::attr --- BORROWING
    
