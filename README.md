An MS Access project of a Hotel being a part of the University of Lodz "Databases" course.

# HOTEL - management system

**Authors:** Paweł Żurawski, Patryk Mielke

### Summary
The database contains information about rooms, bookings, payments and their methods, as well as clients, invoices, employees, and their positions, including related forms and reports.

---

### Table of Contents

1. **User Guide**
2. **Project Background Description**
3. **Project Description**
4. **Normalization/Denormalization**
5. **Database Model**
   - Entities
   - Attributes
   - Relationships
6. **Table Listing**
7. **Business Rules**
8. **Conceptual Model**
9. **Logical Model**
10. **Physical Model**
11. **Table Index Listing**
12. **Queries**
    - KwDaneDoFakturaPozycje
    - KwDaneKlienta
    - KwDostepnePokojeWTerminie
    - KwFaktura
    - KwFakturaPozycje
    - KwPokojePosegregowane
    - KwRezerwacjaWyborPokoju
    - KwWolnePokoje
    - KwZajetePokoje
    - oblozenie_pokoi_w_danym_okresie
    - oblozenie_w_danym_okresie
    - oblozenie_w_danym_roku
    - oblozenie_w_danym_roku_miesieczne
    - rezerwacjeNadchodzące
    - rezerwacjeTrwające
    - suma_przychodow_w_danym_okresie
    - suma_przychodow_w_danym_roku
    - suma_przychodow_w_danym_roku_kwartalnie
    - suma_przychodow_w_danym_roku_miesiecznie
13. **Reports**
    - oblozenie_pokoi_w_danym_okresie
    - oblozenie_w_danym_okresie
    - oblozenie_w_danym_roku
    - oblozenie_w_danym_roku_miesieczne
    - RaWolnePokoje
    - RaZajetePokoje
    - rezerwacjeNadchodzące
    - rezerwacjeTrwające
    - suma_przychodow_w_danym_okresie
    - suma_przychodow_w_danym_roku
    - suma_przychodow_w_danym_roku_kwartalnie
    - suma_przychodow_w_danym_roku_miesiecznie
14. **Templates**
    - WzórFaktury
15. **Forms**
    - AplikacjaHotel
    - FoFaktura
    - FoFakturaPozycje
    - FoHotel
    - FoInneFormularze
    - FoKlient
    - FoMetodaPłatności
    - FoPokoje
    - FoPracownik
    - FoRaporty
    - FoRezerwacja
    - FoRezerwacjeNadchodzące
    - FoRezerwacjeTrwające
    - FoSkracanie
    - FoStanowisko
    - FoTypPokoju
    - ListaPokoiDoPrzedluzenia
    - oblozenie_pokoi_w_danym_okresie
    - oblozenie_w_danym_okresie
    - oblozenie_w_danym_roku
    - oblozenie_w_danym_roku_miesiecznie
    - suma_przychodow_w_danym_okresie
    - suma_przychodow_w_danym_roku
    - suma_przychodow_w_danym_roku_kwartalnie
    - suma_przychodow_w_danym_roku_miesiecznie
    - wolne_pokoje_w_danym_terminie

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



## Queries

### KwDaneDoFakturaPozycje

**SQL:**

```sql
SELECT Rezerwacja.IdRezerwacji, TypPokoju.Cena AS CenaBrutto, 1+[DataOdjazdu]-[DataPrzybycia] AS Ilosc
FROM TypPokoju 
INNER JOIN (Pokój 
INNER JOIN (Klient 
INNER JOIN Rezerwacja ON Klient.[IdKlienta] = Rezerwacja.Klient) 
ON Pokój.[IdPokoju] = Rezerwacja.Pokoj) 
ON TypPokoju.[IdTypu] = Pokój.[Typpokoju];
```

Description:
Returns results containing three columns: IdRezerwacji, CenaBrutto, and Ilosc, where Ilosc is the result of calculations performed on the DataOdjazdu and DataPrzybycia columns from the Rezerwacja table, with an additional value of 1. CenaBrutto represents the room price from the TypPokoju table. The result includes data from the joined tables: Klient, Pokój, Rezerwacja, and TypPokoju.

### KwDaneKlienta

**SQL:**

```sql
SQL: SELECT Klient.IdKlienta, [Imię] & " " & [Nazwisko] AS [Imię i nazwisko], Klient.Telefon AS Telefon
FROM Klient;
```

Description: Returns results that include three columns: "IdKlienta" - customer identifier, "[Imię i nazwisko]" - concatenated string of the customer's first and last name separated by a space, "Telefon" - customer's phone number. The result includes data from the "Klient" table, where each tuple will contain information about the customer's identifier, their first and last name, and their phone number.


### KwDostepnePokojeWTerminie

