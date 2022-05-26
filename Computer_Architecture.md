##  Explain pipeline concept in detail.
- Pipeline is an implementation technique that exploits parallelism among the instructions in a sequential instruction stream. Pipeline allows overlapping the execution of multiple instructions. A Pipeline is like an assembly line each step or pipeline stage completes a part of an instruction Each stage of the pipeline will be operating a separate instruction. Instructions enter at one end, progress through the stage and exit at the other end. If the stages are perfectly balanced (assuming ideal conditions), then the time per instruction on pipeline processor is given by the ratio:
    ### Time per instruction on unpipelined machine : Number of Pipeline stages
    Under these conditions, the speedup from pipelining is equal to the number of stage pipelines. In practice, the pipeline stages are not perfectly balanced and pipeline does involve some overhead. Therefore, the speedup will be always then practically less than the number of stages of the pipeline. Pipeline yields a reduction in the average execution time per instruction. If the processor is assumed to take one (long) clock cycle per instruction, then pipelining decreases the clock cycle time. If the processor is assumed to take multiple CPI, then pipelining will aid to reduce the CPI.

### - In Memory-to-Memory vector processor the operands for instruction, the intermediate result and the final result all these are retrieved from the main memory. TI-ASC, CDC STAR-100, and Cyber-205 use memory-to-memory format for vector instructions.

### - In Register-to-Register vector processor the source operands for instruction, the  intermediate result, and the final result all are retrieved from vector or scalar registers. Cray-1 and Fujitsu VP-200 use register-to-register format for vector instructions.

### - The vector length also affects the efficiency of processing as the longer vector length  would cause overhead of subdividing the long vector for processing.

### For obtaining the better performance the optimized object code must be produced in order to utilize pipeline resources to its maximum.
1. Improving the vector instruction: We can improve the vector instruction by reducing the memory access, and maximize resource utilization.
2. Integrate the scalar instruction: The scalar instruction of the same type must be integrated as a batch. As it will reduce the overhead of reconfiguring the pipeline again and again.
3. Algorithm: Choose the algorithm that would work faster for vector pipelined processing.
4. Vectorizing Compiler: A vectorizing compiler must regenerate the parallelism by using the higher-level programming language. In advance programming, the four-stage are identified in the development of the parallelism. Those are
    - Parallel Algorithm (A)
    - High-level Language (L)
    - Efficient object code (O)
    - Target machine code (M)
- We can see a parameter in the parenthesis at each stage which denotes the degree of parallelism. In the ideal situation, the parameters are expected in the order A ≥ L ≥ O ≥ M .

## Write about basic pipelining hazards and various pipelining hazards.
- Pipelining increases the CPU instruction throughput but, it does not reduce the execution time of an individual instruction.
- Pipelining increases the execution time of each instruction due to overhead in the control of the pipeline.
- Pipeline overhead arises from the combination of register delays and clock skew. Imbalance among the pipe stages reduces the performance since the clock can run no faster than the time needed for the slowest pipeline stage.
- A stall causes the pipeline performance to degrade from ideal performance. Performance improvement from pipelining is obtained from :
    ### Speedup = Pipeline depth  : ( 1 + Pipeline stall cycles per instruction )
- There are 3 types of hazards
    - Structural hazard
    - Data Hazard
    - Control Hazard
- **Structural hazard**
    - Structural hazard arise from resource conflicts, when the hardware cannot support all possible combination of instructions simultaneously in overlapped execution. If some combination of instructions cannot be accommodated because of resource conflicts, the processor is said to have structural hazard. Structural hazard will arise when some functional unit is not fully pipelined or when some resource has not been duplicated enough to allow all combination of instructions in the pipeline to execute.
    - For example, if memory is shared for data and instruction as a result, when an instruction contains data memory reference, it will conflict with the instruction reference for a later instruction. This will cause hazard and pipeline stalls for 1 clock cycle.

### Pipeline stall is commonly called Pipeline bubble or just simply bubble
- **Data Hazard**
    - Consider the pipelined execution of the following instruction sequence.
        - DADD      R1, R2, R3
        - DSUB      R4, R1, R5
        - AND       R6, R1, R5
        - OR        R8, R1, R9
        - XOR       R10,R1, R11
    DADD instruction produces the value of R1 in WB stage (Clock cycle 5) but the DSUB instruction reads the value during its ID stage (clock cycle 3). This problem is called Data Hazard. DSUB may read the wrong value if precautions are not taken. AND instruction will read the register during clock cycle 4 and will receive the wrong results. The XOR instruction operates properly, because its register read occurs in clock cycle 6 after DADD writes in clock cycle 5. The OR instruction also operates without incurring a hazard because the register file reads are performed in the second half of the cycle whereas the writes are performed in the first half of the cycle.
    - **Minimizing data hazard by Forwarding**: Forwarding works as follows:
        1. The output of ALU from EX/MEM and MEM/WB pipeline register is always feedback to the ALU inputs.
        2. If the Forwarding hardware detects that the previous ALU output serves as the source for the current ALU operations, control logic selects the forwarded result as the input rather than the value read from the register file.
- **Control Hazard**
    - Control Hazard occur when the decision of what instruction to fetch has not been made by the time the next instruction is fetched.  For example : When a branch is executed, it may or may not change the content of PC.
        - if a branch is taken, the content of PC is changed to target wrong address.
        - if a branch is taken, the content of PC is not changed.
    - **Can be solved by reducing branch penalties**
        1. Freeze or Flush the pipeline, holding or deleting any instructions after the branch until the branch destination is known. It is a simple scheme and branch penalty is fixed and cannot be reduced by software
        2. Treat every branch as not taken, simply allowing the hardware to continue as if the branch were not to executed. Care must be taken not to change the processor state until the branch outcome is known.

