This is a fully documented MS Access project for a hotel) being a part of the University of Lodz DBs course

## DATABASE – HOTEL

**Authors:** Paweł Żurawski, Patryk Mielke

### Summary
The database contains information about rooms, bookings, payments and their methods, as well as clients, invoices, employees, and their positions, including related forms and reports.

---

### Table of Contents

1. **User Guide** — 5
2. **Project Background Description** — 5
3. **Project Description** — 5
4. **Normalization/Denormalization** — 5
5. **Database Model** — 6
   - Entities — 6
   - Attributes — 6
   - Relationships — 10
6. **Table Listing** — 11
7. **Business Rules** — 12
8. **Conceptual Model** — 13
9. **Logical Model** — 14
10. **Physical Model** — 15
11. **Table Index Listing** — 16
12. **Queries** — 17
    - KwDaneDoFakturaPozycje — 17
    - KwDaneKlienta — 17
    - KwDostepnePokojeWTerminie — 18
    - KwFaktura — 21
    - KwFakturaPozycje — 22
    - KwPokojePosegregowane — 23
    - KwRezerwacjaWyborPokoju — 24
    - KwWolnePokoje — 26
    - KwZajetePokoje — 26
    - oblozenie_pokoi_w_danym_okresie — 27
    - oblozenie_w_danym_okresie — 28
    - oblozenie_w_danym_roku — 29
    - oblozenie_w_danym_roku_miesieczne — 29
    - rezerwacjeNadchodzące — 31
    - rezerwacjeTrwające — 31
    - suma_przychodow_w_danym_okresie — 32
    - suma_przychodow_w_danym_roku — 33
    - suma_przychodow_w_danym_roku_kwartalnie — 33
    - suma_przychodow_w_danym_roku_miesiecznie — 35
13. **Reports** — 37
    - oblozenie_pokoi_w_danym_okresie — 37
    - oblozenie_w_danym_okresie — 38
    - oblozenie_w_danym_roku — 39
    - oblozenie_w_danym_roku_miesieczne — 39
    - RaWolnePokoje — 41
    - RaZajetePokoje — 42
    - rezerwacjeNadchodzące — 42
    - rezerwacjeTrwające — 43
    - suma_przychodow_w_danym_okresie — 43
    - suma_przychodow_w_danym_roku — 44
    - suma_przychodow_w_danym_roku_kwartalnie — 45
    - suma_przychodow_w_danym_roku_miesiecznie — 46
14. **Templates** — 47
    - WzórFaktury — 47
15. **Forms** — 48
    - AplikacjaHotel — 48
    - FoFaktura — 61
    - FoFakturaPozycje — 61
    - FoHotel — 62
    - FoInneFormularze — 62
    - FoKlient — 65
    - FoMetodaPłatności — 65
    - FoPokoje — 66
    - FoPracownik — 67
    - FoRaporty — 68
    - FoRezerwacja — 68
    - FoRezerwacjeNadchodzące — 69
    - FoRezerwacjeTrwające — 69
    - FoSkracanie — 70
    - FoStanowisko — 70
    - FoTypPokoju — 71
    - ListaPokoiDoPrzedluzenia — 72
    - oblozenie_pokoi_w_danym_okresie — 74
    - oblozenie_w_danym_okresie — 75
    - oblozenie_w_danym_roku — 76
    - oblozenie_w_danym_roku_miesiecznie — 76
    - suma_przychodow_w_danym_okresie — 77
    - suma_przychodow_w_danym_roku — 78
    - suma_przychodow_w_danym_roku_kwartalnie — 79
    - suma_przychodow_w_danym_roku_miesiecznie — 79
    - wolne_pokoje_w_danym_terminie — 81

---

### User Guide

#### Project Background Description
The hotel rents rooms to clients for leisure purposes. The documented database includes information about rooms, bookings, payments and their methods, clients, invoices, employees, and their positions, along with details related to the above. The database supports booking and canceling stays, checking in and out clients, as well as generating invoices and reports on room occupancy and revenue.

#### Project Description
The database contains information about hotel rooms, bookings, payments, clients, and employees with their positions. It also includes queries to check room occupancy for a user-specified period, overall occupancy for a user-specified period, yearly and monthly occupancy, and hotel revenue for a period or year (broken down by months/quarters), as well as ongoing and upcoming bookings. The aforementioned queries have been used to create forms and reports that are also included in the database. The database is equipped with a set of forms designed to manage table contents while validating the accuracy of input data. The most important of these is the Hotel Application, which allows for making reservations, checking in and out, generating reports, and managing tables. The reports concern overall hotel occupancy for a user-specified period, individual room occupancy, monthly occupancy throughout the year, or hotel revenue for a user-specified period or year (broken down by months/quarters), as well as ongoing and upcoming bookings.

