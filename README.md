# HWSVRP Data Repository

This repository contains the input data, test instances and results for the Hybrid Weather-Dependent Supply Vessel Routing Problem (HWSVRP).

## Contents

| File | Description |
| --- | --- |
| `Data.txt` | Includes locations with orders, charging locations, service times, coordinates, paired locations and vessel parameters. |
| `Distance_matrix.txt` | Distance matrix for the locations. |
| `HYBRID_ShipPowerCurves.xml` | Power curves for a generic PSV under different weather states |
| `HYBRID_wavedata.nc` | Three years of weather data from January 1st 2020 for an area in the North Sea. |
| `Installation_data.xlsx` | Installation-related data and supporting operational inputs. |
| `Results.xlsx` | Results for running the different solution methods on the test instances. |

## Main data summary

### Structure of `Data.txt`

`Data.txt` is a Python dictionary-style input file that defines the full routing instance. The main blocks are:

- `locations_orders`: the set of order locations used in the instances. Each key is a location ID and the corresponding value stores the operational data for that node.
- `T_S`: service time at each location in time steps. For charging nodes, the service time is set to `0`.
- `locations_coordinates`: geographic coordinates for every location ID, including the depot and charging locations.
- `locations_charging`: charging locations and the maximum possible energy charged during service under still water conditions.
- `pairs`: the paired order/charging locations that share the same physical location, such as `(4,5)` for `GFA` and `(23,24)` for `TRA`.
- Global parameters such as `o`, `d`, `t_ret`, `t_prep`, `delta_t`, `E`, and `start_hour` define the parameter settings used for the instances.

### Location ID to name mapping

The internal IDs are mapped to location names as follows. Note that some IDs share the same physical site, which is why values such as `(4,5)` or `(23,24)` appear together.

| ID(s) | Location | Notes |
| --- | --- | --- |
| 0, 31 | MONG | Depot / start and return node |
| 1 | APT | Order location |
| 2 | ASL | Order location |
| 3 | DSS | Order location |
| 4, 5 | GFA | Charging location at 5 |
| 6 | GFB | Order location |
| 7 | GFC | Order location |
| 8 | KVB | Order location |
| 9, 10 | MLA | Charging location at 10 |
| 11 | MLB | Order location |
| 12 | NLN | Order location |
| 13 | OSC | Order location |
| 14, 15 | OSE | Charging location  at 15 |
| 16 | OSO | Order location |
| 17 | OSS | Order location |
| 18 | STA | Order location |
| 19 | STB | Order location |
| 20 | STC | Order location |
| 21 | TRB | Order location |
| 22 | TRC | Order location |
| 23, 24 | TRA | Charging location at 24 |
| 25 | VAL | Order location |
| 26 | CPR | Order location |
| 27 | ISW | Order location |
| 28 | WM1 | Charging location |
| 29 | WM2 | Charging location  |
| 30 | WM3 | Charging location  |

### Example parameters from the dataset

- Depot / origin: `o = 0`
- Destination / end node: `d = 31`
- Planning horizon / return time (in time steps): `t_ret = 180`
- Preparation time (in time steps): `t_prep = 34`
- Time step (in hours): `delta_t = 0.25`
- Energy consumption (kWh) during servicing and charging (still water conditions): `E = 125`
- Weather scenario: `start_hour = 1080`
- Electricity and fuel costs:
  - `C_E = 1.75`
  - `C_F = 1.2`

## Test Instance Generation

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


