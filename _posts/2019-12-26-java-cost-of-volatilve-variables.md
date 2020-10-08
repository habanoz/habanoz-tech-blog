---
title: "Java: Cost of volatile variables"
categories:
  - Java
tags:
  - volatile variables
  - java
  - java memory model
  - atomic variables
  - locks
---

## Introduction

Use of volatile variables is common among Java developers as a way of implicit synchronization. JIT compilers may reorder program execution to increase performance. Java memory model[1] constraints reordering of volatile variables. Thus volatile variable access should has a cost which is different than a non-volatile variable access.

This article will not discuss technical details on use of volatile variables. Performance impact of volatile variables is explored by using a test application.

## Objective

Exploring volatile variable costs and comparing with alternative approaches.

## Audience

This article is written for developers who seek to have a view about cost of volatile variables.

## Test Configuration

Test application runs read and write actions on java variables. A non volatile primitive integer, a volatile primitive integer and an AtomicInteger is tested. Non-volatile primitive integer access is controlled with ReentrantLock and ReentrantReadWriteLock  to compare with explicit locking schemes.

A single test result is produced by doing 1 million read or write operations. Read and Write operations are conducted simultaneously. In some tests writing is excluded. In some tests 2 threads are used to read simultaneously.

For reliable results, each test is repeated 100 times for each variable type. Tests are run in the following order:

* Non-volatile Primitive Integer (Shared read/write)
* Non-volatile Primitive Integer with Reentrant Lock (Synch Read/Write)
* Non-volatile Primitive Integer with Reentrant ReadWrite Lock (RW Synch Read/Write)
* Volatile primitive integer (Volatile read/write)
* AtomicInteger (Atomic read/write)

During test JIT compiler my compile some code sections. Later executions may benefit from optimizations. To eliminate any JIT compiler affect, tests are repeated 5 times in the same order.

At the and for each variable type 500 test results are generated.

## Results

Average duration values are shown in y-axis. All values are in milliseconds. 

Please note that 500 test results are used for each variable and in each test a single thread made 1 million read or write operations. Results should be interpreted by considering thread counts and variable counts.{: .notice--warning}

### No writer, single reader

![No writer, single reader](https://1.bp.blogspot.com/-omjyDWEiNr4/XgR-Q3_Fu2I/AAAAAAAAD4k/5dARONSz6cs1g-qVHocycCADUj_BJ8xqwCLcBGAsYHQ/s1600/single_reader.png)

### No writer, 2 readers

![No writer, 2 readers](https://1.bp.blogspot.com/-WJuQ53IQHTk/XgR-vJ6tfqI/AAAAAAAAD4s/vuFlmYJDLHow6jCMfGdFoXIGrsD7uUzUACLcBGAsYHQ/s1600/2reader.png)

### 1 Writer, 1 Readers

![1 Writer, 1 Readers](https://1.bp.blogspot.com/-TuOFKDMVtuU/XgSLO5MHnxI/AAAAAAAAD5Y/H-8uwuLMnbEEJYdyK63dK7xTZdweb8W9wCLcBGAsYHQ/s1600/1reader1writer.png)

### 1 Writer, 2 Readers

![1 Writer, 2 Readers](https://1.bp.blogspot.com/-g9yEHpFfmPw/XgR_b1R4wTI/AAAAAAAAD44/X5WKzoyCWJATeJ_AcC9_3YkPmjkKkYqSQCLcBGAsYHQ/s640/2reader1writer.png)

### 1 Reader, 2 Variables

![1 Reader, 2 Variables](https://1.bp.blogspot.com/-FpRk3wFkbYI/XgR_lvBoxYI/AAAAAAAAD48/62dYspqlahg3mYW7IrF2RwjXV8rjsXQQgCLcBGAsYHQ/s1600/single_reader_2_reads.png)


## Interpreting Results

Test 1 uses 1 thread to make read operations. No concurrent write is done. Access to volatile and non volatile variables have similar costs. Using locks to constraint access is very costly.

Test 2 uses 2 threads to make concurrent reads. Results are not averaged by thread count. If we consider thread count, and divide results by 2, non volatile variable access is similar to  Test 1, which is expected.

However, volatile and atomic variables have somewhat increased costs. Reentrant Lock cost increases, which is not surprising.

ReentrantReadWrite Lock cost  increases much more than Reentrant Lock which is not expected. Expected results were close to the results of Test 1. Cost of ReentrantReadWrite Lock in all tests is not understandable. Curies readers my inspect test application code [2].

Test 3 uses 1 reader and 1 writer to inspect affect of changes. Non volatile variable access cost is similar to Test 2. Writing cost is slightly more costly compared to reading cost.Volatile reads still similar to non-volatile reads. Volatile writes however, now more than 2 times costlier than non-volatile writes. Atomic variables read cost is similar to volatile read costs. Atomic write cost is similar to volatile write cost.

If read and write costs are summed, Reentrant lock cost is found to be similar to test 2 costs. ReentrantReadWrite Lock costs are again high and not reasonable.

Test 4 adds one more reader to Test 3. Since there are two readers, divide results by 2 while interpreting. Non volatile and atomic operations are similar to results of Test 3.

Test 5 is the same setup with Test 1. Only difference is instead of 1 variable, 2 variables are used. This test aims to see if using two memory barrier is more costly than using single memory barrier through use of Locks. According to results, using locks is still more costly.

## Conclusion

Volatile variables and Atomic variables are cheap ways of implicit synchronization.

Use of locks should be avoided when possible.

## References

1. [Java Memory Model](https://docs.oracle.com/javase/specs/jls/se8/html/jls-17.html#jls-17.4)
2. [Test Application Source Code](https://github.com/habanoz/java-volatile-test)




