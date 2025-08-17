# FCFS Job Scheduling Simulator

This project is a C program that simulates the First-Come, First-Served (FCFS) CPU scheduling algorithm. It models a simple job interview scheduling system for students and calculates key performance metrics to evaluate the efficiency of the algorithm.

The program demonstrates fundamental concepts of operating systems, process management, and inter-process communication (IPC).

## 🌟 Key Features

* **FCFS Simulation:** Schedules "students" (processes) for interviews based on their arrival time, adhering to the FCFS principle.
* **Performance Metrics:** Calculates and displays a detailed breakdown of:
    * **Completion Time:** The time at which each interview is completed.
    * **Turnaround Time:** The total time a student waits from arrival until the completion of their interview.
    * **Waiting Time:** The total time a student spends waiting for their interview to begin.
* **Average Times:** Computes and prints the average turnaround time and average waiting time for all students.
* **Inter-Process Communication (IPC):** Utilizes `fork()` and `pipe()` to create a child process for calculations and send the results back to the parent process for display, showcasing a practical application of IPC.
* **User-Friendly Interface:** Provides a simple command-line interface for users to input student data and select their role (Student or Interviewer).

## 🛠️ How to Compile and Run

### Prerequisites
* A C compiler (e.g., GCC)

### Compilation
1.  Save the code as a `.c` file (e.g., `fcfs_scheduler.c`).
2.  Open your terminal or command prompt.
3.  Navigate to the directory where you saved the file.
4.  Compile the program using GCC:
    ```bash
    gcc fcfs_scheduler.c -o fcfs_scheduler
    ```

### Execution
1.  Run the compiled executable:
    ```bash
    ./fcfs_scheduler
    ```
2.  Follow the on-screen prompts to enter the number of students and their arrival and interview duration times.

## 📂 Project Structure

* `fcfs_scheduler.c`: The core C source code for the FCFS simulation.

## 📄 Explanation of the Code

* **`struct Process`:** Defines a structure to hold information for each student/process, including `id`, `arrivalTime`, `burstTime`, `completionTime`, `turnaroundTime`, and `waitingTime`.
* **`calculateTimes()`:** This function is where the FCFS logic is implemented. It iterates through the processes and calculates the completion, turnaround, and waiting times for each.
* **`main()`:** The main function handles user interaction, sorts the processes by arrival time, and uses `fork()` and `pipe()` for process communication. The child process (`pid == 0`) performs the calculations, while the parent process (`pid > 0`) receives the results and displays the final output.

This project serves as an effective demonstration of process scheduling fundamentals and is a great asset for a technical portfolio.
