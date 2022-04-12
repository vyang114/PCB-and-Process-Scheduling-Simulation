# PCB-and-Process-Scheduling-Simulation
An interactive operating system simulation that supports O/S functions using circular queue in C.


Design Decisions

User input:
1. Program only accepts uppercase commands.
2. Program assumes user only enter integers for priority and process PID.


Init_Process:
1. Always has a PID of 0.


Create:
1. When a first non-init-process is created, it checks if there is any process running. If there is no process running, it becomes the running process right away, otherwise it gets added to the respective priority ready queue to be ready to run.


Quantum, Exit:
1. When the running process has high priority: it checks if there is any process in the high priority ready queue. If there is, the first process in the queue becomes the next running process and the current running process is added to the end of it. If there is no other process readied in the high priority queue, the running process gets to keep running.

2. When the running process has normal priority: it checks if there is any process in the high priority ready queue first. If there is, the first process in the queue becomes the next running process and the current running process is added to the end of the normal priority ready queue. Then, it checks the normal queue. If there is a process readied, the first process in the queue becomes the next running process and the current running process is added to the end of it. If there is no other process readied in both the high priority and normal priority queues, the running process gets to keep running.

3. When the running process has low priority: it checks if there is any process in the high priority ready queue first. If there is, the first process in the queue becomes the next running process. If there is no high priority process, it checks if there is any normal priority process. If there is, the first process in the normal queue becomes the next running process. If there is none, it checks the low queue. If there is a process readied, the first process in the queue becomes the next running process. If there is no other process readied in all the queues, the running process gets to keep running.


Messages:
1. Messages refer to messages created by a Send() operation.
2. All the message instances have a PID of the process that the message is being sent to, a "from" field that stores the PID of the process that sent the message, and a "msg" field that stores the message.
3. All the message instances are added to a "Message List" every time they are created.
4. A message will only be received and displayed when its receiving process does a Receive(), and the message be removed from the list.
5. If a process is killed or exited and it still has a message on the list that has not been received, the message will also be removed from the list.


Replies:
1. Replies refer to messages created by a Reply() operation.
2. All the reply instances have a PID of the process that the reply is being sent to, a "from" field that stores the PID of the process that sent the reply, and a "msg" field that stores the reply.
3. All the reply instances are added to a "Reply List" every time they are created.
4. Replies can only be sent to processes that have done a Send().
5. Replies will be automatically received and displayed when its receiving process becomes the running process, and the reply will be removed from the list.
6. If a process is killed or exited and it still has a reply on the list that has not been received, the reply will also be removed from the list.


Total_Info:
1. Displays all the queues and lists in the system and the PIDs of the processes that each contains.








