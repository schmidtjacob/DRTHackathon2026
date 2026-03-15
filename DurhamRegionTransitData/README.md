# Dataset README
## Durham College 2026 Hackathon — Dataset Descriptions

This README describes the datasets included in this repository. They support analysis of transit vehicle preventative maintenance scheduling, PRESTO fare system ridership activity, and rider feedback for **Durham Region Transit (DRT)**, Ontario, Canada.

> **See also:** [GTFS_DATA_DICTIONARY.md](GTFS_DATA_DICTIONARY.md) for GTFS schedule and realtime data specifications.

---

## Repository Structure

```
├── 20260212_Preventative_Maintenance_Open_Activities.csv
├── Maintenance_2026_Hackathon_file_descriptions.xlsx
├── NEW_PM_Service-_Fluid_and_Filter_Requirements_June_19__2025.xlsx
├── PRESTO_field_definitions_and_data_types.xlsx
├── 2025_Dec_1-7_PRESTO_Ridership_Data.csv
├── Full Maintenance.zip
├── Full PRESTO.zip
├── RATE MY RIDE.zip
├── README.md
└── GTFS_DATA_DICTIONARY.md
```

---

## Sample Datasets

The following files in the root directory are samples intended for initial exploration and development.

### 1. `20260212_Preventative_Maintenance_Open_Activities.csv` *(a.k.a. "HotList")*

**Description:** A snapshot (as of February 12, 2026) of all open preventative maintenance (PM) work orders for transit vehicles. Known internally as the **HotList**, this file tracks buses that are due or overdue for scheduled inspections, along with odometer-based trigger data and work order details.

**Rows:** 206  
**Columns:** 24

| Field | Type | Description |
|---|---|---|
| `cgdivision` | String | Reporting division |
| `ownergroup` | String | Maintenance site responsible for the asset |
| `pmnum` | String | Preventative Maintenance record number |
| `pmdescription` | String | PM description — bus number and inspection type |
| `jpdescription` | String | Work order description — bus type, make, and inspection type |
| `nexttrigger` | Float | Odometer reading that will trigger the next inspection |
| `unitstogo` | Float | Kilometres remaining until next inspection is due |
| `alias` | String | **Bus number (short alias) — joins with GTFS-RT `vehicle.label` and Rate My Ride `vehicle_label`** |
| `assetdescription` | String | Vehicle year, type, make, and bus number |
| `locdescription` | String | Physical location of the asset |
| `metername` | String | Source of mileage information (e.g., Odometer) |
| `lastreading` | Float | Most recent odometer reading |
| `pmstatus` | String | Status of the PM record (e.g., ACTIVE) |
| `assetstatus` | String | Status of the asset (e.g., OPERATING) |
| `assetnum` | String | Unique asset identifier |
| `frequency` | Float | Scheduled inspection interval in kilometres |
| `tolerance` | Float | Allowable tolerance (km) around the scheduled inspection point |
| `wonum` | String | Work order number |
| `wodescription` | String | Work order description — bus number and inspection type |
| `reportdate` | DateTime | Date the inspection should occur |
| `lastpmwogenread` | Float | Odometer reading at the time the last work order was generated |
| `dayslate` | Integer | Number of days past the scheduled report date |
| `curjpdescription` | String | Current job plan description — bus type, make, and inspection type |
| `unitslate` | Integer | Kilometres past the scheduled inspection trigger |

### 2. `2025_Dec_1-7_PRESTO_Ridership_Data.csv`

**Description:** One week of PRESTO fare system transaction data covering December 1–7, 2025. Each row represents a single card tap event at a bus stop location. Customer identifiers are masked for privacy.

**Rows:** 63,443  
**Columns:** 8

| Field | Type | Definition |
|---|---|---|
| `transaction_key` | int | Unique identifier for a transaction (combined with `trxdate`) |
| `trxdate` | DATE | Date of the transaction |
| `trxtime` | TIME | Time of the transaction |
| `Transaction_type` | varchar | `Period Pass` = monthly pass tap; `E-Purse` = single pay-per-use tap |
| `trxlocationid` | string | **Bus stop ID — joins with GTFS `stops.stop_id`** |
| `loc_desc` | varchar | **Bus stop name — joins with GTFS `stops.stop_name`** |
| `Fare_Class` | varchar | Fare card class: `Adult`, `Youth`, `Senior`, `PS1` (Post-Secondary) |
| `masked_esn` | varchar | Anonymized fare card identifier |

