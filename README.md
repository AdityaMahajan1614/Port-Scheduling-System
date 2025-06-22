# Port Scheduler Simulation

This project is a C-based simulation of a port scheduling system. It manages the docking and undocking of ships, cargo handling with cranes, and communication between different system components using advanced operating system concepts like Inter-Process Communication (IPC) and multithreading.

The core logic is implemented in [`scheduler.c`](scheduler.c).

## Core Concepts Implemented

-   **Inter-Process Communication (IPC):**
    -   **Shared Memory:** Used for efficient data sharing between the main simulation process and the scheduler for new ship requests and discovered authorization strings.
    -   **Message Queues:** The primary mechanism for event-driven communication between the main process, scheduler, and solver processes.
-   **Concurrency and Parallelism:**
    -   **Multithreading (`pthreads`):** The scheduler uses multiple threads to parallelize the process of guessing the authorization string required for a ship to undock, significantly speeding up the process by distributing the workload among available solver processes.
-   **Scheduling Algorithms:**
    -   **Priority-Based Docking:** Emergency ships are prioritized over normal ships. Ships are further sorted by category to optimize dock usage.
    -   **Resource Management:** Efficiently allocates docks to incoming ships and cranes to cargo based on capacity and availability.

## How to Run

### Prerequisites

-   A Linux or Unix-like environment.
-   `gcc` compiler.
-   The provided `validation.out` executable.

### Directory Structure

Ensure your project is set up with the following structure. Your compiled `scheduler.out`, the provided `validation.out`, and the `testcase_X` folders must all be in the same parent directory.

```
.
├── scheduler.out
├── validation.out
├── testcase1/
│   └── input.txt
└── testcase2/
    └── input.txt
```

### Compilation

Compile your [`scheduler.c`](scheduler.c) file using `gcc`.
````sh
gcc scheduler.c -o scheduler.out
````

 Open Two Terminals 
   - Please note that the executable file for the validation process has been provided
    (validation.out). You may have to execute the command chmod 777 validation.out
    before running the file.
  - Run the validation program in one terminal with X as a command-line input, where X
    denotes the test case number. Use the command ./validation.out X, where X is the test
    case number.
  - Run your scheduler program in the second terminal. Use the command
    ./scheduler.out X, where X is the test case number.
