## Intro

## 1 Parallel Computing Hardware
### Sequential vs. parallel computing
Sequential
* simple straight forward
* not taking advantage of the parallel hardware
Parrallel
* Higher throughput: 
    - same task faster
    - or more tasks in same time
* need extra effort for coordination

### Parallel computing architectures

One of the most widely used systems for classifying multiprocessor architectures is Flynn's taxonomy,

#### Flynn's taxonomy

Flynn's taxonomy distinguishes four classes of computer architecture based on two factors
* the number of concurrent instruction or control streams
* the number of data streams

The class names are usually written as four letter acronyms that indicate whether they have single or multiple instruction streams and data streams
* SIMD stands for Single Instruction, Multiple Data.
* The simplest of these four classes is the **Single Instruction, Single Data** or **SISD** architecture, which is __a sequential computer with a single processor unit__.
* The next class in Flynn's taxonomy is **Single Instruction, Multiple Data**, or **SIMD**, which is a type of parallel computer with multiple processing units. All of its processors execute the same instruction at any given time, but they can each operate on different data element. *As an SIMD computer, our two processors are both executing the same chopping instruction, but I'm chopping celery as my data while Baron chops a carrot. - And we'll execute those instructions in sync with each other. (chopping)* **This type of SIMD architecture is well-suited for applications that perform the same handful of operations on a massive set of data elements** like image processing. And most modern computers use graphic processing units or **GPUs** with SIMD instructions to do just that.
* **Multiple Instruction, Single Data** or **MISD** architecture, each processing unit independently executes its own separate series of instructions. However, all of those processors are operating on the same single stream of data. **MISD doesn't make much practical sense, so it's not a commonly used architecture.**
* **Multiple Instruction, Multiple Data** or MIMD computer, every processing unit can be executing a different series of instructions, and at the same time, each of those processors can be operating on a different set of data. **MIMD is the most commonly used architecture in Flynn's taxonomy, and you'll find it in everything from multicore PCs to network clusters and supercomputers.** Now, that broad MIMD category is sometimes further subdivided into two parallel programming models, which also have four letter names. 
    - **Single Program, Multiple Data**, or SPMD
    - **Multiple Program, Multiple Data**, MPMD.

In the SPMD model, multiple processing units are executing a copy of the same single program simultaneously. However, they can each use different data. That might sound a lot like the SIMD architecture from earlier, but it's different because although each processor is executing the same program, they do not have to be executing the same instruction at the same time. The processors can run asynchronously and the program usually includes conditional logic that allows different tasks within the program to only execute specific parts of the overall program. If Olevia and I are both following the same recipe or program, I can execute part of it, while Olevia's processor handles a different task. **This SPMD model is the most common style of parallel programming** and when we show you programming examples later in this course, we'll structure the code as a single program and execute it on a multicore desktop computer, which is an MIMD architecture.

Multiple Data or MPMD model. In this scenario, processors can be executing different, independent programs at the same time while of course also be operating on different data. Typically in this model, one processing node will be selected as the host or manager, which runs one program that farms out data to the other nodes running a second program. Those other nodes do their work and return their results to the manager. MPMD is not as common as SPMD, but it can be useful for some applications that lend themselves to functional decomposition, which we'll cover later on.


### Shared vs. distributed memory
In addition to a parallel computer's architecture which can be categorized using Flynn's taxonomy, another aspect is Memory. It's important to understand
* how the memory is organized
* how the computer accesses data

* Computer memory usually operates at a much slower speed than processors do 
* when one processor is reading or writing to memory, that often prevents any other processors from accessing that same memory element


There are two main memory architectures that exist for parallel computing, **shared memory** and **distributed memory**. 

#### Shared
In a shared memory system, all processors have access to the same memory as part of a global address space. Although each processor operates independently, if one processor changes a memory location, all of the other processors will see that change. 

the term shared memory doesn't necessarily mean all of this data exists on the same physical device. It could be spread across a cluster of systems. The key is that both of our processors see everything that happens in the shared memory space. 

Shared memory is often classified into one of two categories
* uniform memory access
* nonuniform memory access, 
which are based on how the processors are connected to memory and how quickly they can access it. 
##### UMA
In a uniform memory access or **UMA** system, all of the processors have equal access to the memory, meaning they can access it equally fast. There are several types of UMA architectures, but the most common is a **symmetric multiprocessing system** or **SMP**. An SMP system has two or more identical processors which are connected to a single shared memory often through a system bus. In the case of modern multicore processors, which you find in everything from desktop computers to cell phones, each of the processing cores are treated as a separate processor. *For this course, we'll be focused on parallel programming within the SMP architecture.* And the example code we show you will be running on a multicore desktop computer. 