---

## Full Datasets

For comprehensive analysis, complete datasets are available in the following archives. Extract the zip files to access the full data.

### `Full Maintenance.zip`

Contains the complete maintenance dataset corresponding to the sample HotList CSV above. Use this archive when you need the full historical or expanded scope of preventative maintenance records.

### `Full PRESTO.zip`

Contains the complete PRESTO ridership dataset corresponding to the sample week above. Use this archive when you need extended date ranges or the full scope of ridership transaction data.

---

## Rate My Ride Data

### `RATE MY RIDE.zip`

Extract this archive to access `DRTON_rate_my_ride.csv`.

**Description:** Rider feedback responses collected through the Rate My Ride feature in the Transit app. Each row represents a single user response to a survey question while riding DRT. User identifiers are hashed for privacy.

**Columns:** 30

| Field | Type | Description | GTFS Join |
|---|---|---|---|
| `answer_id` | String | Unique identifier for the response | — |
| `datetime_local_timezone` | DateTime | Time of response submission | — |
| `hashed_user_id` | String | Anonymized user identifier | — |
| `feed_name` | String | GTFS feed name | — |
| `route_short_name` | String | Short route name | **→ `routes.route_short_name`** |
| `route_long_name` | String | Full route name | **→ `routes.route_long_name`** |
| `network_name` | String | Network name in Transit app | — |
| `question_id` | String | Question identifier | — |
| `question_title` | String | Question text | — |
| `question_subtitle` | String | Question subtext | — |
| `answer_title` | String | Answer text | — |
| `followed_up_from_question_title` | String | Previous question (follow-ups only) | — |
| `followed_up_from_answer_title` | String | Previous answer (follow-ups only) | — |
| `user_trip_id` | String | User's trip identifier | — |
| `trip_id` | String | GTFS trip identifier | **→ `trips.trip_id`** |
| `stop_id` | String | Stop identifier | **→ `stops.stop_id`** |
| `stop_name` | String | Stop name | **→ `stops.stop_name`** |
| `stop_code` | String | Rider-facing stop code | **→ `stops.stop_code`** |
| `start_stop_id` | String | Boarding stop ID | **→ `stops.stop_id`** |
| `start_stop_lat` | Float | Boarding stop latitude | — |
| `start_stop_lng` | Float | Boarding stop longitude | — |
| `start_stop_name` | String | Boarding stop name | — |
| `start_stop_code` | String | Boarding stop code | — |
| `end_stop_id` | String | Alighting stop ID | **→ `stops.stop_id`** |
| `end_stop_lat` | Float | Alighting stop latitude | — |
| `end_stop_lng` | Float | Alighting stop longitude | — |
| `end_stop_name` | String | Alighting stop name | — |
| `end_stop_code` | String | Alighting stop code | — |
| `vehicle_id` | String | GTFS-RT vehicle ID | **→ GTFS-RT `vehicle.id`** |
| `vehicle_label` | String | Bus number | **→ GTFS-RT `vehicle.label`, PM `alias`** |
| `trip_has_real_time` | Boolean | Real-time data availability | — |

---

## Reference Files

### `Maintenance_2026_Hackathon_file_descriptions.xlsx`

Data dictionary for the HotList (PM Open Activities) dataset.

### `NEW_PM_Service-_Fluid_and_Filter_Requirements_June_19__2025.xlsx`

Fluid and filter requirements for PM service levels (A, B, C, D). Multi-row header structure — use `header=[0,1]` in pandas.

### `PRESTO_field_definitions_and_data_types.xlsx`

Data dictionary for PRESTO ridership data.

---

## GTFS Data — External Data Source

Durham Region Transit publishes GTFS data that can be joined with hackathon datasets.

> **Full documentation:** See [GTFS_DATA_DICTIONARY.md](GTFS_DATA_DICTIONARY.md)

### Quick Access

| Resource | URL |
|---|---|
| GTFS Static Feed | https://opendata.durham.ca/datasets/931bc536b42e4b3aa72270dab4133c90 |
| Durham Open Data | https://opendata.durham.ca/search?tags=Durham%20Transit |
| GTFS-RT (Realtime) | https://www.transit.land/feeds/f-dpz-durhamregiontransit~rt |