**SQL:**

```sql
PARAMETERS [Forms]![FoRezerwacja]![DataPrzybycia] DateTime, [Forms]![FoRezerwacja]![DataOdjazdu] DateTime;
SELECT DISTINCT P.[NumerPokoju] AS Pokój, P.Typpokoju AS Typ, P.IdPokoju
FROM Pokój AS P LEFT JOIN Rezerwacja AS R ON P.[IdPokoju] = R.Pokoj
WHERE (
    ((R.DataPrzybycia IS NULL AND [Forms]![FoRezerwacja]![DataPrzybycia] < [Forms]![FoRezerwacja]![DataOdjazdu])
    OR ([Forms]![FoRezerwacja]![DataPrzybycia] < [Forms]![FoRezerwacja]![DataOdjazdu] AND R.DataOdjazdu IS NULL)
    OR (R.DataPrzybycia IS NOT NULL AND R.DataOdjazdu IS NOT NULL AND ([Forms]![FoRezerwacja]![DataPrzybycia] >= R.DataOdjazdu OR [Forms]![FoRezerwacja]![DataOdjazdu] <= R.DataPrzybycia)))
    OR ((R.StatusRezerwacji IN (3, 4) AND (SELECT COUNT(*) FROM Rezerwacja AS R2 WHERE R2.Pokoj = P.[IdPokoju] AND R2.IdRezerwacji <> R.IdRezerwacji AND ([Forms]![FoRezerwacja]![DataPrzybycia] >= R2.DataPrzybycia AND [Forms]![FoRezerwacja]![DataPrzybycia] < R2.DataOdjazdu) OR ([Forms]![FoReRezerwacja]![DataOdjazdu] > R2.DataPrzybycia AND [Forms]![FoRezerwacja]![DataOdjazdu] <= R2.DataOdjazdu))) = 0)
    OR ((R.StatusRezerwacji IN (1, 2) AND (SELECT COUNT(*) FROM Rezerwacja AS R2 WHERE R2.Pokoj = P.[IdPokoju] AND R2.IdRezerwacji <> R.IdRezerwacji AND ([Forms]![FoRezerwacja]![DataPrzybycia] >= R2.DataPrzybycia AND [Forms]![FoRezerwacja]![DataPrzybycia] < R2.DataOdjazdu) OR ([Forms]![FoRezerwacja]![DataOdjazdu] > R2.DataPrzybycia AND [Forms]![FoRezerwacja]![DataOdjazdu] <= R2.DataOdjazdu)) AND R2.StatusRezerwacji IN (1, 2)) > 0))
    AND (((SELECT COUNT(*) FROM Rezerwacja AS R3 WHERE R3.Pokoj = P.[IdPokoju] AND R3.DataPrzybycia = [Forms]![FoRezerwacja]![DataPrzybycia] AND R3.DataOdjazdu = [Forms]![FoRezerwacja]![DataOdjazdu] AND R3.StatusRezerwacji IN (3, 4)) > 0)
    OR ((SELECT COUNT(*) FROM Rezerwacja AS R4 WHERE R4.Pokoj = P.[IdPokoju] AND R4.DataPrzybycia = [Forms]![FoRezerwacja]![DataPrzybycia] AND R4.DataOdjazdu = [Forms]![FoRezerwacja]![DataOdjazdu] AND R4.StatusRezerwacji IN (1, 2)) > 0)
    OR ((SELECT COUNT(*) FROM Rezerwacja AS R5 WHERE R5.Pokoj = P.[IdPokoju] AND R5.DataPrzybycia = [Forms]![FoRezerwacja]![DataPrzybycia] AND R5.DataOdjazdu = [Forms]![FoRezerwacja]![DataOdjazdu]) = 0));
```

Description: Returns available hotel rooms based on the selected check-in and check-out dates from the form. It considers different booking scenarios and room availability, taking into account booking statuses and dates.


### KwFaktura

**SQL:**