Now, in most modern processors, each core has its own **cache**, which is a small, very fast piece of memory that only it can see, and it uses it to store data that it's frequently working with. However, caches introduce the challenge that if one processor copies a value from the shared main memory, and then makes a change to it in its local cache, then that change needs to be updated back in the shared memory before another processor reads the old value, which is no longer current. This issue, called **cache coherency**, is handled by the hardware in multicore processors, so **we will not go into detail on it for this course**, but it's something you should be aware of if you find yourself working with larger, more complex parallel computing systems.
##### NUMA
The other type of shared memory is a nonuniform memory access or NUMA system, which is **often made by physically connecting multiple SMP systems together**. The access is **nonuniform** because some processors will have quicker access to certain parts of memory than others. It takes longer to access things over the bus. But overall, every processor can still see everything in memory. 


##### Summary of shared memory
* advantage: easier for programming in regards to memory, because it's easier to share data between different parts of a parallel program. 
* The downside is that they don't always scale well. Adding more processors to a shared memory system will increase traffic on the shared memory bus, and if you factor in maintaining cache coherency, it becomes a lot of communication that needs to happen between all the parts.
* In addition to that, shared memory puts responsibility on the programmer to synchronize memory accesses to ensure correct behavior, but we'll look into that later.

#### distributed
In a distributed memory system, **each processor has its own local memory with its own address space**, so the concept of a global address space doesn't exist. All the processors are connected through some sort of network, which can be as simple as Ethernet. Each processor operates independently, and if it makes changes to its local memory, that change is **not automatically** reflected in the memory of other processors. 

Disadvantage: change not automatically reflected on other nodes, and the programmer to explicitly define how and when data is communicated between the nodes

The advantage of a distributed memory architecture is that it's **scalable**. When you add more processors to the system, you get more memory too. 

This structure makes it cost-effective to use commodity, off-the-shelf computers, and networking equipment to build large distributed memory systems. Most supercomputers use some form of distributed memory architecture or a hybrid of distributed and shared memory. - But for this course, we'll stick with simple shared memory in an SMP architecture.



## Threads and processes
### Thread vs. process
When a computer runs an application, that instance of the program executing is referred to as a process. 

#### A process 
* includes: code, data, and state information.
* independent instance of a running program
* separate address space in memory. 

An operating system's job is to manage hundreds of active processes at once. - 

#### Thread
Now, within every process, there are one or more smaller sub elements called **threads**. 
* independent path of execution; a different sequence of instructions
* it can only exist as part of a process
* OS schedule threads for execution: threads are the basic units that the operating system manages and it allocates time on the processor to actually execute them.

#### Data sharing
Threads that belong to the same process share the processes' address space, which gives them access to the same resources in memory including the program's executable code and data.


> You can think of the kitchen that our two threads are working in like the shared address space for our process. We both have direct access to the same cookbooks containing our instructions or code, and the ingredients that we're cooking with represents the data and variables we're manipulating. The ability for both of us to use these resources is certainly convenient, and it enables us to easily work together, but it does create the potential to cause problems if we don't coordinate our actions, as we'll see later in this course.

Sharing resources between separate processes is not as easy as sharing between threads in the same process, because every process exists in its own address space
> its own separate kitchen. In this process, our two threads are making a salad, but that other process next-door is running a different program. Those threads are baking a cake. - Our variables and data are isolated to this address space, this kitchen, so the threads in the other process can't directly access our salad data.

There are ways to communicate and share data between processes, but it requires a bit more work than communicating between threads. You have to use system-provided **inter-process communication(IPC) mechanisms** like 
* sockets and pipes
* allocating special inter-process **shared memory space**
* remote procedure calls
which is beyond the scope of what we'll be discussing in this course.

#### Processes or Threads

Which is better - it depends

**a rule of thumb, if you can structure your program to take advantage of multiple threads, stick with using threads rather than multiple processes.** 
* Threads are "lightweight" - requires less overhead to create and terminate than a process
* usually faster for an operating system to switch between executing threads from the same process than to switch between different processes.

### Thread vs Process: Java Demo
Exercise: 02_02

JVM
* each java application executes within its own instance of JVM
* Each JVM instance is a separate, independent process

JVM creates additional threads to handle stuff, gabage collection etc.

### Concurrent vs. parallel execution
Just because a program is structured to have multiple threads or processes does not mean they'll necessarily execute in parallel. 

Concurrency refers to the ability of a program to be broken into different parts that can run independently of each other, executed out of order or partially out of order without affecting the end result.

Concurrency is about how a program is structured and the composition of independently executing processes. 

> Consider this recipe to make a salad, which includes several steps that involve slicing and chopping vegetables. We can decompose those steps into a collection of concurrent tasks because the relative order in which we do them doesn't matter. They're order independent. To keep things simple, let's just focus on two of those tasks for now. I'll chop onions. - And I'll slice cucumbers. This knife represents our computer's processor. We only have one knife, so this is a single core processor. And only one of us will be able to execute our vegetable chopping routine at any given time. - We'll have to take turns. You go first. - Thanks. My thread will use a processor to execute and slice some cucumbers. Then, after a bit, we'll swap places. - Now my thread gets some time to execute and slice onions. - I want to slice now. - So we'll swap places again, and we'll keep on doing this until we're both done.