#### Normalization/Denormalization
All attributes are atomic, thus the database adheres to the first normal form. Each attribute depends only on the primary key and not on other attribute values, meeting the second normal form requirements. Additionally, there are no transitive dependencies, thus the database meets the third normal form requirements. Denormalization has not been applied as the intended users of this database are assumed to have limited database knowledge, and denormalization would reduce the clarity of the database.

## Database Model

### Entities

**Table 1: Entity Overview**

| Name                 | Description                                |
|----------------------|--------------------------------------------|
| Faktura              | Stores invoice data.                      |
| Hotel                | Stores hotel information.                 |
| Klient               | Stores client information.                |
| Metoda Płatności     | Stores supported payment methods.         |
| Płeć                 | Stores a list of genders.                 |
| Pokój                | Stores information about rooms in the hotel. |
| Pracownik            | Stores employee information.              |
| Rezerwacja           | Stores reservation details.               |
| Stanowisko           | Stores a list of job positions in the hotel. |
| Status Rezerwacji    | Stores reservation status.                |
| Typ Pokoju           | Stores information about room types.      |
| Województwo          | Stores a list of provinces.               |

### Attributes

**Table 2: Faktura Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Numer Faktury        | Number     | Required    | Primary key                    |
| Klient               | Number     | Required    | Foreign key                    |
| Firma                | Text(50)   | Optional    | Foreign key                    |
| Nip                  | Text(10)   | Optional    |                                |
| Rezerwacja           | Number     | Required    | Foreign key                    |
| Kwota                | Currency   | Required    |                                |
| Data wystawienia     | Date       | Required    | Today                          |
| Opłacone             | Yes/No     | Required    |                                |
| Metoda płatności     | Number     | Required    | Foreign key                    |

**Table 3: Hotel Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Kod Hotelu           | Text(6)    | Required    | Primary key                    |
| Nazwa                | Text(50)   | Required    |                                |
| Ulica                | Text(50)   | Required    |                                |
| Numer budynku        | Text(10)   | Required    |                                |
| Kod pocztowy         | Text(6)    | Required    |                                |
| Miasto               | Text(50)   | Required    |                                |
| Województwo          | Number     | Required    | Foreign key                    |
| Telefon              | Text(9)    | Required    |                                |
| Adres E-mail         | Text(80)   | Required    |                                |
| NIP                  | Text(10)   | Required    |                                |
| Numer Rachunku       | Text(26)   | Required    |                                |

**Table 4: Klient Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Klienta           | Number     | Required    | Primary key                    |
| Imię                 | Text(20)   | Required    |                                |
| Nazwisko             | Text(30)   | Required    |                                |
| Płeć                 | Number     | Required    | Foreign key                    |
| Numer dowodu         | Text(9)    | Required    |                                |
| Telefon              | Text(9)    | Required    |                                |
| Adres E-mail         | Text(80)   | Required    |                                |
| Ulica                | Text(80)   | Required    |                                |
| Numer Budynku        | Text(10)   | Required    |                                |
| Kod Pocztowy         | Text(6)    | Required    |                                |
| Miasto               | Text(50)   | Required    |                                |
| Województwo          | Number     | Required    | Foreign key                    |

**Table 5: Metoda Płatności Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Metody            | Number     | Required    | Primary key                    |
| Metoda Płatności     | Text(20)   | Required    |                                |

**Table 6: Płeć Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Płci              | Number     | Required    | Primary key                    |
| Nazwa                | Text(9)    | Required    |                                |

**Table 7: Pokój Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Pokoju            | Number     | Required    | Primary key                    |
| Numer Pokoju         | Number     | Required    |                                |
| Kod Hotelu           | Text(6)    | Required    |                                |
| Typ Pokoju           | Number     | Required    | Foreign key                    |
| Czy Dostępny         | Yes/No     | Required    |                                |

**Table 8: Pracownik Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Pracownika        | Number     | Required    | Primary key                    |
| Imię                 | Text(20)   | Required    |                                |
| Nazwisko             | Text(30)   | Required    |                                |
| Stanowisko           | Number     | Required    | Foreign key                    |
| Wynagrodzenie        | Currency   | Required    |                                |
| Kod Hotelu           | Text(6)    | Required    |                                |
| Płeć                 | Number     | Required    | Foreign key                    |
| Numer dowodu         | Text(9)    | Required    |                                |
| Telefon              | Text(9)    | Required    |                                |
| Adres E-mail         | Text(80)   | Required    |                                |
| Ulica                | Text(80)   | Required    |                                |
| Numer Budynku        | Text(10)   | Required    |                                |
| Kod Pocztowy         | Text(6)    | Required    |                                |
| Miasto               | Text(50)   | Required    |                                |
| Województwo          | Number     | Required    | Foreign key                    |