```sql
SELECT Faktura.[NumerFaktury], Faktura.Firma AS FirmaKlienta, Faktura.NIP AS NIPKlienta, [Klient_1].[Imię] & " " & [Klient_1].[Nazwisko] AS Klient, Faktura.[DataWystawienia], Faktura.Opłacone, Faktura.[MetodaPłatności], "Pokój '" & [Typpokoju].Nazwa & "'" AS Pokój, FakturaPozycje.Ilość, FakturaPozycje.[Cenanetto], FakturaPozycje.[PodatekVAT], FakturaPozycje.CenaBrutto, Hotel.Nazwa AS Hotel, [Hotel].[Ulica] & " " & [Hotel].[NumerBudynku] AS Adres1, [Hotel].[Miasto] & " " & [Hotel].[KodPocztowy] AS Adres2, Hotel.Telefon, Hotel.NIP AS NIPHotelu, Hotel.[NumerRachunku]
FROM Klient AS Klient_1 INNER JOIN (Klient INNER JOIN (Hotel INNER JOIN (TypPokoju INNER JOIN ((Pokój INNER JOIN Rezerwacja ON Pokój.[IdPokoju] = Rezerwacja.Pokoj) INNER JOIN (Faktura INNER JOIN FakturaPozycje ON Faktura.[NumerFaktury]=FakturaPozycje.[NumerFaktury]) ON Rezerwacja.IdRezerwacji=FakturaPozycje.[IdRezerwacji]) ON [Typpokoju].[IdTypu]=Pokój.[Typpokoju]) ON Hotel.[KodHotelu] = Pokój.[KodHotelu]) ON Klient.[IdKlienta] = Rezerwacja.Klient) ON Klient_1.[IdKlienta]=Faktura.[IdKlient]
WHERE (((Faktura.NumerFaktury)=Forms![AplikacjaHotel]!PodformularzNawigacji.Form![NumerFaktury]));
```

Description: Contains detailed information related to the invoice, such as invoice number, client details, hotel details, room details, quantity, net prices, VAT, gross price, and others. The result pertains to an invoice with a specific invoice number provided from the hotel application form.


### KwFakturaPozycje

**SQL:**

```sql
SELECT Rezerwacja.Klient, Rezerwacja.[StatusRezerwacji]
FROM StatusRezerwacji INNER JOIN (TypPokoju INNER JOIN (Pokój INNER JOIN Rezerwacja ON Pokój.[IdPokoju]=Rezerwacja.Pokoj) ON [Typpokoju].[Id Typu]=Pokój.[Typpokoju]) ON [StatusRezerwacji].[Id Status]=Rezerwacja.[StatusRezerwacji]
WHERE (((Rezerwacja.[StatusRezerwacji])=2 Or (Rezerwacja.[StatusRezerwacji])=3));
```

Description: Returns information about clients and booking status for reservations with statuses 2 or 3. The result comes from the joined tables: StatusRezerwacji, TypPokoju, Pokój, and Rezerwacja.


### KwPokojePosegregowane

**SQL:**

```sql
SELECT Pokój.NumerPokoju, Pokój.Typpokoju
FROM Pokój
ORDER BY Pokój.NumerPokoju;
```

Description: Contains information about room numbers and types, sorted by room number in ascending order. The result comes from the "Pokój" table.


### KwRezerwacjaWyborPokoju

**SQL:**

```sql
SELECT Pokój.[Numer Pokoju] AS Pokój, [Typpokoju].[Liczba Osób] AS Osoby, [Typpokoju].Name, [Typpokoju].[Ilość łóżek] AS Łóżka
FROM TypPokoju INNER JOIN Pokój ON [Typpokoju].[Id Typu]=Pokój.[Typ pokoju];
```

Description: Contains information regarding room numbers, number of people, room type names, and number of beds. The result comes from the "TypPokoju" and "Pokój" tables, with data joined based on room type and category identifiers.


### KwWolnePokoje

**SQL:**

```sql
SELECT Pokój.[Id Pokoju], Pokój.[Numer Pokoju] AS Pokój, [Typpokoju].Nazwa, [Typpokoju].[Liczba Osób]
FROM TypPokoju INNER JOIN Pokój ON [Typpokoju].[Id Typu]=Pokój.[Typ pokoju]
WHERE (((Pokój.[Czy dostępny])=Yes));
```

Description: Contains information about available rooms, including room ID, room number, room type name, and number of people. It returns only rooms that are available.


### KwZajetePokoje

**SQL:**

```sql
SELECT Pokój.[NumerPokoju], Pokój.[Typpokoju], [Typpokoju].[Liczba Osób]
FROM TypPokoju INNER JOIN Pokój ON [Typpokoju].[Id Typu]=Pokój.[Typpokoju]
WHERE (((Pokój.[Czydostępny])=No));
```

Description: Contains information about rooms marked as unavailable, including room number, room type, and number of people. The result comes from the "Pokój" table.


### oblozenie_pokoi_w_danym_okresie

**SQL:**

```sql
SELECT r.Pokoj, Count(r.Pokoj) AS oblozenie, r.DataPrzybycia AS Od, r.DataOdjazdu AS Do
FROM Rezerwacja AS r
WHERE (((r.DataPrzybycia) Between Forms!oblozenie_pokoi_w_danym_okresie!DataPrzyjazdu And Forms!oblozenie_pokoi_w_danym_okresie!DataOdjazdu) And ((r.DataOdjazdu) Between Forms!oblozenie_pokoi_w_danym_okresie!DataPrzyjazdu And Forms!oblozenie_pokoi_w_danym_okresie!DataOdjazdu))
GROUP BY r.Pokoj, r.DataPrzybycia, r.DataOdjazdu
ORDER BY r.Pokoj DESC;
```

