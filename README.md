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

## Part 2: Open Queueing Network

In the open network, jobs arrive from outside according to a Poisson process with rate λ, are processed by a single CPU, then by one of two disks, and finally leave the system. Service times are exponential.

- **CPU service rate:** μ_CPU = 10 jobs/sec  
- **Fast disk service rate:** μ_fast = 12 jobs/sec  
- **Slow disk service rate:** μ_slow = 9 jobs/sec  

The effective disk stage capacity is about 10.5 jobs/sec, so the **CPU is the theoretical bottleneck** and the maximum sustainable throughput is ≈ 10 jobs/sec. This is confirmed by simulation: as λ increases, throughput X tracks λ up to about 10 jobs/sec, at which point CPU utilization reaches 100% while both disks remain below full utilization.

### Disk queueing configurations

The project compares two queueing disciplines at the disk stage:

- **Single shared queue**

  A single common waiting line feeds both disks. Jobs leaving the CPU join a shared queue (modeled with a `simpy.Store`), and each disk repeatedly pulls the next job from this queue. This mirrors one physical line in front of two servers and tends to keep both disks well utilized.

- **Separate queues with shortest-queue routing**

  Each disk has its own queue (the internal `simpy.Resource` queues). When a job finishes at the CPU, the current queue lengths (including jobs in service) of the fast and slow disks are inspected, and the job is routed to the disk with fewer total jobs (ties are broken randomly). This implements a dynamic shortest-queue policy.

For representative arrival rates (e.g., λ = 5.0, 7.0, 8.5 jobs/sec), simulations show that both configurations are stable and that mean response times are very close. The **single shared queue** is consistently, but only slightly, better, which aligns with queuing theory intuition that pooling customers into one line reduces server idleness.


---

## Installation

### 1. Clone Repository

``git clone https://github.com/HardyUnine/Simulation25Fall-Project.git``

``cd Simulation25Fall-Project``

### 2. Create Virtual Environment

**macOS:**

``python3 -m venv venv``

``source venv/bin/activate``


**Windows:**

``python -m venv venv``

``./venv/Scripts/activate``


### 3. Install Dependencies

``pip install -r requirements.txt``
