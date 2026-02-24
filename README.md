# 1. Introduction
This project presents a relational SQLite database that simulates energy usage, water consumption, and environmental monitoring across a smart campus.<br>
The database was fully generated using Python in Google Colab to ensure:<br>
&nbsp;&nbsp;&nbsp;&nbsp;* Realistic and reproducible data<br/>
&nbsp;&nbsp;&nbsp;&nbsp;* Data integrity through foreign and compound keys<br/>
&nbsp;&nbsp;&nbsp;&nbsp;* Compliance with assignment instructions<br/>
&nbsp;&nbsp;&nbsp;&nbsp;* No personal or sensitive information<br><br>
*&nbsp;&nbsp;The resulting database file is: smart_campus_energy.db

# 2. Data Generation Process
The database was generated programmatically using Python in Google Colab, following these steps:
## 2.1 Buildings Table
*&nbsp;&nbsp;Contains static information for 40 campus buildings<br/>
*&nbsp;&nbsp;Columns:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;1.&nbsp;&nbsp;building_type (nominal)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;2.&nbsp;&nbsp;department (nominal)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;3.&nbsp;&nbsp;building_area_sqm (ratio)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;4.&nbsp;&nbsp;sustainability_rating (ordinal)<br/>
*&nbsp;&nbsp;Random selection from predefined lists ensured realistic distribution.<br/>
*&nbsp;&nbsp;building_area_sqm uses 500–5000 m² to simulate real building sizes.<br/>
*&nbsp;&nbsp;Buildings.csv
## 2.2 EnergyUsage Table
*&nbsp;&nbsp;Stores energy and water consumption per building<br/>
*&nbsp;&nbsp;Columns:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;1.&nbsp;&nbsp;energy_source (nominal)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;2.&nbsp;&nbsp;energy_consumption_kwh (ratio)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;3.&nbsp;&nbsp;water_usage_liters (ratio)<br/>
*&nbsp;&nbsp;Each building has one usage record<br/>
*&nbsp;&nbsp;Relational integrity maintained with building_id as a foreign key<br/>
*&nbsp;&nbsp;EnergyUsage.csv 
## 2.3 UsageLogs Table
*&nbsp;&nbsp;Daily environmental logs for 30 days per building<br/>
*&nbsp;&nbsp;40 buildings × 30 days = 1,200+ rows<br/>
*&nbsp;&nbsp;Columns:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;1.&nbsp;&nbsp;temperature_celsius (interval)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;2.&nbsp;&nbsp;occupancy_level (ordinal)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;3.&nbsp;&nbsp;air_quality_index (interval)<br/>
*&nbsp;&nbsp;Uses a compound primary key (building_id, log_date) to prevent duplicates<br/>
*&nbsp;&nbsp;UsageLogs.csv <br><br>
*&nbsp;&nbsp;Python randomization ensured that values were realistic and consistent for all data types (nominal, ordinal, interval, ratio).

# 3. Database Schema
## 3.1 Buildings Table
| Column                | Data Type | Notes                                                       |
|-----------------------|-----------|-------------------------------------------------------------|
| building_id           | INTEGER   | Primary Key                                                 |
| building_name         | TEXT      | Unique identifier                                           |
| building_type         | TEXT      | Nominal: Academic, Residential, Laboratory, Administrative |
| department            | TEXT      | Nominal: Department responsible                             |
| building_area_sqm     | REAL      | Ratio: 0+ m², meaningful zero                               |
| sustainability_rating | TEXT      | Ordinal: Poor → Excellent                                   |



## 3.2 EnergyUsage Table
| Column                 | Data Type | Notes                                         |
|------------------------|-----------|-----------------------------------------------|
| usage_id               | INTEGER   | Primary Key                                   |
| building_id            | INTEGER   | Foreign Key → Buildings.building_id           |
| energy_source          | TEXT      | Nominal: Grid, Solar, Wind                    |
| energy_consumption_kwh | REAL      | Ratio: 0+ kWh                                 |
| water_usage_liters     | REAL      | Ratio: 0+ liters                              |

## 3.3 UsageLogs Table
| Column              | Data Type | Notes                                   |
|---------------------|-----------|-------------------------------------------|
| building_id         | INTEGER   | Foreign Key → Buildings.building_id      |
| log_date            | TEXT      | Date of record                           |
| temperature_celsius | REAL      | Interval: 0°C is arbitrary               |
| occupancy_level     | TEXT      | Ordinal: Low < Medium < High             |
| air_quality_index   | INTEGER   | Interval: relative AQI scale             |
| Primary Key         | building_id + log_date | Ensures unique daily log per building |
### Relationships:
*&nbsp;&nbsp;EnergyUsage.building_id → Buildings.building_id<br/>
*&nbsp;&nbsp;UsageLogs.building_id → Buildings.building_id

# 4. Justification for Separate Tables
*&nbsp;&nbsp;Buildings Table: Holds static attributes; avoids duplication in other tables.<br/>
*&nbsp;&nbsp;EnergyUsage Table: Stores energy and water consumption separately for clarity and normalization.<br/>
*&nbsp;&nbsp;UsageLogs Table: Stores daily monitoring data with a compound key to prevent duplicate entries.<br/>

### Constraints enforce:
*&nbsp;&nbsp;Nominal/ordinal categories via CHECK constraints<br/>
*&nbsp;&nbsp;Non-negative ratio/interval values<br/>
*&nbsp;&nbsp;Referential integrity via foreign keys<br>
*&nbsp;&nbsp;This structure supports realistic, normalized, and relationally consistent data.

# 5. Ethical and Data Privacy Considerations
*&nbsp;&nbsp;All data is synthetic, with no personal or sensitive information.<br/>
*&nbsp;&nbsp;Building identifiers (Building_1, Building_2, etc.) are simulated.<br/>
*&nbsp;&nbsp;Randomized values simulate real-world energy usage while maintaining privacy.<br/>
*&nbsp;&nbsp;This ensures compliance with data protection and ethical guidelines.

# 6. Conclusion
The Smart Campus Energy Usage & Sustainability database:<br/>
*&nbsp;&nbsp;Meets all assignment requirements: ≥7 columns, ≥1,000 rows, all 4 data types<br/>
*&nbsp;&nbsp;Implements foreign keys and a compound key for relational integrity<br/>
*&nbsp;&nbsp;Provides realistic, randomized synthetic data suitable for analysis<br/>
*&nbsp;&nbsp;Fully reproducible using Python in Google Colab<br/>

### Database download from Colab:<br/>
from google.colab import files<br/>
files.download("smart_campus_energy.db")

# 7. Appendix 
*&nbsp;&nbsp;The Python code used to generate the database is included in the Colab notebook.<br/>
smart_campus_energy.ipynb