Description: Contains information about room occupancy in a specified period. Results are grouped by room number, arrival date, and departure date, allowing for the analysis of occupancy over time.


### oblozenie_w_danym_okresie

**SQL:**

```sql
SELECT Count(r.Pokoj) AS oblozenie, Format(Forms!oblozenie_w_danym_okresie!DataPrzyjazdu,"dd/mm/yyyy") AS Od, Format(Forms!oblozenie_w_danym_okresie!DataOdjazdu,"dd/mm/yyyy") AS Do
FROM Rezerwacja AS r
WHERE (((r.DataPrzybycia) Between Forms!oblozenie_w_danym_okresie!DataPrzyjazdu And Forms!oblozenie_w_danym_okresie!DataOdjazdu)  AND ((r.DataOdjazdu) Between Forms!oblozenie_w_danym_okresie!DataPrzyjazdu And Forms!oblozenie_w_danym_okresie!DataOdjazdu));
```

Description: Contains overall occupancy for all rooms in a specified period. Occupancy is counted as the number of reservations within the given period. The "From" and "To" dates are formatted based on the form.


### oblozenie_w_danym_roku

**SQL:**

```sql
SELECT Count(r.Pokoj) AS oblozenie, Forms!oblozenie_w_danym_roku!RokRaport AS rok
FROM Rezerwacja AS r
WHERE YEAR(r.DataPrzybycia) = Forms!oblozenie_w_danym_roku!RokRaport AND YEAR(r.DataOdjazdu) = Forms!oblozenie_w_danym_roku!RokRaport;
```

Description: Contains monthly room occupancy for a given year based on reservations. Occupancy is calculated for each month of the year, with missing data in a given month showing a value of 0.

### oblozenie_w_danym_roku_miesieczne

**SQL:**

```sql
SELECT IIf(IsNull(r.oblozenie),0,r.oblozenie) AS oblozenie, m.rok, m.miesiac
FROM (SELECT DISTINCT Year(DataPrzybycia) AS rok, 1 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 2 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 3 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 4 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 5 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 6 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 7 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 8 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 9 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 10 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 11 AS miesiac FROM Rezerwacja     UNION ALL SELECT DISTINCT Year(DataPrzybycia) AS rok, 12 AS miesiac FROM Rezerwacja )  AS m LEFT JOIN (SELECT Count(IdRezerwacji) AS oblozenie, Year(DataPrzybycia) AS rok, Month(DataPrzybycia) AS miesiac FROM Rezerwacja WHERE Year(DataPrzybycia) = Forms!oblozenie_w_danym_roku_miesiecznie!RokRaport     AND Year(DataOdjazdu) = Forms!oblozenie_w_danym_roku_miesiecznie!RokRaport GROUP BY Year(DataPrzybycia), Month(DataPrzybycia))  AS r ON (m.miesiac = r.miesiac) AND (m.rok = r.rok)
WHERE m.rok = Forms!oblozenie_w_danym_roku_miesiecznie!RokRaport
ORDER BY m.rok, m.miesiac;
```

Description: Contains monthly room occupancy for a given year based on reservations. Occupancy is calculated for each month of the year, with missing data in a given month showing a value of 0.


### rezerwacjeNadchodzące

**SQL:**

```sql
SELECT R.IdRezerwacji, P.NumerPokoju, R.DataPrzybycia
FROM Pokój AS P INNER JOIN Rezerwacja AS R ON P.IdPokoju = R.Pokoj
WHERE (((R.DataPrzybycia) Between Date() And Date()+7) AND ((R.StatusRezerwacji)=1));
```

Description: Contains information about upcoming reservations (within the next week from today) and reservation status (status 1). The result includes reservation ID, room number, and arrival date.


### rezerwacjeTrwające

**SQL:**

```sql
SELECT R.IdRezerwacji, P.NumerPokoju, R.DataOdjazdu
FROM Pokój AS P INNER JOIN Rezerwacja AS R ON P.IdPokoju = R.Pokoj
WHERE (((R.StatusRezerwacji)=2));
```

Description: Contains information about currently ongoing reservations (status 2). The result includes reservation ID, room number, and departure date.


### suma_przychodow_w_danym_okresie

**SQL:**

