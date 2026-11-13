# commands-
# OPERATING SYSTEMS LAB – COMPLETE PRACTICAL EXECUTION GUIDE
## Ubuntu 24.04 | GCC Compiler | Practicals 1 to 8

## STEP 0: ONE-TIME SETUP

1. Open Ubuntu Terminal by pressing `Ctrl + Alt + T`.
2. Check whether GCC is installed:

```bash
gcc --version
```

3. If GCC is missing, install it:

```bash
sudo apt update
sudo apt install -y build-essential
```

4. Create the main OS Lab folder and all practical folders:

```bash
mkdir -p ~/OS_Lab
cd ~/OS_Lab
mkdir -p exp1 exp2 exp3 exp4 exp5 exp6 exp7 exp8
```

## HOW TO CREATE AND SAVE PROGRAM FILES

Follow these steps for every practical:

1. Open Ubuntu Applications.
2. Search for and open **Text Editor**.
3. Copy the required program code from the corresponding Practical in the PDF, under **Step 2 – Program Code**.
4. Paste the code into Text Editor.
5. Click **Save As**.
6. Open the correct practical folder inside `OS_Lab`.
7. Enter the exact filename mentioned below.
8. Click Save.
9. Open Terminal and execute the compilation and running commands.

IMPORTANT: Save each program in its respective folder. Do not save all programs in the same folder.

---

# PRACTICAL 1: SHELL PROGRAMMING – ADDRESS BOOK

### Step 1: Create the file

Folder: `~/OS_Lab/exp1`

Filename: `addressbook.sh`

Open Text Editor, paste the Practical 1 Address Book code from the PDF and save it as `addressbook.sh` inside `exp1`.

### Step 2: Execute the program

```bash
cd ~/OS_Lab/exp1
chmod +x addressbook.sh
./addressbook.sh
```

### Step 3: Sample input

Use the menu options in this order:

- Enter `1` – Create Address Book.
- Enter `3` – Insert a Record.
  - Name: `John`
  - Phone: `9876543210`
  - Email: `john@gmail.com`
- Enter `3` – Insert another Record.
  - Name: `Alice`
  - Phone: `9123456780`
  - Email: `alice@yahoo.com`
- Enter `2` – View Address Book.
- Enter `5` – Modify a Record and provide the requested name and updated details.
- Enter `4` – Delete a Record and provide the name.
- Enter `2` – View the updated records.
- Enter `6` – Exit.

To check the saved address book:

```bash
cat addressbook.txt
```

---

# PRACTICAL 2: PROCESS MANAGEMENT – FORK, ZOMBIE AND ORPHAN

### Step 1: Create three files

Folder: `~/OS_Lab/exp2`

Create these three files using Text Editor:

1. `fork_wait_sort.c`
2. `zombie.c`
3. `orphan.c`

Paste the corresponding Practical 2 program codes from the PDF into each file and save.

### A) FORK AND WAIT

Compile and execute:

```bash
cd ~/OS_Lab/exp2
gcc fork_wait_sort.c -o fws
./fws
```

Input:

```text
5
45 12 78 10 32
```

Expected sorted output:

```text
10 12 32 45 78
```

The child process performs Insertion Sort and the parent process performs Bubble Sort.

### B) ZOMBIE PROCESS

Open Terminal 1:

```bash
cd ~/OS_Lab/exp2
gcc zombie.c -o zombie
./zombie
```

Open Terminal 2 within approximately 20 seconds:

```bash
ps -eo pid,ppid,stat,comm | grep -E 'Z|zombie'
```

Check the `STAT` column. The letter `Z` indicates a zombie process.

### C) ORPHAN PROCESS

```bash
cd ~/OS_Lab/exp2
gcc orphan.c -o orphan
./orphan
```

Wait approximately 5 seconds for the output.

The program displays the parent process exiting, the child process running and its new parent PID.

---

# PRACTICAL 3: THREAD SYNCHRONIZATION – PRODUCER CONSUMER

### Step 1: Create the file

Folder: `~/OS_Lab/exp3`

Filename: `producer_consumer.c`

Open Text Editor, paste the Practical 3 code from the PDF and save it.

### Step 2: Compile and execute

```bash
cd ~/OS_Lab/exp3
gcc producer_consumer.c -o pc -pthread
./pc
```

### Step 3: Input and expected output

No input is required.

Wait approximately 20 seconds for execution to finish.

The producer generates these values:

```text
10
20
30
40
50
60
70
80
90
100
```

The consumer consumes the same values in order.

Note: The exact order of producer and consumer messages may vary because both run concurrently.

---

# PRACTICAL 4: DINING PHILOSOPHERS PROBLEM

### Step 1: Create the file

Folder: `~/OS_Lab/exp4`

Filename: `dining_philosophers.c`

Open Text Editor, paste the Practical 4 code from the PDF and save it.

### Step 2: Compile and execute

```bash
cd ~/OS_Lab/exp4
gcc dining_philosophers.c -o dp -pthread
./dp
```

### Step 3: Input and expected output

No input is required.

The program demonstrates synchronization between philosophers using threads and mutexes.

Expected final message:

```text
All philosophers finished - no deadlock.
```

### Optional: Run the unsafe version

```bash
gcc -DUNSAFE dining_philosophers.c -o dp_unsafe -pthread
./dp_unsafe
```

