#include <stdio.h>
#include <unistd.h>  
#include <stdlib.h> 
#include <sys/wait.h> 

struct Process {
    int id;             
    int arrivalTime;    
    int burstTime;      
    int completionTime; 
    int turnaroundTime; 
    int waitingTime;    
};


void calculateTimes(struct Process processes[], int n) {
    int currentTime = 0;

    for (int i = 0; i < n; i++) {
        if (currentTime < processes[i].arrivalTime) {
            currentTime = processes[i].arrivalTime;
        }
        processes[i].completionTime = currentTime + processes[i].burstTime;
        currentTime = processes[i].completionTime;

        processes[i].turnaroundTime = processes[i].completionTime - processes[i].arrivalTime;
        processes[i].waitingTime = processes[i].turnaroundTime - processes[i].burstTime;
    }
}


void printTable(struct Process processes[], int n) {
    printf("Student#   Arrival   Duration   Completion   Turnaround   Waiting\n");
    printf("-----------------------------------------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("   S%d        %2d         %2d          %2d           %2d          %2d\n",
               processes[i].id,
               processes[i].arrivalTime,
               processes[i].burstTime,
               processes[i].completionTime,
               processes[i].turnaroundTime,
               processes[i].waitingTime);
    }
}


void calculateAverageTimes(struct Process processes[], int n) {
    float totalTAT = 0, totalWT = 0;

    for (int i = 0; i < n; i++) {
        totalTAT += processes[i].turnaroundTime;
        totalWT += processes[i].waitingTime;
    }

    printf("\nAverage Turnaround Time: %.2f\n", totalTAT / n);
    printf("Average Waiting Time: %.2f\n", totalWT / n);
}

int main() {
    int n;
    int roleChoice;

    
    printf("=========================================\n");
    printf("Welcome to the Student Interview Scheduler!\n");
    printf("This program simulates scheduling students for interviews\n");
    printf("and calculates relevant metrics such as waiting time,\n");
    printf("turnaround time, and completion time.\n");
    printf("=========================================\n\n");

   
    printf("Select your role:\n");
    printf("1. Student\n");
    printf("2. Interviewer\n");
    printf("Enter your choice: ");
    scanf("%d", &roleChoice);

    
    int pipefd[2];
    if (pipe(pipefd) == -1) {
        perror("Pipe failed");
        exit(1);
    }

    if (roleChoice == 1) {
        printf("You are a Student.\n");
        printf("Enter the number of students: ");
        scanf("%d", &n);

        struct Process processes[n];

        
        for (int i = 0; i < n; i++) {
            processes[i].id = i + 1;
            printf("Enter Arrival Time and Interview Duration for Student S%d: ", i + 1);
            scanf("%d %d", &processes[i].arrivalTime, &processes[i].burstTime);
        }

       
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (processes[j].arrivalTime > processes[j + 1].arrivalTime) {
                    struct Process temp = processes[j];
                    processes[j] = processes[j + 1];
                    processes[j + 1] = temp;
                }
            }
        }

        
        pid_t pid = fork();

        if (pid < 0) {
            perror("Fork failed");
            exit(1);
        } else if (pid == 0) { 
            close(pipefd[0]); 
            calculateTimes(processes, n);
            write(pipefd[1], processes, sizeof(processes)); 
            close(pipefd[1]); 
            exit(0);
        } 
        else {
            wait(NULL); 
            close(pipefd[1]);
            read(pipefd[0], processes, sizeof(processes)); 
            close(pipefd[0]);

           
            printTable(processes, n);
            calculateAverageTimes(processes, n);
        }

    } else if (roleChoice == 2) {
        printf("You are an Interviewer.\n");
        printf("\nAs an Interviewer, you should be focused on reviewing and managing the interview schedules.\n");
        printf("You can assess the waiting times, turnaround times, and completion times for each student.\n");
        printf("\nPress '0' to exit: ");
        int exitChoice;
        scanf("%d", &exitChoice);
        if (exitChoice == 0) {
            printf("Program successfully executed.\n");
            exit(0);
        }
    } 
    else {
        printf("Invalid choice. Exiting...\n");
        exit(1);
        
    }

    return 0;
}
