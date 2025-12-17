# Simulation Project: Closed & Open Queueing Networks

## Overview

This project simulates closed and open queueing network systems to analyze throughput, response times, and the impact of hardware upgrades and load balancing strategies.

**Date:** Fall 2025

---

## Part 1: Closed Queueing Network (Questions 1-5)

A system with N=40 jobs circulating through:
- **CPU**: 2 seconds average service time
- **Fast Disk**: 3 seconds average service time  
- **Slow Disk**: 30 seconds average service time
- **Rest Area**: 15 seconds average think time

### Q1: Load Balancing Strategy Comparison

**Objective:** Compare two load balancing strategies (Random, Proportional, JSQ) to maximize system throughput.

**Result:** JSQ (Join-Shortest-Queue) emerged as the optimal strategy with maximum throughput ~0.367 jobs/sec.

### Q2: Faster CPU Impact

**Objective:** Evaluate the impact of reducing CPU service time from 2s to 1s.

**Finding:** CPU upgrade had negligible impact (~0%) on throughput when disk is the bottleneck.

### Q3: Second Fast Disk Impact

**Objective:** Measure throughput and response time improvements by adding a second fast disk.

**Result:** 
- Throughput improvement: +35.9%
- Response time improvement: +27.4%

### Q4: Combined Improvements

**Objective:** Evaluate the combined effect of both upgrades (1s CPU + 2 fast disks).

**Finding:** Throughput reaches maximum ~0.700 jobs/sec (I/O bound by design).

### Q5: Performance Plots

**Objective:** Generate comparative plots across all 4 scenarios showing throughput and response time curves.

**Output:** `q5_final_plots.png` with side-by-side throughput and response time plots.

---

## Part 2: Open Queueing Network (Questions 1-2)

Jobs arrive via Poisson process (rate λ), process through CPU then disk, and leave.

- **CPU Service Rate:** 10 jobs/sec
- **Fast Disk Service Rate:** 12 jobs/sec
- **Slow Disk Service Rate:** 9 jobs/sec

### Q2a: Single Queue Strategy

Common queue for both disks with random routing.

### Q2b: Shortest Queue Strategy

Separate queues with JSQ load balancing from CPU to disk selection.


---

## Installation

### 1. Clone Repository
python3 -m venv venv

### 2. Create Virtual Environment

**macOS:**
python3 -m venv venv
source venv/bin/activate
**Windows:**
python -m venv venv
venv\Scripts\activate


### 3. Install Dependencies

pip install -r requirements.txt