This demonstrates the possibility of deadlock. Stop the program using `Ctrl + C` if it gets stuck.

---

# PRACTICAL 5: DEADLOCK AVOIDANCE – BANKER'S ALGORITHM

### Step 1: Create the file

Folder: `~/OS_Lab/exp5`

Filename: `bankers.c`

Open Text Editor, paste the Practical 5 code from the PDF and save it.

### Step 2: Compile and execute

```bash
cd ~/OS_Lab/exp5
gcc bankers.c -o bankers
./bankers
```

### Step 3: Enter the following input in order

Number of processes:

```text
5
```

Number of resource types:

```text
3
```

Allocation Matrix (enter each row):

```text
0 1 0
2 0 0
3 0 2
2 1 1
0 0 2
```

Maximum Matrix (enter each row):

```text
7 5 3
3 2 2
9 0 2
2 2 2
4 3 3
```

Available Resources:

```text
3 3 2
```

### Step 4: Expected output

```text
System is in Safe State.

Safe Sequence: P1 -> P3 -> P4 -> P0 -> P2
```

---

# PRACTICAL 6: INTER-PROCESS COMMUNICATION USING FIFO (NAMED PIPES)

### Step 1: Create two files

Folder: `~/OS_Lab/exp6`

Create these files using Text Editor:

1. `process1.c`
2. `process2.c`

Paste the corresponding Practical 6 code from the PDF into each file and save.

### Step 2: Compile both programs

```bash
cd ~/OS_Lab/exp6
gcc process1.c -o p1
gcc process2.c -o p2
```

### Step 3: Execute using two Terminal windows

Open Terminal 1:

```bash
cd ~/OS_Lab/exp6
./p2
```

Open Terminal 2:

```bash
cd ~/OS_Lab/exp6
./p1
```

### Step 4: Enter input in Terminal 2

```text
Operating Systems laboratory experiment
```

After entering the sentence:

1. Press Enter.
2. Press Enter again on an empty line to finish input.

### Step 5: Expected output

```text
Output received from Process 2:

Number of Characters = 39
Number of Words = 4
Number of Lines = 1
```

### Step 6: Check generated files

```bash
ls -l fifo1 fifo2
cat result.txt
```

### Step 7: Cleanup after execution

```bash
rm -f fifo1 fifo2 result.txt
```

IMPORTANT: Both programs must run in the same `exp6` folder, using two separate Terminal windows.

---

# PRACTICAL 7: INTER-PROCESS COMMUNICATION USING UNNAMED PIPE

### Step 1: Create the file

Folder: `~/OS_Lab/exp7`

Filename: `pipe_file.c`

Open Text Editor, paste the Practical 7 code from the PDF and save it.

### Step 2: Compile the program

```bash
cd ~/OS_Lab/exp7
gcc pipe_file.c -o pf
```

### Step 3: Create a sample text file

```bash
printf "Operating System Laboratory\nIPC using Pipes\n" > sample.txt
```

### Step 4: Execute the program

```bash
./pf
```

### Step 5: Enter input

When the program asks for a filename, enter:

```text
sample.txt
```

Expected output:

```text
Contents of File:
Operating System Laboratory
IPC using Pipes
```

---

# PRACTICAL 8: DISK SCHEDULING ALGORITHMS – SSTF, SCAN AND C-LOOK

### Step 1: Create three files

Folder: `~/OS_Lab/exp8`

Create these files using Text Editor:

1. `sstf.c`
2. `scan.c`
3. `clook.c`

Paste the respective Practical 8 program codes from the PDF into each file and save.

### Step 2: Compile all three programs

```bash
cd ~/OS_Lab/exp8
gcc sstf.c -o sstf
gcc scan.c -o scan
gcc clook.c -o clook
```

### A) SSTF – Shortest Seek Time First

Execute:

```bash
./sstf
```

Input:

```text
8
98 183 37 122 14 124 65 67
53
```

Expected total seek time:

```text
Total Seek Time = 236
```

### B) SCAN – Elevator Algorithm

Execute:

```bash
./scan
```

Input:

```text
8
98 183 37 122 14 124 65 67
53
200
```

Expected total seek time:

```text
Total Seek Time = 331
```

### C) C-LOOK Algorithm

Execute:

```bash
./clook
```

Input:

```text
8
98 183 37 122 14 124 65 67
53
```

Expected total seek time:

```text
Total Seek Time = 322
```

---

# FINAL FILE CHECKLIST

| Practical | Files to save |
|---|---|
| 1 | addressbook.sh |
| 2 | fork_wait_sort.c, zombie.c, orphan.c |
| 3 | producer_consumer.c |
| 4 | dining_philosophers.c |
| 5 | bankers.c |
| 6 | process1.c, process2.c |
| 7 | pipe_file.c |
| 8 | sstf.c, scan.c, clook.c |

## IMPORTANT EXECUTION NOTES

1. Always open the correct practical folder before compiling.
2. Use the exact filenames mentioned in this guide.
3. Copy program source code from the corresponding Practical's Step 2 in the PDF.
4. For C programs using threads, compile with `-pthread`.
5. For Practical 6, always use two Terminal windows.
6. If a program gets stuck, press `Ctrl + C`.
7. For Practical 8, compile all three algorithms separately.
8. Do not close the Terminal while a program is executing.

**All eight practicals are organized according to the OS Lab Complete Practical Guide PDF.**
