# Operating Systems: Temperature Data Analysis System

## 📖 Introduction
This report presents a C implementation for the processing and analysis of temperature sensor data from different regions. The solution is composed of three programs—`sort`, `stats`, and `report`—that interact using anonymous pipes and system calls to ensure high performance and efficiency. The project prioritizes memory efficiency, parallelism, and modularity.

---

## 🏗️ Process Architecture
The system uses a multi-process architecture to handle large volumes of data while staying within memory constraints.



### 1. `sort` Program
* **Objective**: Sorts temperature records for a specific region directly within the binary file.
* **Memory Efficiency**: Utilizes a buffer (`BUFFER_SIZE`) to process records in parts, ensuring the program respects limited memory restrictions.
* **Counting Sort**: Implements an efficient counting sort algorithm to order data without requiring extra alocations.
* **Direct I/O**: Sorted data is written directly to the binary file using `pwrite`, eliminating the need for temporary files.

### 2. `stats` Program
* **Objective**: Calculates statistical data for a region and outputs it to `stdout` or binary files.
* **Sort Invocation**: Uses `fork` and `execlp` to launch the `sort` program, ensuring data is ordered before calculations begin.
* **Calculations**: Identifies the Maximum, Minimum, Average (mean), and Median values for the region.
* **Process Management**: Uses `waitpid` to synchronize and wait for the sorting process to complete before proceeding with data analysis.

### 3. `report` Program
* **Objective**: Aggregates statistics from all regions and identifies the highlights (maximums and minimums) in each category.
* **Parallel Execution**: Launches multiple `stats` processes simultaneously to reduce total execution time, controlled by a maximum process limit.
* **Communication**: Employs anonymous pipes (`pipe`) to receive statistical results from each child `stats` process.
* **Final Report**: Generates a detailed summary of all regional data and identifies which regions stand out in the final dataset.

---

## 🚀 Key Features and Scalability
* **Process Control**: The `report` program features a mechanism to limit the number of simultaneous active processes, preventing system overload.
* **High Performance**: Testing demonstrated that the architecture efficiently supports up to 180 regions with 200,000 records each.
* **Modular Design**: The separation into three independent programs allows for easy maintenance and potential reuse of individual components in other projects.

---

## 👥 Authors
* **José Novais** - A105056
* **Miguel Machado** - A103668
* **Tiago Diogo** - A103665

---
*Developed for the Engineering in Telecommunications and Informatics course - University of Minho (December 2024)*
