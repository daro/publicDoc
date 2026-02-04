# Naming Convention Standard (SQL) – Team Agreement

## Cel (Purpose)
Ten dokument opisuje standard nazewnictwa, którego używamy w bazie **HealthOne**, aby cały zespół tworzył **ERD**, **SQL** i dokumentację w sposób spójny.

---

## Co ustandaryzowaliśmy (What we standardised)

### 1) Nazwy tabel (Table names)
- `snake_case`
- rzeczowniki w liczbie pojedynczej (np. `patient`, `doctor`, `hospital`, `prescription`)
- bez sufiksów normalizacji (np. usunięte `_3nf`, `_2nf` itp. w finalnym projekcie)

### 2) Nazwy kolumn (Column names)
- `snake_case`
- opisowe i konsekwentne w całym schemacie (te same pojęcia = te same nazwy w różnych tabelach)

### 3) Klucze główne (Primary keys, PK)
- format: `<table>_id` dla większości tabel głównych  
  **Przykłady:**  
  - `patient.patient_id`  
  - `doctor.doctor_id`  
  - `hospital.hospital_id`  
  - `drug.drug_id`  
  - `insurance.insurance_id`
- gdy naturalny identyfikator jest inny, nazywamy go jednoznacznie  
  **Przykłady:** `rx_id` dla `prescription`, `visit_id` dla `visit`
- dla tabel łączących (junction tables) stosujemy klucze złożone z ID referencji  
  **Przykład:** `doctor_hospital(doctor_id, hospital_id)`

### 4) Klucze obce (Foreign keys, FK)
- używamy tej samej nazwy kolumny co referencjonowany PK (jeśli to możliwe)  
  **Przykład:** `visit.patient_id -> patient.patient_id`
- dla relacji samoreferencyjnych (recursive/self-reference) nazywamy FK explicite  
  **Przykład:** `patient.insurance_holder_patient_id -> patient.patient_id`

### 5) Nazwy constraintów (zalecane) (Constraint names – recommended)
- PK constraints: `pk_<table>`
- FK constraints: `fk_<from_table>_<to_table>` *(albo `fk_<from_table>_<column>` jeśli czytelniejsze)*
- Unique constraints: `uq_<table>_<column(s)>`
- Indexes: `ix_<table>_<column(s)>`

---

## Dlaczego to pomaga (Impact on our work)
- **Czytelność ERD:** relacje są prostsze do odczytania, bo nazwy PK/FK są przewidywalne.
- **Szybsze pisanie SQL:** łatwiej “zgadnąć” nazwy kolumn bez ciągłego sprawdzania schematu.
- **Mniej błędów:** mniej pomyłek w nazwach FK i warunkach JOIN.
- **Lepsza praca zespołowa:** każdy może niezależnie tworzyć skrypty/diagramy, które do siebie pasują.
- **Lepszy odbiór/ocena:** schemat wygląda profesjonalnie i jest łatwy do przejrzenia.

---

## Zasady kciuka (Rules of thumb)
- **Spójność jest ważniejsza** niż “idealny” styl.
- Nie mieszamy konwencji (np. `id` w jednej tabeli i `patient_id` w innej), chyba że jest ku temu jasno udokumentowany powód.
- Jeśli dodajemy nowe tabele/kolumny, stosujemy te same wzorce jak powyżej.

---

## Źródła / uzasadnienie (Sources / justification)
- **Zasady vendorów:** bazy mają ograniczenia dot. identyfikatorów i słów zastrzeżonych; `lowercase snake_case` zmniejsza potrzebę cudzysłowienia nazw.
- **Popularna praktyka:** `<table>_id` i identyczne nazwy FK upraszczają JOIN-y i czytanie schematu.
- **Guides/style:** spójne nazewnictwo constraintów i indeksów ułatwia debug i utrzymanie.

---

## Referencje (References)
- MySQL Reference Manual – Identifiers (zasady nazw identyfikatorów, quoting, reserved words)  
  https://dev.mysql.com/doc/en/identifiers.html
- SQL Style Guide (sqlstyle.guide) – guidance on naming + jawne nazwy constraintów  
  https://www.sqlstyle.guide/
- Navicat blog – przykład konwencji dla FK constraintów (`fk_...`)  
  https://www.navicat.com/en/company/aboutus/blog/2225-a-quick-guide-to-naming-conventions-in-sql-part-2
- Stack Overflow – praktyka `tablename_id` jako PK i dopasowane FK  
  https://stackoverflow.com/questions/7899200/is-there-a-naming-convention-for-mysql
- Stack Overflow – korzyść z identycznych nazw PK/FK (np. `JOIN ... USING()`)  
  https://stackoverflow.com/questions/1369593/primary-key-foreign-key-naming-convention

---

*End of note*
