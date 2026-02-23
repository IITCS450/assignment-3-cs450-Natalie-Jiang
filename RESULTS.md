#Setup
There were 3 processes using the lotter_ratio program. This executes the testlottery in each process. The processes were assigned 100, 50, and 1 tickets respectively.

#Workload
Each process ran a CPU-heavy loop with 30,000,000 iterations. There were no waiting or I/O so all processes were competing for CPU time. This allows us to observe how the scheduler distributes CPU among the processes.

#Observed Results
##Run 1
|PID | Tickets | Ticks |
|--------------|-------|
|5   |100      |13     |
|6   |50       |13     |
|7   |1        |14     |
Total Time = 30 ticks

##Run 2
|PID | Tickets | Ticks |
|--------------|-------|
|10  |50       |13     |
|9   |100      |13     |
|11  |1        |14     |
Total Time = 93 ticks

##Run 3
|PID | Tickets | Ticks |
|--------------|-------|
|13  |100      |13     |
|14  |50       |14     |
|15  |1        |24     |
Total Time = 73 ticks

##Run 4
|PID | Tickets | Ticks |
|--------------|-------|
|17  |100      |13     |
|18  |50       |13     |
|19  |1        |17     |
Total Time = 49 ticks

Processes with more tickets generally finished sooner. While processes with fewer tickets took a bit longer. The order could vary because the lottery scheduler makes random choices each tick.

##Notes
The lottery scheduler is random. This means that a short run can show some variation. For example, the 1 ticket process could finish as quickly as a higher ticket process. However, in longer runs, the random differences average out. The CPU time becomes more proportional to the number of tickets. The scheduler gives more CPU to processes with higher ticket count.