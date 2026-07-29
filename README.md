# ✈️ Flight Delays Analysis — Power BI Dashboard

Anàlisi de **5.8 milions de vols dels EUA el 2015** per identificar patrons de retard, causes principals i rendiment per aerolínia i aeroport.

## 🔗 Dashboard Interactiu
**[👉 Veure el dashboard en viu](https://app.powerbi.com/view?r=eyJrIjoiNThlMGMwM2QtYzY1OS00MDEzLWE1YmEtNDgxM2E1NjUxZGNhIiwidCI6ImI5YTE0ZTYxLTUyYjAtNDFhNC04OGY3LWYzYjNmNmQ1ZDgwZiIsImMiOjh9)**

---

## 📊 Pàgines del Dashboard

| Pàgina | Contingut |
|---|---|
| 1 — Resum Executiu | KPIs globals, tendència anual i distribució de causes |
| 2 — Rendiment per Aerolínia | Rànquing de puntualitat, minuts acumulats i comparativa |
| 3 — Anàlisi per Aeroport | Top 15 aeroports origen i destinació, buscador |
| 4 — Causes del Retard | Distribució per motiu, evolució mensual i per aerolínia |
| 5 — Evolució Temporal | Tendències mensuals, per dia de la setmana i taula resum |

---

## 🔍 Insights Principals

- **Hawaiian Airlines** és l'aerolínia més puntual (89.50%), mentre que **Spirit Air Lines** és la pitjor (71.74%)
- **Juny** és el pitjor mes de l'any en puntualitat, coincidint amb l'inici de la temporada alta d'estiu
- La causa principal de retard és **l'avió tardà** (39.84%) — els retards es propaguen en cadena al llarg del dia
- **Atlanta (ATL)**, l'aeroport amb més vols, manté una puntualitat del 84.34% — per sobre de la mitjana nacional
- **Insight inesperat:** les aerolínies de menor volum no són necessàriament les més puntuals. Spirit Air Lines i Frontier Airlines, dues de les quatre aerolínies més petites del dataset, presenten els pitjors percentatges de puntualitat — contradient la intuïció inicial que les aerolínies grans pateixen més retards per saturació operativa

---

## 🛠️ Decisions Tècniques

**Modelat de dades (Star Schema):**
- Taula de fets: `flights` (5.8M registres)
- 4 taules de dimensió: `airlines`, `airports_origin`, `airports_destination`, `DimData`
- Role-playing dimensions per aeroports — dues taules separades per evitar problemes de cross-filter bidireccional

**Power Query:**
- Eliminació de columnes innecessàries per optimitzar el pes del model
- Creació de la columna `DATE` combinant `YEAR`, `MONTH` i `DAY`
- Creació de la columna `DELAY_REASON` amb lògica condicional per identificar la causa dominant de cada retard (inclou gestió de vols cancel·lats i desviats)
- Conversió de nulls a 0 a les columnes de causa de retard

**DAX (17 mesures):**
- Mesures base: `Total Vols`, `% Puntualitat`, `Retard Mitjà Arribada`, `% Cancel·lació`
- Mesures de causes: `Total Minuts` i `% Minuts` per a les 5 causes de retard
- `RANKX(ALL('airlines'), [% Puntualitat],, DESC)` per al rànquing dinàmic d'aerolínies
- `CALCULATE` amb `ALL(DimData)` per a valors globals independents del context temporal
- Objectius basats en benchmarks reals del DOT (Department of Transportation dels EUA)

**Funcionalitats avançades:**
- Sync Slicers entre les 5 pàgines
- Tooltips personalitzats amb mini-dashboard per aerolínia
- Format condicional amb regles basades en valors decimals
- Visuals KPI i Gauge amb objectius del sector
- Paràmetre per filtrar causes de retard al gràfic de línies
- Edit Interactions personalitzades entre visuals

---

## 📁 Dataset

**Font:** Kaggle — 2015 Flight Delays and Cancellations (USDOT)  
[🔗 Descarregar dataset](https://www.kaggle.com/datasets/usdot/flight-delays)

**Fitxers originals:**
- `flights.csv` — 5.8M registres de vols
- `airlines.csv` — 14 aerolínies
- `airports.csv` — aeroports dels EUA

---

## 🧰 Eines

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=flat&logo=microsoft&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=flat&logo=microsoft&logoColor=white)

---

## 👤 Autor

**Eudald** — PL-300 Microsoft Certified: Power BI Data Analyst  
[🔗 Certificació PL-300](https://learn.microsoft.com/api/credentials/share/en-gb/eudaldvalentisarra-7791/15650AE430BE5A11?sharingId=4ECDFAB7F1B78BAC)