In this scenario, we're running concurrently because our two independent processes overlap in time. However, since we only have a single processor, only one of us will actually be executing at any instant in time. If we swap places and take turns more frequently, it might create the illusion that we're executing simultaneously on our single processor, but this is not true parallel execution.

**To actually execute in parallel, we need parallel hardware.** In our kitchen, that means another knife and cutting board, a second processor. 

In regards to computers, parallel hardware can come in a variety of forms.
* Most modern processors have multiple processing cores
* GPUs, contain hundreds, or even thousands, of specialized cores working in parallel to make amazing graphics that you see on the screen
* computer clusters distribute their processing across multiple systems.


> Since we've structured ourselves as concurrent operations, I can begin slicing cucumbers with this processor. - While I cut onions with the other one. Now we're **actually executing in parallel** because we're both **executing at the same time**. And, as a result, we're able to finish the job **faster**. 

#### Comparison
Concurrency:
* program structure
* being able to deal with multiple things at once(illusion at least)

Parallelism
* simultaneous execution
* actually doing multiple things at once. Those things could be related, like chopping vegetables, but they don't have to be.

Concurrency enables a program to execute in parallel, given the necessary hardware. But a concurrent program is not inherently parallel.

And programs may not always benefit from parallel execution
> For example, the software drivers that handle I/O devices, like a mouse, keyboard, and hard drive, need to execute concurrently. They're managed by the operating system as independent things that get executed, as needed. In a multi-core system, the execution of those drivers might get split amongst the available processors. However, **since I/O operations occur rather infrequently, relative to the speed at which computer operates, we don't really gain anything from parallel execution**. Those sparse independent tasks can run just fine on a single processor, and we wouldn't feel a difference. 

**Concurrent** programming is useful for **I/O-dependent tasks**
> like graphical user interfaces. When the user clicks a button to execute an operation, that might take a while. To avoid locking up the user interface until it's completed, we can run the operation in a separate concurrent thread. This leaves the thread that's running the UI free to accept new inputs.

That sort of I/O-dependent task is a good use case for concurrency. **Parallel** processing really becomes useful for **computationally intensive tasks**, such as Matrix multiplication.

### Execution scheduling
#### Scheduler
The OS includes a scheduler that controls when different threads and processes get their turn to execute on the CPU. The scheduler makes it possible for multiple programs to run concurrently on a single processor.

When a process is created and ready to run, it gets loaded into memory and placed in the ready queue. Think of these as cooks in the kitchen that are ready to work. 

The scheduler is like the head chef that tells the other cooks when they get to use the cutting board.It cycles through the ready processes so they get a chance to execute on the processor. If there are **multiple processors**, then the OS will schedule processes to run on each of them, to make the most use of the additional resources.
* A process will run until it finishes, and then the scheduler will assign another process to execute on that processor.
* Or, a process might get blocked and have to wait for an I/O event, in which case it will go into a separate **I/O waiting queue**, so another process can run.
* Or, the scheduler might determine that a process has spent its fair share of time on the processor, and swap it out for another process from the ready queue. When that occurs, it's called a **context switch**. 

#### Context switch

The operating system has to
* save the state, or context, of the process that was running, so it can be resumed later,
* load the context of the new process that's about to run.

> If I'm a process that's executing on this processor to chop cucumbers, when a scheduler decides it's time for a context switch, I'll need to pause what I'm doing and store the state of that task. - And as the new process that just got scheduled, I'll load my state information and then begin executing.

context switches are not instantaneous. It takes time to save and restore the registers and memory state, so the scheduler needs a strategy for how frequently it switches between processes. 

#### Scheduling algorithms:
* First come, first served
* shortest job next
* priority
* shortest remaining time
* round-robin
* multiple-level queues

Some of these algorithms are preemptive, which means they may pause, or preempt, a running, low-priority task when a higher priority task enters the ready state.
In non-preemptive algorithms, once a process enters the ready state, it'll be allowed to run for its allotted time.


Which algorithm a scheduler chooses to implement will depend on its goals. Some schedulers might try to maximize throughput, or the amount of work they complete in a given time

others might aim to minimize latency, to improve the system's responsiveness. 

Different operating systems have different purposes, and a desktop OS like Windows will have a different set of goals and use a different type of scheduler than a real-time OS for embedded systems. 

While it's important to understand the concept of scheduling, and that it's taking place, you usually don't need to worry about the nitty-gritty details of how the scheduler works, because it's often handled under the hood by the operating system. In fact, you might not have any control over when the parts of your program actually execute. - And that's an important thing to keep in mind. **Avoid running programs expecting that multiple threads or processes will execute in a certain order, or for an equal amount of time, because the operating system may choose to schedule them differently from run to run.**

### Execution scheduling: java demo 
02_05

To demo: You can see that each time we run this, we're getting a different result. So scheduling is not always consistent, so you shouldn't rely on it for threads to be executed in equal amount of time or in a particular order.

















































