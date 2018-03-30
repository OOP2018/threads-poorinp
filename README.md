## Threads and Synchronization

This lab illustrates the problem of synchronization when many threads are operating on a shared object.  The general issue is called "thread safety", and it is a major cause of errors in computer software.

## Assignment

To the problems on the lab sheet and record your answers here.

1. Record average run times.
2. Write your explanation of the results.  Use good English and proper grammar.  Also use good Markdown formatting.

## ThreadCount run times

These are the average runtime using 3 or more runs of the application.
The Counter class is the object being shared by the threads.
The threads use the counter to add and subtract values.

| Counter class           | Limit              | Runtime (sec)   |
|:------------------------|:-------------------|-----------------|
| Unsynchronized counter  |10,000,000          |0.01623967       |
| Using ReentrantLock     |10,000,000          |0.93780167       |
| Syncronized method      |10,000,000          |0.38102467       |
| AtomicLong for total    |10,000,000          |0.253279         |

## 1. Using unsynchronized counter object

1.1) The result is not zero. It is not the same each time. 

1.2) Average running time is 0.01623967 seconds.

1.3) It is not the same because computer use multi-thread. The resources
to run the thread is the same, but one thread add the counter and the another thread subtract counter
by not care about what is the value is. 

## 2. Implications for Multi-threaded Applications

How might this affect real applications?

In Banking situation, using multi-thread will help people do more task at the same time.
People can withdraw, deposit and transfer at the same time. So, the process 
can achieve without waiting for another process to start and execute.


## 3. Counter with ReentrantLock

3.1) The result is always zero. Average running time is 0.93780167 seconds.

3.2) In problem 3 we lock the thread to run only one process, the
result will be zero then unlock to run another process.
But in problem 1 the process is running while another process is running, the result will not be zero.

3.3) ReentrantLock can lock thread to use only that thread and it will unlock after the process is finished.
We use in this program because we don't want many threads run at the same time, preventing the interrupt from
each thread.

3.4) It will process in try until the process finish then unlock to work in another process. 

## 4. Counter with synchronized method

4.1) Yes the total is zero. The average running time is 0.38102467.

4.2) In problem 1 the process is running while another process is running, the result will not be zero.
In problem 4, each counter's process will run in one thread until finished then run new process with
another thread.

4.3) A simple strategy for preventing thread interferences and memory consistency errors.
We use in this program because I want one thread to working on one task and waiting this task
finished then work on another task.

## 5. Counter with AtomicLong

5.1) Because it will update counter automatically. so it will use little time for threads can work together.

5.2) Because it will update counter automatically. so it will use little time for threads can work together.
An AtomicLong is used in applications such as atomically incremented sequence numbers.

## 6. Analysis of Results

6.1) AtomicLong is the fastest, and ReentrantLock is the slowest.

6.2) Synchronized method because it is more flexible than AtomicLong that use for incrementing sequence numbers
and faster than ReentrantLock.

## 7. Using Many Threads (optional)