### Key GTFS Files

| File | Purpose | Key Fields |
|---|---|---|
| `stops.txt` | Stop locations | `stop_id`, `stop_code`, `stop_name`, `stop_lat`, `stop_lon` |
| `routes.txt` | Route definitions | `route_id`, `route_short_name`, `route_long_name` |
| `trips.txt` | Trip instances | `trip_id`, `route_id`, `service_id` |
| `stop_times.txt` | Arrival/departure times | `trip_id`, `stop_id`, `arrival_time`, `departure_time` |
| `calendar.txt` | Service schedules | `service_id`, days of week, date range |

### GTFS Realtime Entities

| Entity | Purpose | Key Fields |
|---|---|---|
| VehiclePosition | Live vehicle locations | `vehicle.id`, `vehicle.label`, `position`, `trip.trip_id` |
| TripUpdate | Arrival predictions | `trip.trip_id`, `stop_time_update[]`, `delay` |
| ServiceAlert | Disruption notices | `cause`, `effect`, `header_text`, `informed_entity[]` |

---

## Dataset Relationships — Join Keys

```
GTFS (Schedule/Realtime)         Hackathon Datasets
────────────────────────         ──────────────────
stops.stop_id            ◄────── PRESTO.trxlocationid
stops.stop_name          ◄────── PRESTO.loc_desc
stops.stop_id            ◄────── RateMyRide.stop_id
stops.stop_code          ◄────── RateMyRide.stop_code
routes.route_short_name  ◄────── RateMyRide.route_short_name
routes.route_long_name   ◄────── RateMyRide.route_long_name
trips.trip_id            ◄────── RateMyRide.trip_id
vehicle.id (RT)          ◄────── RateMyRide.vehicle_id
vehicle.label (RT)       ◄────── RateMyRide.vehicle_label
vehicle.label (RT)       ◄────── PM_Maintenance.alias
```

### Join Key Summary

| From Dataset | Field | To Dataset | Field |
|---|---|---|---|
| PRESTO | `trxlocationid` | GTFS | `stops.stop_id` |
| PRESTO | `loc_desc` | GTFS | `stops.stop_name` |
| Rate My Ride | `stop_id` | GTFS | `stops.stop_id` |
| Rate My Ride | `route_short_name` | GTFS | `routes.route_short_name` |
| Rate My Ride | `trip_id` | GTFS | `trips.trip_id` |
| Rate My Ride | `vehicle_label` | GTFS-RT | `vehicle.label` |
| Rate My Ride | `vehicle_label` | PM Maintenance | `alias` |
| PM Maintenance | `alias` | GTFS-RT | `vehicle.label` |

---

## Quick Start — Python

```python
import pandas as pd
import partridge as ptg

# Load GTFS
feed = ptg.load_feed('gtfs.zip')

# Load PRESTO and join with stop coordinates
presto = pd.read_csv('2025_Dec_1-7_PRESTO_Ridership_Data.csv')
presto_geo = presto.merge(
    feed.stops[['stop_id', 'stop_lat', 'stop_lon']],
    left_on='trxlocationid',
    right_on='stop_id',
    how='left'
)

# Load Rate My Ride and join with route info
rmr = pd.read_csv('DRTON_rate_my_ride.csv')
rmr_routes = rmr.merge(
    feed.routes[['route_short_name', 'route_id', 'route_type']],
    on='route_short_name',
    how='left'
)
```

---

## Hackathon Use Cases

1. **Maintenance Optimization:** Correlate PM schedules (`alias`) with ridership patterns to minimize service disruption.

2. **Route Performance:** Join Rate My Ride feedback with GTFS routes to identify satisfaction issues by route.

3. **Geographic Analysis:** Add coordinates to PRESTO taps via GTFS `stops.txt` for spatial visualization.

4. **Vehicle Tracking:** Link Rate My Ride `vehicle_label` with PM Maintenance `alias` to connect rider feedback with maintenance history.

5. **On-Time Performance:** Compare GTFS-RT predictions with static schedules using `trip_id` as the join key.

---

## Additional Resources

- **GTFS Documentation:** https://gtfs.org/
- **Durham Open Data:** https://opendata.durham.ca/
- **GTFS Validator:** https://gtfs-validator.mobilitydata.org/