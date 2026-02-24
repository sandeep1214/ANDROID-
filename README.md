# 1. Introduction
This project presents a relational SQLite database that simulates energy usage, water consumption, and environmental monitoring across a smart campus.<br/>
The database was fully generated using Python in Google Colab to ensure:<br/>
<br>*Realistic and reproducible data<br/>
<br>*Data integrity through foreign and compound keys<br/>
<br>*Compliance with assignment instructions<br/>
<br>*No personal or sensitive information<br/>
<br>*The resulting database file is: smart_campus_energy.db

# 2. Data Generation Process
The database was generated programmatically using Python in Google Colab, following these steps:
## 2.1 Buildings Table
*Contains static information for 40 campus buildings<br/>
*Columns:<br/>
<br><br>1.building_type (nominal)<br/>
<br><br>2.department (nominal)<br/>
<br><br>3.building_area_sqm (ratio)<br/>
<br><br>4.sustainability_rating (ordinal)<br/>
<br>*Random selection from predefined lists ensured realistic distribution.<br/>
<br>*building_area_sqm uses 500–5000 m² to simulate real building sizes.<br/>
*Buildings.csv
## 2.2 EnergyUsage Table
*Stores energy and water consumption per building<br/>
*Columns:<br/>
1.energy_source (nominal)<br/>
2.energy_consumption_kwh (ratio)<br/>
3.water_usage_liters (ratio)<br/>
*Each building has one usage record<br/>
*Relational integrity maintained with building_id as a foreign key<br/>
*EnergyUsage.csv 
## 2.3 UsageLogs Table
*Daily environmental logs for 30 days per building<br/>
*40 buildings × 30 days = 1,200+ rows<br/>
*Columns:<br/>
1.temperature_celsius (interval)<br/>
2.occupancy_level (ordinal)<br/>
3.air_quality_index (interval)<br/>
*Uses a compound primary key (building_id, log_date) to prevent duplicates<br/>
*UsageLogs.csv <br/>
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
*EnergyUsage.building_id → Buildings.building_id<br/>
*UsageLogs.building_id → Buildings.building_id

# 4. Justification for Separate Tables
*Buildings Table: Holds static attributes; avoids duplication in other tables.<br/>
*EnergyUsage Table: Stores energy and water consumption separately for clarity and normalization.<br/>
*UsageLogs Table: Stores daily monitoring data with a compound key to prevent duplicate entries.<br/>

### Constraints enforce:
*Nominal/ordinal categories via CHECK constraints<br/>
*Non-negative ratio/interval values<br/>
*Referential integrity via foreign keys<br/>
This structure supports realistic, normalized, and relationally consistent data.

# 5. Ethical and Data Privacy Considerations
*All data is synthetic, with no personal or sensitive information.<br/>
*Building identifiers (Building_1, Building_2, etc.) are simulated.<br/>
*Randomized values simulate real-world energy usage while maintaining privacy.<br/>
*This ensures compliance with data protection and ethical guidelines.

# 6. Conclusion
The Smart Campus Energy Usage & Sustainability database:<br/>
*Meets all assignment requirements: ≥7 columns, ≥1,000 rows, all 4 data types<br/>
*Implements foreign keys and a compound key for relational integrity<br/>
*Provides realistic, randomized synthetic data suitable for analysis<br/>
*Fully reproducible using Python in Google Colab<br/>
Database download from Colab:<br/>
from google.colab import files<br/>
files.download("smart_campus_energy.db")

# 7. Appendix 
*The Python code used to generate the database is included in the Colab notebook.<br/>
smart_campus_energy.ipynb
