# Inter-Process Communication : Shared Memory and Message Passing
=================================================

Course: Operating Systems (NCKU CSIE 2025)
Topic: Inter-Process Communication (IPC)
Due Date: 2025-10-17 (before Lab 1 course finishes)
Environment: Ubuntu 24.04 LTS on VirtualBox

------------------------------------------------------------

## 1. Overview
------------
<img width="884" height="454" alt="image" src="https://github.com/user-attachments/assets/0b918db7-9833-480e-acfa-a927c6d96cb1" />

This project implements inter-process communication between a sender and a receiver process in the C language.
Two different communication mechanisms are used and compared:

1. Message Passing (System V Message Queue)
2. Shared Memory (System V Shared Memory)

The purpose of this lab is to understand the principles of IPC and synchronization, implement both mechanisms,
and compare their performance in terms of communication speed.

------------------------------------------------------------

## 2. Implementation Summary
--------------------------
<img width="822" height="481" alt="image" src="https://github.com/user-attachments/assets/2fd45d44-ae2f-4457-b22b-b1c17a9d6cb4" />

Each mechanism uses a common mailbox structure provided by the TA.
The mailbox includes a flag and storage space that define the communication method.

Files in the repository:
- sender.c / sender.h: Implements send(message, &mailbox) and main()
- receiver.c / receiver.h: Implements receive(&message, &mailbox) and main()
- message.txt: Input file containing messages (1–1024 bytes per line, no blank lines)
- Makefile: Builds the executables
- mailbox: Structure used for both mechanisms

------------------------------------------------------------

## 3. Build Instructions
----------------------
To compile all files, run:
    make

The Makefile should generate two executables:
    sender
    receiver

------------------------------------------------------------

## 4. How to Run
--------------
Mechanism argument:
  1 = Message Passing
  2 = Shared Memory

Open two terminal windows.

In Terminal A (receiver):
    ./receiver 1
or
    ./receiver 2

In Terminal B (sender):
    ./sender 1 message.txt
or
    ./sender 2 message.txt

The sender reads each line from message.txt and sends it to the receiver.
When the sender reaches EOF, it sends an exit message.
The receiver terminates after receiving the exit message.

<img width="737" height="612" alt="image" src="https://github.com/user-attachments/assets/2d7e5820-0837-4241-a47a-e19ca9231dda" />



------------------------------------------------------------

## 5. Time Measurement
--------------------
Only measure the time spent directly on communication.

Include:
- msgsnd / msgrcv operations
- Shared memory access

Exclude:
- Waiting or blocking time
- Printing or I/O time

At the end of execution, both sender and receiver should print their total communication time.

Expected result: Shared Memory should be faster than Message Passing.

------------------------------------------------------------

## 6. System V API Reference
--------------------------
Message Queue:
    msgget, msgsnd, msgrcv, msgctl
Shared Memory:
    shmget, shmat, shmdt, shmctl
Semaphore (optional):
    semget, semop, semctl

------------------------------------------------------------

## 7. Learning Objectives
-----------------------
- Understand how processes communicate in Unix-like systems
- Learn how kernel IPC resources are created, used, and destroyed
- Implement process synchronization using semaphores
- Compare performance between copy-based and shared-memory communication

------------------------------------------------------------

## 8. Development Environment
---------------------------
Operating System: Ubuntu 24.04 LTS (VirtualBox)
Compiler: gcc 13 or later
Tools: make, gdb, vim, git

------------------------------------------------------------

## 9. Setup Steps
----------------
1. Clone the repository:
       git clone [https://github.com/pukyle/os_2025_lab1.git](https://github.com/pukyle/os_2025_lab1)
       cd os_2025_lab1

2. Build the project:
       make

3. Run sender and receiver as described above.

4. Modify and test your implementation.

------------------------------------------------------------

## 10. References
---------------
- Operating System Concepts by Silberschatz, Galvin, and Gagne
- Linux Manual Pages: man 7 ipc, man msgget, man shmget
- NCKU OS 2025 Lab 1 slides (TAs: 鄭宇辰, 張庭瑋, 黃柏盛)

------------------------------------------------------------