## Arithmatic Pipeline
- An arithmetic pipeline divides an arithmetic problem into various sub problems for execution in various pipeline segments. It is used for floating point operations, multiplication and various other computations. The process or flowchart arithmetic pipeline for floating point addition is shown in the diagram.
    <pre font-family="Cascadia Code">
            <u>Exponents</u>                        <u>Mantissas</u>
                x   y                           x   y
                |   |                           |   |
            +-----------+                   +-----------+
            |     R     |                   |     R     |
            +-----------+                   +-----------+
                  |                               |
    Segment +-------------------+                 |
        1:  | Compare exponents |   Difference    |
            |  by subtraction   |-----+           |
            +-------------------+     |           |
                  |                   |           |
            +-----------+             |           |
            |     R     |             |           |
            +-----------+             |           |
                  |                   |           |
    Segment +-------------------+     |   +----------------+
        2:  | Chooose exponent  |     +-->| Align Mantissa |
            +-------------------+         +----------------+
                  |                               |
                  |                         +-----------+
                  |                         |     R     |
                  |                         +-----------+
                  |                               |
                  |                       +----------------+
    Segment       |                       | Add / Subtract |
        3:        |                       |   mantissas    |
                  |                       +----------------+
                  |                               |
            +-----------+                   +-----------+
            |     R     |                   |     R     |
            +-----------+                   +-----------+
                  |                               |
    Segment +-------------------+        +------------------+
        4:  |  Adjust exponent  |        | Normalise result |
            +-------------------+        +------------------+
                  |                               |
            +-----------+                   +-----------+
            |     R     |                   |     R     |
            +-----------+                   +-----------+
                  |                               |
    </pre>
    Floating point addition using arithmetic pipeline :<br>
    The following sub operations are performed in this case:
    1. Compare the exponents.
    2. Align the mantissas.
    3. Add or subtract the mantissas.
    4. Normalise the result

    First of all the two exponents are compared and the larger of two exponents is chosen as the result exponent. The difference in the exponents then decides how many times we must shift the smaller exponent to the right. Then after shifting of exponent, both the mantissas get aligned. Finally the addition of both numbers take place followed by normalisation of the result in the last segment.<br>
    **Example:**<br>
    Let us consider two numbers,
        <pre font-family="Cascadia Code">
        X=0.3214*10^3 and Y=0.4500*10^2 </pre>
    **Explanation:**<br>
    First of all the two exponents are subtracted to give 3-2=1. Thus 3 becomes the exponent of result and the smaller exponent is shifted 1 times to the right to give
        <pre font-family="Cascadia Code">
        Y=0.0450*10^3 </pre>
    Finally the two numbers are added to produce
        <pre font-family="Cascadia Code">
        Z=0.3664*10^3 </pre>
    As the result is already normalized the result remains the same.

## What makes pipelining hard to implements?
- Overlapping of instructions makes it more difficult to know whether an instruction can safely change the state of the CPU. In a pipelined CPU, an instruction execution extends over several clock cycles. When this instruction is in execution, the other instruction may raise exception that may force the CPU to abort the instruction in the pipeline before they complete.<br>
    Types of exceptions:<br>
    The term exception is used to cover the terms interrupt, fault and exception. I/O device request, page fault, Invoking an OS service from a user program, Integer arithmetic overflow, memory protection overflow, Hardware malfunctions, Power failure etc. are the different classes of exception. Individual events have important characteristics that determine what action is needed corresponding to that exception.
    1. **Synchronous versus Asynchronous:**
        If the event occurs at the same place every time the program is executed with the same data and memory allocation, the event is asynchronous. Asynchronous events are caused by devices external to the CPU and memory such events are handled after the completion of the current instruction.
    2. **User requested versus coerced:**
        User requested exceptions are predictable and can always be handled after the current instruction has completed. Coerced exceptions are caused by some hardware event that is not under the control of the user program. Coerced exceptions are harder to implement because they are not predictable
    3. **User maskable versus user non maskable:**
        If an event can be masked by a user task, it is user maskable. Otherwise it is user non maskable.
    4. **Within versus between instructions:**
        Exception that occur within instruction are usually synchronous, since the instruction triggers the exception. It is harder to implement exceptions that occur within instructions than those between instructions, since the instruction must be stopped and restarted. Asynchronous exceptions that occurs within instructions arise from catastrophic situations and always causes program termination.
    5. **Resume versus terminate:**
        If the program’s execution continues after the interrupt, it is a resuming event otherwise if is terminating event. It is easier implement exceptions that terminate execution.

## Write a short note on restartable exception.
- Stopping and restarting execution: The most difficult exception have 2 properties:
    1. Exception that occur within instructions
    2. They must be restartable
- For example, a page fault must be restartable and requires the intervention of OS. Thus, pipeline must be safely shutdown, so that the instruction can be restarted in the correct state. If the restarted instruction is not a branch, then we will continue to fetch the sequential successors and begin their execution in the normal fashion.
- Restarting is usually implemented by saving the PC of the instruction at which to restart. Pipeline control can take the following steps to save the pipeline state safely.
    1. Force a trap instruction in to the pipeline on the next IF
    2. Until the trap is taken, turn off all writes for the faulting instruction and for all instructions that follow in pipeline. This prevents any state changes for instructions that will not be completed before the exception is handled.
    3. After the exception – handling routine receives control, it immediately saves the PC of the faulting instruction. This value will be used to return from the exception later.
