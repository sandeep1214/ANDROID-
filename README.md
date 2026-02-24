# 1. Introduction
This project presents a relational SQLite database that simulates energy usage, water consumption, and environmental monitoring across a smart campus.<b/>
The database was fully generated using Python in Google Colab to ensure:<b/>
Realistic and reproducible data<b/>
Data integrity through foreign and compound keys<b/>
Compliance with assignment instructions<b/>
No personal or sensitive information<b/>
The resulting database file is: smart_campus_energy.db <b/>

# 2. Data Generation Process
The database was generated programmatically using Python in Google Colab, following these steps:
## 2.1 Buildings Table
Contains static information for 40 campus buildings<b/>
Columns:<b/>
obuilding_type (nominal)<b/>
odepartment (nominal)<b/>
obuilding_area_sqm (ratio)<b/>
osustainability_rating (ordinal)<b/>
Random selection from predefined lists ensured realistic distribution.<b/>
building_area_sqm uses 500–5000 m² to simulate real building sizes.<b/>
Buildings.csv<b/>
## 2.2 EnergyUsage Table
Stores energy and water consumption per building<b/>
Columns:<b/>
oenergy_source (nominal)<b/>
oenergy_consumption_kwh (ratio)<b/>
owater_usage_liters (ratio)<b/>
Each building has one usage record<b/>
Relational integrity maintained with building_id as a foreign key<b/>
EnergyUsage.csv <b/>
## 2.3 UsageLogs Table
Daily environmental logs for 30 days per building<b/>
40 buildings × 30 days = 1,200+ rows<b/>
Columns:<b/>
otemperature_celsius (interval)<b/>
ooccupancy_level (ordinal)<b/>
oair_quality_index (interval)<b/>
Uses a compound primary key (building_id, log_date) to prevent duplicates<b/>
UsageLogs.csv <b/>
Python randomization ensured that values were realistic and consistent for all data types (nominal, ordinal, interval, ratio).

# 3. Database Schema
## 3.1 Buildings Table
Column	Data Type	Notes
building_id	INTEGER	Primary Key
building_name	TEXT	Unique identifier
building_type	TEXT	Nominal: Academic, Residential, Laboratory, Administrative
department	TEXT	Nominal: Department responsible
building_area_sqm	REAL	Ratio: 0+ m², meaningful zero
sustainability_rating	TEXT	Ordinal: Poor → Excellent



## 3.2 EnergyUsage Table
Column	Data Type	Notes
usage_id	INTEGER	Primary Key
building_id	INTEGER	Foreign Key → Buildings.building_id
energy_source	TEXT	Nominal: Grid, Solar, Wind
energy_consumption_kwh	REAL	Ratio: 0+ kWh
water_usage_liters	REAL	Ratio: 0+ liters

## 3.3 UsageLogs Table
Column	Data Type	Notes
building_id	INTEGER	Foreign Key → Buildings.building_id
log_date	TEXT	Date of record
temperature_celsius	REAL	Interval: 0°C is arbitrary
occupancy_level	TEXT	Ordinal: Low < Medium < High
air_quality_index	INTEGER	Interval: relative AQI scale
Primary Key	building_id + log_date	Ensures unique daily log per building
### Relationships:
EnergyUsage.building_id → Buildings.building_id<b/>
UsageLogs.building_id → Buildings.building_id

# 4. Justification for Separate Tables
Buildings Table: Holds static attributes; avoids duplication in other tables.<b/>
EnergyUsage Table: Stores energy and water consumption separately for clarity and normalization.<b/>
UsageLogs Table: Stores daily monitoring data with a compound key to prevent duplicate entries.<b/>

### Constraints enforce:
Nominal/ordinal categories via CHECK constraints<b/>
Non-negative ratio/interval values<b/>
Referential integrity via foreign keys<b/>
This structure supports realistic, normalized, and relationally consistent data.

# 5. Ethical and Data Privacy Considerations
All data is synthetic, with no personal or sensitive information.<b/>
Building identifiers (Building_1, Building_2, etc.) are simulated.<b/>
Randomized values simulate real-world energy usage while maintaining privacy.<b/>
This ensures compliance with data protection and ethical guidelines.

# 6. Conclusion
The Smart Campus Energy Usage & Sustainability database:<b/>
Meets all assignment requirements: ≥7 columns, ≥1,000 rows, all 4 data types<b/>
Implements foreign keys and a compound key for relational integrity<b/>
Provides realistic, randomized synthetic data suitable for analysis<b/>
Fully reproducible using Python in Google Colab<b/>
Database download from Colab:<b/>
from google.colab import files<b/>
files.download("smart_campus_energy.db")

# 7. Appendix 
The Python code used to generate the database is included in the Colab notebook.<b/>
smart_campus_energy.ipynb