```sql
SELECT Sum(fp.CenaBrutto) AS przychody, Format(Forms!suma_przychodow_w_danym_okresie!DataPrzyjazdu,"dd/mm/yyyy") AS Od, Format(Forms!suma_przychodow_w_danym_okresie!DataOdjazdu,"dd/mm/yyyy") AS Do
FROM FakturaPozycje AS fp, Faktura AS f
WHERE (((f.DataWystawienia) Between Forms!suma_przychodow_w_danym_okresie!DataPrzyjazdu And Forms!suma_przychodow_w_danym_okresie!DataOdjazdu) And ((fp.NumerFaktury)=f.NumerFaktury));
```

Description: Contains total revenue for a specified period. Revenue is calculated based on invoices and their items issued during that period. The "From" and "To" dates are formatted according to the form.

### suma_przychodow_w_danym_roku

**SQL:**

```sql
SELECT SUM(fp.CenaBrutto) AS przychody, Forms!suma_przychodow_w_danym_roku!RokRaport AS rok
FROM FakturaPozycje AS fp, Faktura AS f
WHERE (YEAR(f.DataWystawienia) = Forms!suma_przychodow_w_danym_roku!RokRaport) AND ((fp.NumerFaktury)=f.NumerFaktury);
```

Description: Contains total revenue for a specified year. Revenue is calculated based on invoices and their items for that year.


### suma_przychodow_w_danym_roku_kwartalnie

**SQL:**

```sql
SELECT IIf(IsNull(fp.przychody),0,fp.przychody) AS przychody, m.rok, m.kwartal
FROM (SELECT DISTINCT Year(DataWystawienia) AS rok, 1 AS kwartal FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 2 AS kwartal FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 3 AS kwartal FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 4 AS kwartal FROM Faktura )  AS m LEFT JOIN (SELECT Year(DataWystawienia) AS rok, IIf(Month(DataWystawienia) In (1,2,3),1,IIf(Month(DataWystawienia) In (4,5,6),2,IIf(Month(DataWystawienia) In (7,8,9),3,4))) AS kwartal, Sum(CenaBrutto) AS przychody FROM FakturaPozycje INNER JOIN Faktura ON FakturaPozycje.NumerFaktury = Faktura.NumerFaktury GROUP BY Year(DataWystawienia), IIf(Month(DataWystawienia) In (1,2,3),1,IIf(Month(DataWystawienia) In (4,5,6),2,IIf(Month(DataWystawienia) In (7,8,9),3,4))))  AS fp ON (m.kwartal = fp.kwartal) AND (m.rok = fp.rok)
WHERE m.rok = Forms!suma_przychodow_w_danym_roku_kwartalnie!RokRaport
ORDER BY m.rok, m.kwartal;
```

Description: Contains quarterly revenue for a specified year. It calculates the sum of revenue for each quarter of the year based on invoices and their items.

### suma_przychodow_w_danym_roku_miesiecznie

**SQL:**

```sql
SELECT NZ(Sum(fp.CenaBrutto),0) AS przychody, m.rok, m.miesiac
FROM (SELECT DISTINCT Year(DataWystawienia) AS rok, 1 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 2 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 3 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 4 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 5 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 6 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 7 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 8 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 9 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 10 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 11 AS miesiac FROM Faktura     UNION ALL SELECT DISTINCT Year(DataWystawienia) AS rok, 12 AS miesiac FROM Faktura )  AS m LEFT JOIN (SELECT Year(DataWystawienia) AS rok, Month(DataWystawienia) AS miesiac, CenaBrutto FROM FakturaPozycje INNER JOIN Faktura ON FakturaPozycje.NumerFaktury = Faktura.NumerFaktury)  AS fp ON (m.miesiac = fp.miesiac) AND (m.rok = fp.rok)
WHERE m.rok = Forms!suma_przychodow_w_danym_roku_miesiecznie!RokRaport
GROUP BY m.rok, m.miesiac
ORDER BY m.rok, m.miesiac;
```

Description: Contains monthly revenue for a given year. The sum of gross prices from invoice items is grouped by year and month, with missing data in a given month showing a value of 0.



## Reports

### oblozenie_pokoi_w_danym_okresie

