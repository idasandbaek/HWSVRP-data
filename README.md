# HWSVRP Data Repository

This repository contains the input data, test instances and results for the Hybrid Weather-Dependent Supply Vessel Routing Problem (HWSVRP).

## Contents

| File | Description |
| --- | --- |
| `Data.txt` | Main instance definition in Python dictionary format. Includes locations with orders, charging locations, service times, coordinates, charging stations, vessel parameters, and routing constraints. |
| `Distance_matrix.txt` | Distance matrix for the locations. |
| `HYBRID_ShipPowerCurves.xml` | Three years of weather data from January 1st 2020 for an area in the North Sea. |
| `HYBRID_wavedata.nc` | Wave-condition dataset used to estimate environmental effects on vessel performance. |
| `Installation_data.xlsx` | Installation-related data and supporting operational inputs. |
| `Results.xlsx` | Output results or solution summaries from the optimization process. |

## Main data summary

The current data in `Data.txt` includes:

- A set of order and charging locations
- Coordinates for each location
- Service times `T_S` and opening hours
- Charging stations `locations_charging`
- Vessel parameters such as capacity, speed, and battery-related settings
- Routing parameters including depot, return time, preparation time, and time-step size

### Example parameters from the dataset

- Depot / origin: `o = 0`
- Destination / end node: `d = 31`
- Planning horizon / return time: `t_ret = 180`
- Preparation time: `t_prep = 34`
- Time step: `delta_t = 0.25`
- Energy consumption during servicing and charging (still water) `E = 125`
- Weather scenario: `start_hour = 1080`
- Electricity and fuel coefficients:
  - `C_E = 1.75`
  - `C_F = 1.2`

The pairs of locations represents the order location and the associated charging location. 



### Test Instance Generation

A total of **451 test instances** were generated to evaluate and compare the solution methods. The instances are constructed from **five instance groups**, as shown in the table below.

Each test instance is defined by three components:

1. A set of **order locations** from one of the five instance groups.
2. A **weather scenario**.
3. An **emission reduction target**, represented by the parameter $\alpha$.

For each instance group, test instances are generated using the first **4, 6, 8, ..., 22** order locations in the group, as well as an instance containing **all 23 order locations**. 

If an order location has an associated charging location, the corresponding charging location is also included in the instance.

For example, when the first four order locations of an instance group are selected, the order locations are **GFA, TRC, ISW, and TRA**. Any charging locations associated with these installations are included as well.

Three weather scenarios are considered: **Good, Medium, and Severe**. The scenarios are derived from historical weather data and are defined by a starting hour relative to **1 January 2020**:

| Weather scenario | Starting hour |
|------------------|---------------|
| Good             | 2400          |
| Medium           | 1080          |
| Severe           | 4040          |

The selected starting hour determines the weather conditions used throughout the instance.

For each combination of instance group, problem size, and weather scenario, three emission reduction targets are considered. The parameter $\alpha$ takes the following values:

- $\alpha = 0.3$
- $\alpha = 0.5$
- $\alpha = 1.0$

The parameter $\alpha$ specifies the allowed fraction of the reference emissions. Thus, lower values correspond to stricter emission reduction requirements.

Each instance is uniquely identified by its instance group, number of order locations, weather scenario, and $\alpha$ value.

The complete test set contains **451 instances**.



| Row | Random 1 | Random 2 | Random 3 | Random 4 | Random 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | GFA (4,5) | TRA (23,24) | MLA (9,10) | OSS (17) | TRA (23,24) |
| 2 | TRC (22) | STA (18) | OSC (13) | GFA (4,5) | NLN (12) |
| 3 | ISW (27) | CPR (26) | KVB (8) | KVB (8) | STA (18) |
| 4 | TRA (23,24) | OSO (16) | TRB (21) | OSC (13) | STB (19) |
| 5 | GFB (6) | MLB (11) | GFB (6) | CPR (26) | ASL (2) |
| 6 | STB (19) | DSS (3) | APT (1) | MLA (9,10) | DSS (3) |
| 7 | ASL (2) | STC (20) | VAL (25) | STB (19) | TRB (21) |
| 8 | NLN (12) | OSS (17) | DSS (3) | DSS (3) | GFA (4,5) |
| 9 | MLB (11) | OSC (13) | TRA (23,24) | ASL (2) | CPR (26) |
| 10 | APT (1) | GFA (4,5) | STC (20) | GFB (6) | GFC (7) |
| 11 | OSS (17) | GFB (6) | OSO (16) | VAL (25) | MLB (11) |
| 12 | OSC (13) | KVB (8) | OSS (17) | GFC (7) | STC (20) |
| 13 | GFC (7) | NLN (12) | TRC (22) | TRA (23,24) | OSE (14,15) |
| 14 | KVB (8) | VAL (25) | ISW (27) | OSO (16) | KVB (8) |
| 15 | DSS (3) | TRB (21) | GFA (4,5) | STA (18) | ISW (27) |
| 16 | OSO (16) | OSE (14,15) | NLN (12) | STC (20) | OSO (16) |
| 17 | OSE (14,15) | ASL (2) | MLB (11) | MLB (11) | VAL (25) |
| 18 | STA (18) | ISW (27) | STA (18) | TRB (21) | OSS (17) |
| 19 | TRB (21) | TRC (22) | STB (19) | NLN (12) | GFB (6) |
| 20 | VAL (25) | GFC (7) | GFC (7) | OSE (14,15) | MLA (9,10) |
| 21 | CPR (26) | STB (19) | OSE (14,15) | APT (1) | OSC (13) |
| 22 | MLA (9,10) | MLA (9,10) | ASL (2) | TRC (22) | APT (1) |


