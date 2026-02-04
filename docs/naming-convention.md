# Naming Convention Standard (SQL) – Team Agreement

## Purpose
This document describes the naming standard we use in the **HealthOne** database so everyone on the team writes **ERDs**, **SQL**, and documentation consistently.

---

## What we standardised

### 1) Table names
- `snake_case`
- singular nouns (e.g., `patient`, `doctor`, `hospital`, `prescription`)
- no normalisation suffixes (we removed `_3nf`, `_2nf`, etc. in the final design)

### 2) Column names
- `snake_case`
- descriptive and consistent across tables (same concepts = same names in different tables)

### 3) Primary keys (PK)
- format: `<table>_id` for most master tables  
  **Examples:**  
  - `patient.patient_id`  
  - `doctor.doctor_id`  
  - `hospital.hospital_id`  
  - `drug.drug_id`  
  - `insurance.insurance_id`
- when the natural identifier is different, we name it clearly  
  **Examples:** `rx_id` for `prescription`, `visit_id` for `visit`
- for junction tables we use composite keys made from the referenced IDs  
  **Example:** `doctor_hospital(doctor_id, hospital_id)`

### 4) Foreign keys (FK)
- use the same column name as the referenced PK whenever possible  
  **Example:** `visit.patient_id -> patient.patient_id`
- self-referencing FK (recursive relationship) is named explicitly  
  **Example:** `patient.insurance_holder_patient_id -> patient.patient_id`

### 5) Constraint names (recommended)
- PK constraints: `pk_<table>`
- FK constraints: `fk_<from_table>_<to_table>` (or `fk_<from_table>_<column>` if clearer)
- Unique constraints: `uq_<table>_<column(s)>`
- Indexes: `ix_<table>_<column(s)>`

---

## Why this helps (impact on our work)
- **ERD clarity:** relationships are easier to read because PK/FK names match and are predictable.
- **Faster SQL writing:** you can guess column names without checking every table.
- **Fewer bugs:** reduces mismatch errors (wrong FK column name, wrong join column).
- **Easier teamwork:** everyone can independently create scripts/diagrams that fit together.
- **Easier marking/review:** the schema looks professional and consistent, and reviewers can follow it quickly.

---

## Rules of thumb
- Consistency is more important than a “perfect” naming style.
- Don’t mix conventions (e.g., `id` in one table and `patient_id` in another) unless there is a clear documented reason.
- If we add new tables/columns, we follow the same patterns above.

---

## Sources / justification (why these conventions are common)
- **Vendor rules:** databases have identifier rules and reserved words; using lowercase `snake_case` reduces the need for quoting.
- **Widely used practice:** using `<table>_id` and matching FK names makes joins and schema reading simpler.
- **Style guidance:** naming constraints and indexes consistently makes debugging and maintenance easier.

---

## References
- MySQL Reference Manual – Identifiers (rules for naming identifiers, quoting, reserved words)  
  https://dev.mysql.com/doc/en/identifiers.html
- SQL Style Guide (sqlstyle.guide) – guidance on naming and explicitly naming constraints  
  https://www.sqlstyle.guide/
- Navicat blog – example conventions for naming foreign key constraints (`fk_...`)  
  https://www.navicat.com/en/company/aboutus/blog/2225-a-quick-guide-to-naming-conventions-in-sql-part-2
- Stack Overflow discussion – common practice: `tablename_id` PK and matching FK names  
  https://stackoverflow.com/questions/7899200/is-there-a-naming-convention-for-mysql
- Stack Overflow discussion – benefit of identical PK/FK names enabling `JOIN ... USING()`  
  https://stackoverflow.com/questions/1369593/primary-key-foreign-key-naming-convention

---

*End of note*