**Table 9: Rezerwacja Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Rezerwacji        | Number     | Required    | Primary key                    |
| Klient               | Number     | Required    | Foreign key                    |
| Pokój                | Number     | Required    | Foreign key                    |
| Data Przybycia       | Date       | Required    |                                |
| Data Odjazdu         | Date       | Required    |                                |
| Status Rezerwacji    | Number     | Required    | Foreign key                    |

**Table 10: Stanowisko Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Stanowiska        | Number     | Required    | Primary key                    |
| Stanowisko           | Text(40)   | Required    |                                |

**Table 11: Status Rezerwacji Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Status            | Number     | Required    | Primary key                    |
| Status Rezerwacji    | Text(20)   | Required    |                                |

**Table 12: Typ Pokoju Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Typu              | Number     | Required    | Primary key                    |
| Nazwa                | Text(30)   | Required    |                                |
| Liczba osób          | Number     | Required    |                                |
| Ilość łóżek          | Number     | Required    |                                |
| Cena                 | Currency   | Required    |                                |

**Table 13: Województwo Attributes**

| Attribute            | Data Type  | Required    | Description                     |
|----------------------|------------|-------------|---------------------------------|
| Id Województwa       | Number     | Required    | Primary key                    |
| Województwo          | Text(19)   | Required    |                                |

### Relationships

**Table 14: Entity Relationships**

| Parent Entity        | Child Entity           | Cardinality | Type            | Existence |
|----------------------|-------------------------|-------------|-----------------|-----------|
| Hotel                | Pokój                   | 1:N         | Identifying     | Required  |
| Hotel                | Pracownik               | 1:N         | Identifying     | Required  |
| Województwo          | Hotel                   | 1:N         | Non-identifying | Required  |
| Województwo          | Klient                  | 1:N         | Non-identifying | Required  |
| Województwo          | Pracownik               | 1:N         | Non-identifying | Required  |
| Płeć                 | Klient                  | 1:N         | Non-identifying | Required  |
| Płeć                 | Pracownik               | 1:N         | Non-identifying | Required  |
| Stanowisko           | Pracownik               | 1:N         | Identifying     | Required  |
| Typ Pokoju           | Pokój                   | 1:N         | Non-identifying | Required  |
| Pokój                | Rezerwacja              | 1:N         | Identifying     | Required  |
| Klient               | Rezerwacja              | 1:N         | Identifying     | Required  |
| Status Rezerwacji    | Rezerwacja              | 1:N         | Non-identifying | Required  |
| Rezerwacja           | Faktura                 | 1:1         | Identifying     | Required  |
| Metoda Płatności     | Faktura                 | 1:N         | Non-identifying | Required  |

### Business Rules

| Use Case                        | Implementation Description                       | Example Action                       | Implementation Location |
|---------------------------------|--------------------------------------------------|-------------------------------------|-------------------------|
| Enforce correct date format      | Data Odjazdu > Data Przybycia                    | Appropriate error message            | Database                |
| Enforce correct NIP format       | 0000000000                                       | 1234567890                          | Database                |
| Enforce correct hotel code format | !LL0000                                          | LO0001                              | Database                |
| Enforce correct postal code format| 00\-000                                          | 12-345                              | Database                |
| Enforce correct phone number format | 900\-000\-000                                  | 123-456-789                         | Database                |
| Enforce correct email format     | ((Like "*?@?*.?*") And (Not Like "*[ ,;]*"))     | test@test.pl                         | Database                |
| Enforce correct first name format | >L<LL?????????????                              | Jan                                 | Database                |
| Enforce correct last name format | >L<LL?????????????                              | Kowalski                            | Database                |
| Enforce correct ID number format  | LLL\-000000                                     | Abc-123456                          | Database                |
| Enforce correct bank account format | 00\ 0000\ 0000\ 0000\ 0000\ 0000\ 0000      | 82 1020 5226 0000 6102 0417 7895   | Database                |

### Conceptual model

![Conceptual Model](images/1.png)

### Logical model

![Logical Model](images/2.png)

### Physical model

![Physical Model](images/3.png)

### Tables

- Faktura
- FakturaPozycje
- Hotel
- Klient
- MetodaPłatności
- Płeć
- Pokój
- Pracownik
- Rezerwacja
- Stanowisko
- StatusRezerwacji
- TypPokoju
- Województwo

### Indexes

- NumerFaktury
- KodHotelu
- IdKlienta
- IdMetodaPłatności
- IdPłci
- IdPokoju
- IdPracownika
- IdRezerwacji
- IdStanowiska
- IdStatus
- IdTypu
- Idwojewodztwa


