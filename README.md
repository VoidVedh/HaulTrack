# 🚛 HaulTrack

> **Fleet Telematics & Driver Safety for a 1,800-Truck Logistics Fleet**  
> *Course:* B.Tech CSE · **Software Engineering & Project Management (SEPM)**  
> *Case Study:* **No. 19 - HaulTrack**  
> *Student:* **Vedh Naik** (Roll No: `150096725163`) · *Cohort:* **Jensen Huang**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-06b6d4?style=for-the-badge&logo=googlechrome&logoColor=white)](https://voidvedh.github.io/HaulTrack/)
[![Fleet Size](https://img.shields.io/badge/Fleet-1%2C800%20Trucks-10b981?style=for-the-badge)](https://voidvedh.github.io/HaulTrack/)
[![Ingestion](https://img.shields.io/badge/Ingestion-5.18M%20records%2Fday-8b5cf6?style=for-the-badge)](https://voidvedh.github.io/HaulTrack/)
[![SEPM](https://img.shields.io/badge/SEPM-Case%20Study%2019-f59e0b?style=for-the-badge)](https://voidvedh.github.io/HaulTrack/)

👉 **[Launch Interactive Web Demo (GitHub Pages)](https://voidvedh.github.io/HaulTrack/)**

---

## 📌 Overview

**HaulTrack** is a fleet telematics and driver-safety system for a logistics firm with **1,800 trucks**, each reporting location, speed, harsh braking, idling and fuel level every **30 seconds**. One system has to satisfy three stakeholders with three definitions of success:

| Stakeholder | Wants | HaulTrack's answer |
| --- | --- | --- |
| **Fleet manager** | Route deviation alerts; a driver safety score | Dispatcher alerts with suppression rules; an advisory coaching score |
| **Drivers' union** | Assurance the score cannot be used for arbitrary dismissal | A written Data Use Policy: the score is never the basis for discipline |
| **Insurer** | Evidence that harsh braking has fallen | A frozen, terrain-normalised harsh-braking KPI served as aggregates |

The core engineering lesson:
> *"The previous vendor's score penalised drivers on hill routes. That was a requirements failure, not an algorithm failure."*

So fairness is written as **measurable requirements** (TN-1 to TN-7) and enforced by a regression test suite that fails the old algorithm.

---

## 🔑 Key Numbers

| Item | Result |
| --- | --- |
| Intermediate COCOMO (44 KLOC, semi-detached, EAF 1.15) | **239.0 person-months, about 17.0 months, about 14 FTE average** |
| Basic COCOMO (same size) | 207.9 person-months, about 16.2 months |
| Difference | +31.2 PM (+15%), all from the EAF |
| Daily ingestion | 1,800 × 2,880 = **5,184,000 records/day** (about 60/s average) |
| Retention | Raw 90 days · identified events 13 months · pseudonymised aggregates 36 months |

---

## 🏗️ Pipeline at a Glance

```
Truck unit -> Secure gateway -> Queue -> Validate/dedupe -> Enrich (map-match + road grade)
          -> Event detector (terrain-aware) -> Nightly scoring (28-day window)
          -> Manager console / Driver self-view / Insurer aggregates API
          -> Route deviation detector -> Dispatcher alerts (never feeds the score)
```

Terrain-aware harsh-braking thresholds (net deceleration, downhill bands): under 2% = 3.0 · 2 to under 5% = 3.3 · 5 to under 8% = 3.6 · 8% and above = 4.0 m/s².

---

## 📂 SEPM Project Deliverables

| # | Deliverable | File | Key contents |
| --- | --- | --- | --- |
| 1 | **Stakeholder Conflict Analysis** | [`01_Stakeholder_Conflict_Analysis_HaulTrack.pdf`](01_Stakeholder_Conflict_Analysis_HaulTrack.pdf) | Stakeholder register, 6 conflicts, gate + weighted-scoring prioritisation, 6 resolution decisions, terrain requirements TN-1..TN-7 |
| 2 | **Estimation Report** | [`02_Estimation_Report_HaulTrack.pdf`](02_Estimation_Report_HaulTrack.pdf) | Intermediate COCOMO, 15-driver table with justification, basic-model comparison |
| 3 | **Design Pack** | [`03_Design_Pack_HaulTrack.pdf`](03_Design_Pack_HaulTrack.pdf) | Ingestion sizing, pipeline architecture, scoring model, class diagram, route deviation activity diagram |
| 4 | **Test Design** | [`04_Test_Design_HaulTrack.pdf`](04_Test_Design_HaulTrack.pdf) | Terrain scoring tests, route deviation tests, hill-route regression (HR-01..05), policy tests |
| 5 | **Project Plan** | [`05_Project_Plan_HaulTrack.pdf`](05_Project_Plan_HaulTrack.pdf) | WBS, Gantt (74 weeks), communication plan, union concern as a risk, risk register |
| 6 | **Data Use Policy** | [`06_Data_Use_Policy_HaulTrack.pdf`](06_Data_Use_Policy_HaulTrack.pdf) | Retention, access control matrix, permitted and prohibited uses, appeals, governance |
| 7 | **Interactive Telematics Demo** | [**Live Web Demo**](https://voidvedh.github.io/HaulTrack/) · [`index.html`](index.html) | Standalone interactive UI demo: Terrain-Aware vs Legacy Scorer, Route Deviation Simulator with canvas, Data Use Policy Engine, Fleet Sizing |

---

## 🖥️ Interactive Web Demo

- **🌐 Live Demo (No installation required):** **[https://voidvedh.github.io/HaulTrack/](https://voidvedh.github.io/HaulTrack/)**
- **💻 Local Access:** Open [`index.html`](index.html) directly in any modern web browser.

The web app demonstrates all core SEPM requirements through interactive widgets:

- **🏔️ Terrain-Aware vs. Legacy Scorer:** Interactive grade-band and deceleration sliders comparing the fair, physics-grounded HaulTrack model against the unfair legacy vendor scoring that penalized hill drivers. Includes presets for key test scenarios (ST-01 flat-road harsh brake, ST-04 6% grade mitigation, ST-05 steep 9% grade, ST-07 unknown gradient, ST-12 low-mileage dampening, ST-13 score floor).
- **🗺️ Route Deviation Canvas Simulator:** Live HTML5 canvas tracking a delivery truck along a 500m safe corridor with 30-second tick steps, consecutive off-corridor notice transitions (0/3 to 3/3), escalation to dispatcher alerts, and 5 operational suppression toggles (Depot Geofence, Planned Stop, Road Closure, Dispatcher Reroute, GPS HDOP > 5.0).
- **🛡️ Data Use Policy Engine:** Interactive role & purpose evaluator testing governance rules (Driver Self-View, Manager Coaching, Insurer Aggregates, Disciplinary Score Export Blocking, and HR Panel Barred Use) with a live tamper-evident audit log.
- **📊 Fleet Architecture & Retention Lifecycle:** Live pipeline sizing metrics for 1,800 trucks (5.18M pings/day), COCOMO project estimates (44 KLOC, 239 PM), and 90-day / 13-month / 36-month data lifecycle stages.

---

## 📜 Academic Reference

- **Student:** Vedh Naik
- **Roll No.:** 150096725163
- **Cohort:** Jensen Huang
- **Course:** B.Tech Computer Science & Engineering · Software Engineering & Project Management
- **Problem Statement:** Case Study No. 19 - HaulTrack
- **Standards / models applied:** COCOMO 81 (Boehm), UML 2, MoSCoW prioritisation, IEEE 829-style test design
