# 🖥️ Computer Architecture Fundamentals for System Design

---
## Computer Architecture Overview
Before understanding large-scale distributed systems, we must understand the high-level architecture of a single computer. A computer is made up of layered components, each optimized for different tasks.

## 🏗️ Computer Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                     COMPUTER ARCHITECTURE                       │
│                                                                 │
│  ┌──────────────┐    ┌─────────────┐    ┌────────────────────┐  │
│  │     CPU      │    │   MEMORY    │    │      STORAGE       │  │
│  │              │    │             │    │                    │  │
│  │ ┌──────────┐ │    │    RAM      │    │  ┌─────┐ ┌─────┐   │  │
│  │ │L1 Cache  │ │◄──►│   ~100ns    │◄──►│  │ SSD │ │ HDD │   │  │
│  │ │  ~1ns    │ │    │  8-128GB    │    │  │100μs│ │10ms │   │  │
│  │ └──────────┘ │    │  Volatile   │    │  └─────┘ └─────┘   │  │
│  │ ┌──────────┐ │    └─────────────┘    │   Non-volatile     │  │
│  │ │L2 Cache  │ │                       └────────────────────┘  │
│  │ │ ~3-10ns  │ │                                               │
│  │ └──────────┘ │    ┌─────────────────────────────────────┐    │
│  │ ┌──────────┐ │    │            NETWORK                  │    │
│  │ │L3 Cache  │ │◄──►│                                     │    │
│  │ │~10-20ns  │ │    │  LAN: ~0.1-1ms                     │    │
│  │ │ Shared   │ │    │  Internet: ~10-100ms+ (SLOWEST)    │    │
│  │ └──────────┘ │    └─────────────────────────────────────┘    │
│  └──────────────┘                                               │
│                                                                 │
│  SPEED: L1 > L2 > L3 > RAM > SSD > HDD > Network              │
└─────────────────────────────────────────────────────────────────┘
```

## Core Components

### 1. Disk Storage (HDD / SSD)
- **Definition:** Long-term, persistent storage (data survives power loss).
- **Types:**
  - **HDD (Hard Disk Drive):** Cheaper, slower (80–160 MB/s typical).
  - **SSD (Solid State Drive):** More expensive, but much faster (500–3500 MB/s).
- **Capacity:** Hundreds of GB → multiple TB.
- **Uses:** Stores OS, applications, files, media, etc.
- **Units:**  
  - 1 byte = 8 bits (bit = 0 or 1).  
  - KB → MB → GB → TB (e.g., 1 TB ≈ 10¹² bytes).

### 2. RAM (Random Access Memory)
- **Definition:** Volatile memory; holds active data while programs run.
- **Quick access**: Allows CPU to rapidly read/write data
- **Properties:**
  - Much smaller than disk (GBs vs TBs).
  - Faster than disk (measured in microseconds, ~5000+ MB/s).
  - Loses data when power is off. (Volatile)
- **Use cases:**  
  - Stores program variables, intermediate computations, runtime stack.
  - Temporary workspace for active processes.

### 3. 🧠 CPU (Central Processing Unit): The Brain of the Computer
- **Definition:** The “brain” of the computer.
- **Responsibilities:**
  - Fetch, decode, and execute instructions.
  - Perform computations (arithmetic, logic).
  - Read/write to RAM, disk, cache.
- **Execution Flow:**
  - Code (written in high-level languages) → compiled into **machine code** (zeros/ones).
  - CPU interprets and runs instructions.
- **Limitations:**
  - Moore’s Law: CPU transistor count historically doubled every ~2 years → speed increased.
  - Plateau in recent years → can’t infinitely scale a single CPU.

#### The Compilation Process
```
High-Level Code → Compiler → Machine Code → CPU Execution
    (Java, C++,        (Translation)    (Binary: 0s & 1s)
     Python, etc.)
```

### 4. Cache (L1, L2, L3)
- **Definition:** Small, ultra-fast memory built inside CPU.
- **Size:** Measured in MB (much smaller than RAM).
- **Speed:** Nanoseconds (10⁻⁹ sec).
- **Levels:**  
  - L1 (fastest, smallest)  
  - L2  
  - L3 (largest, slowest among caches)
- **Purpose:** Store frequently accessed RAM data to reduce average access time.
- **Access strategy:** CPU checks cache first → then RAM if not found.

---

### 5. Motherboard
- Connects all components (CPU, RAM, disk, cache).
- Provides the **buses/paths** for data flow between components.

---

## Key Performance Insights
- **Disk:** Largest, slowest (ms). Persistent.
- **RAM:** Smaller, faster (µs). Volatile.
- **Cache:** Tiny, fastest (ns). Volatile.
- **CPU:** Executes instructions, orchestrates reads/writes.

---

## 🎯 Key Takeaways

### Why This Matters for System Design
- A single machine has **hardware limits** (disk size, RAM size, CPU speed).  
- Distributed systems combine multiple machines to overcome these limits.  
- Many **parallels** exist between computer architecture and distributed system design (e.g., cache ↔ distributed caching, disk ↔ database, CPU ↔ compute nodes).