![image](https://github.com/user-attachments/assets/d7a8857f-82d5-4a83-a080-5ddbf45610a6)

![image](https://github.com/user-attachments/assets/81c908f1-1dd0-41b5-9843-0f33f2cea14b)



Description: This report is generated based on the query oblozenie_pokoi_w_danym_okresie through the oblozenie_pokoi_w_danym_okresie form. It provides information on the number of reservations for a specific room number within a given time period (from January 1, 2023, to January 1, 2024), including the dates for which reservations have been made.

### oblozenie_w_danym_okresie

![image](https://github.com/user-attachments/assets/a3a05a14-b4b0-46f2-a34d-e18d25895bb4)

![image](https://github.com/user-attachments/assets/21a02855-51ee-4f2d-95cf-9482e5d92b52)


Description: This report is generated based on the query oblozenie_w_danym_okresie through the oblozenie_w_danym_okresie form. It provides information on the number of rooms reserved during a specified period (from … to …, with the example period being January 1, 2023, to January 1, 2024).

### oblozenie_w_danym_roku

![image](https://github.com/user-attachments/assets/212f2018-fc2c-4e98-8d06-64bd1c5fd56f)

![image](https://github.com/user-attachments/assets/005e963c-32fb-4fca-bd19-3435ecaf908a)



Description: This report is generated based on the query oblozenie_w_danym_roku through the oblozenie_w_danym_roku form. It provides information on the number of rooms reserved in the user-specified year (in this case, the year 2023).

### oblozenie_w_danym_roku_miesieczne

![image](https://github.com/user-attachments/assets/3894a1d8-040c-4f30-a3d5-bfc44fecd142)

![image](https://github.com/user-attachments/assets/280f075d-db28-431b-8855-e19235cbe299)


Description: This report is generated based on the query oblozenie_w_danym_roku_miesiecznie through the oblozenie_w_danym_roku_miesiecznie form. It provides information on the number of rooms reserved in the user-specified year, broken down by month (for example, all months of 2023).

### RaWolnePokoje

![image](https://github.com/user-attachments/assets/5f693f8f-0460-442d-adec-40c3fa633706)

Description: This report is generated based on the query KwWolnePokoje through the AplikacjaHotel form. It provides information on the available rooms in the hotel.

### RaZajetePokoje

![image](https://github.com/user-attachments/assets/f07c1495-653d-458d-9750-7432ab71eb64)

Description: This report is generated based on the query KwZajetePokoje through the AplikacjaHotel form. It provides information on the occupied rooms in the hotel.

### rezerwacjeNadchodzące

![image](https://github.com/user-attachments/assets/ac1ed21d-6c7b-4fb6-9b6d-6339b9d8db23)

Description: This report is generated based on the query rezerwacjeNadchodzące through the AplikacjaHotel form. It provides information on upcoming reservations in the hotel—those with an arrival date within the next 7 days.

### rezerwacjeTrwające

![image](https://github.com/user-attachments/assets/0c7ba1a8-b146-403c-ac86-4cc9818707cb)

Description: This report is generated based on the query rezerwacjeTrwające through the AplikacjaHotel form. It provides information on current ongoing reservations in the hotel.

### suma_przychodow_w_danym_okresie

![image](https://github.com/user-attachments/assets/a26ee809-5ddd-42f3-9b50-341cbc727adc)

![image](https://github.com/user-attachments/assets/3c0bc901-0b96-48ce-affa-157f0d20f6c7)

Description: This report is generated based on the query suma_przychodow_w_danym_okresie through the suma_przychodow_w_danym_okresie form. It provides information on the total revenue achieved by the hotel for a specified period (from … to …, with the example period being January 1, 2023, to January 1, 2024).

### suma_przychodow_w_danym_roku

![image](https://github.com/user-attachments/assets/47d7580e-7335-4036-8f90-4a7926b0d1ef)

![image](https://github.com/user-attachments/assets/9e5c226d-063e-4b94-804d-4e2452b5f6e5)

Description: This report is generated based on the query suma_przychodow_w_danym_roku through the suma_przychodow_w_danym_roku form. It provides information on the total revenue achieved by the hotel for the user-specified year (in this case, the year 2023).

### suma_przychodow_w_danym_roku_kwartalnie

![image](https://github.com/user-attachments/assets/d782bd87-3fda-4b62-895d-3d861a263756)

![image](https://github.com/user-attachments/assets/50407169-08a1-45b5-a65c-9fdee1ca55d6)

Description: This report is generated based on the query suma_przychodow_w_danym_roku_kwartalnie through the suma_przychodow_w_danym_roku_kwartalnie form. It provides information on the total revenue achieved by the hotel for the user-specified year, broken down by quarters (for example, quarters of 2023).

### suma_przychodow_w_danym_roku_miesiecznie

![image](https://github.com/user-attachments/assets/f2b3f98f-46bc-4e55-a9f4-c5572c159e60)

![image](https://github.com/user-attachments/assets/a522cbf0-fe2a-4e0e-ac6c-433c9cd5a13b)


Description: This report is generated based on the query suma_przychodow_w_danym_roku_miesiecznie through the suma_przychodow_w_danym_roku_miesiecznie form. It provides information on the total revenue achieved by the hotel for the user-specified year, broken down by months.


## Templates

### WzórFaktury

![image](https://github.com/user-attachments/assets/0a9212cc-fb35-49e5-9198-fc3bd191e81b)


Description: This report contains the invoice template onto which data is applied when generating invoices in the Aplikacja Hotel system.



## Forms


### AplikacjaHotel

![image](https://github.com/user-attachments/assets/c443eb1e-1d8f-4f84-9dad-708360c11c4e)
![image](https://github.com/user-attachments/assets/2fadba07-036c-4b73-aa25-eacf30c7b546)
![image](https://github.com/user-attachments/assets/a792e0d5-0311-4596-a3a4-91805d291e96)
![image](https://github.com/user-attachments/assets/7d731016-d895-469e-bcdb-5f507a5bd41d)
![image](https://github.com/user-attachments/assets/db3c2b01-dd88-4b93-a9f8-301a377358eb)
![image](https://github.com/user-attachments/assets/38e7673c-b1d7-49fb-9c2d-6f4b5e7fdec9)
![image](https://github.com/user-attachments/assets/17d08322-54c7-4576-88f6-0e1d23f15c4e)
![image](https://github.com/user-attachments/assets/b5c6b52c-6997-4c7c-a7b7-9cd8ae1c4554)
![image](https://github.com/user-attachments/assets/c238d0d1-a386-4c88-937e-f91d6801826d)
![image](https://github.com/user-attachments/assets/95625108-6dda-4b0a-9199-584f62e8ed8c)
![image](https://github.com/user-attachments/assets/8fbe7e7b-1ab8-49fe-9f6d-f5bd9e2f4c24)
![image](https://github.com/user-attachments/assets/780ec303-da6a-4b31-af38-e2267fdbaaae)
![image](https://github.com/user-attachments/assets/0a5e6897-e33f-4a0e-86c5-7fb07c762fae)
![image](https://github.com/user-attachments/assets/b25be61a-2d25-41df-8cee-1230ea967277)


Description: This form is a fundamental part of the GUI for the project. It allows for checking in and checking out guests, as well as canceling previously made reservations. It includes a room reservation system for selecting stay dates, checking room availability for the specified dates, choosing a room, and making a reservation. It also manages all project tables and generates and prints invoices. Additionally, it provides access to generate the reports mentioned above.

### FoFaktura

![image](https://github.com/user-attachments/assets/07f591f2-257e-4dec-b775-c6d316aa6f30)


Description: This form allows for generating and printing invoices using the invoice template filled with information from the relevant fields in the form, such as VAT number, company name, etc.

### FoFakturaPozycje

![image](https://github.com/user-attachments/assets/0bb5841e-6c72-49a9-9445-0699e0669af5)


Description: This form allows for deleting invoices.

### FoHotel

![image](https://github.com/user-attachments/assets/63032ec4-e010-49da-801d-483a59b6d944)


Description: This form displays information about a specific hotel.

### FoInneFormularze

![image](https://github.com/user-attachments/assets/f14137d9-4333-4984-b209-e1365aabd164)
![image](https://github.com/user-attachments/assets/f47e7af2-8c83-4bfa-8bf1-bfae634acddf)
![image](https://github.com/user-attachments/assets/8ff5ac05-cbe7-4970-9152-973234c13116)
![image](https://github.com/user-attachments/assets/62ac250e-46fa-4197-85ae-8c97557567ea)
![image](https://github.com/user-attachments/assets/9fb4d69a-bf41-4ed1-a992-bdaa71ad5906)


Description: This form allows for managing the tables for Hotel, RoomType, PaymentMethod, Employee, and Position.

### FoKlient

![image](https://github.com/user-attachments/assets/4868f30b-2e82-4e3f-951e-694c221b13a5)


Description: This form allows for managing the Client table.

### FoMetodaPłatności

![image](https://github.com/user-attachments/assets/251c27fa-d831-4958-a576-2cff891cda5c)


Description: This form allows for managing the PaymentMethod table.

### FoPokoje

![image](https://github.com/user-attachments/assets/5ae5c1f7-577f-41de-80a3-caa9fd434e16)


Description: This form displays rooms.

### FoPracownik

![image](https://github.com/user-attachments/assets/b37a1bf6-2a1c-42fd-8fc7-075e3be1b590)


Description: This form allows for managing the Employee table.

### FoRaporty

![image](https://github.com/user-attachments/assets/0160aa24-1c3e-4bff-a38d-71824374dd8f)


Description: This form allows for generating all project reports through the appropriate forms.

### FoRezerwacja

![image](https://github.com/user-attachments/assets/2b07221a-4ddc-4274-ae1f-8d443e8ec241)


Description: This form allows for managing the Reservation table.

### FoRezerwacjeNadchodzące

![image](https://github.com/user-attachments/assets/38cef5fb-7c82-40a8-8480-7b60117a7613)


Description: This form allows for checking in and canceling reservations.

### FoRezerwacjeTrwające

![image](https://github.com/user-attachments/assets/c75b3f01-a3d1-4d61-8a98-856f87a1f3ef)


Description: This form allows for checking out a guest from a room.

### FoSkracanie

![image](https://github.com/user-attachments/assets/cb3e5c18-ce6e-470f-94eb-84206efbb860)


Description: This form allows for shortening a stay.

### FoStanowisko

![image](https://github.com/user-attachments/assets/3ac490e9-30a0-41c5-94e6-56426f933639)


Description: This form allows for managing the Position table.

### FoTypPokoju

![image](https://github.com/user-attachments/assets/a38f6489-6b83-485c-bedf-20b9a2db014b)


Description: This form allows for managing the RoomType table.

### ListaPokoiDoPrzedluzenia

![image](https://github.com/user-attachments/assets/5e3250fd-23fc-4de3-8a41-6b6810581f50)
![image](https://github.com/user-attachments/assets/d45f0c35-92f5-484d-801e-64c867fef41b)


Description: This form allows for extending a stay.

### oblozenie_pokoi_w_danym_okresie

![image](https://github.com/user-attachments/assets/5c022b5e-2979-4326-8aa3-1e3e578547a5)
![image](https://github.com/user-attachments/assets/9758cb57-c03a-474d-9ea9-7f62e90e879f)


Description: This form allows for generating the oblozenie_pokoi_w_danym_okresie report by entering the data for which the report should be generated (e.g., from January 1, 2023, to January 1, 2024).

### oblozenie_w_danym_okresie

![image](https://github.com/user-attachments/assets/ea6d83ab-353c-416a-84b7-1aac3ade865e)
![image](https://github.com/user-attachments/assets/fcd11831-8a81-45d9-8a5e-7b7fed76c78a)


Description: This form allows for generating the oblozenie_w_danym_okresie report by entering the data for which the report should be generated (e.g., from January 1, 2023, to January 1, 2024).

### oblozenie_w_danym_roku

![image](https://github.com/user-attachments/assets/77dbf0bc-d670-40fe-8ed7-cb0cd0eac905)
![image](https://github.com/user-attachments/assets/1c6e78bd-90f1-4491-8669-df16e5e95dbc)


Description: This form allows for generating the oblozenie_w_danym_roku report by entering the data for which the report should be generated (e.g., for the year 2023).

### oblozenie_w_danym_roku_miesiecznie

![image](https://github.com/user-attachments/assets/cfa69e12-427f-4e2f-96c9-601200d07f2e)
![image](https://github.com/user-attachments/assets/a1368649-de72-498c-badb-cbe3b82f74ed)


Description: This form allows for generating the oblozenie_w_danym_roku_miesiecznie report by entering the data for which the report should be generated (e.g., for the year 2023).

### suma_przychodow_w_danym_okresie

![image](https://github.com/user-attachments/assets/a4508815-9419-4324-9c67-8b45d8f44254)
![image](https://github.com/user-attachments/assets/d11ddd68-d773-4961-9986-44e19abf993e)

Description: This form allows for generating the suma_przychodow_w_danym_okresie report by entering the data for which the report should be generated (e.g., from January 1, 2023, to January 1, 2024).

### suma_przychodow_w_danym_roku

![image](https://github.com/user-attachments/assets/cdf70380-261f-40bb-9419-fcde0d3f4634)
![image](https://github.com/user-attachments/assets/5d487d48-0c48-4729-9dc2-53e5af5b67a0)

Description: This form allows for generating the suma_przychodow_w_danym_roku report by entering the data for which the report should be generated (e.g., for the year 2023).

### suma_przychodow_w_danym_roku_kwartalnie

![image](https://github.com/user-attachments/assets/8a21a9e5-e873-41de-8ac1-2c686d579ddf)
![image](https://github.com/user-attachments/assets/7ace57e6-6a96-484f-adf9-95a1857cd79e)


Description: This form allows for generating the suma_przychodow_w_danym_roku_kwartalnie report by entering the data for which the report should be generated (e.g., for the year 2023).

### suma_przychodow_w_danym_roku_miesiecznie

![image](https://github.com/user-attachments/assets/659ba1fe-338d-483c-af88-07d11b9c9bae)
![image](https://github.com/user-attachments/assets/f165e6cd-9ec2-4add-8772-78c6ba58ff99)


Description: This form allows for generating the suma_przychodow_w_danym_roku_miesiecznie report by entering the data for which the report should be generated (e.g., for the year 2023).

### wolne_pokoje_w_danym_terminie

![image](https://github.com/user-attachments/assets/fa5c1d8e-cfa0-4424-aa85-519ef26199eb)

Description: This form allows for displaying a list of available rooms using data retrieved from the AplikacjaHotel form (e.g., from January 1, 2023, to January 1, 2024).
