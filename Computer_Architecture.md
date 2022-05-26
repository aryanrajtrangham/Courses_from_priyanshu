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
    - Parallel Algorithm(A)
    - High-level Language(L)
    - Efficient object code(O)
    - Target machine code (M)
- We can see a parameter in the parenthesis at each stage which denotes the degree of 
parallelism. In the ideal situation, the parameters are expected in the order A ≥ L ≥ O ≥ M .
