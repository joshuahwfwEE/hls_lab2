# hls_labA
dataflow and deadlock with data dependency issue
   
1. foo:  
   this simple module implement an adder and a multplier and a latch in this circuit,
   adder takes l2 and Latch's output as its inputs and then multiplier takes adder's output and l1 as its inputs  
    


2. double foo:  
   this module implement use 2 foo module,  
   double foo: implement 2 adder and 2 multiplier and 2 latch (task interval is lower but using larger amount resource)  
   foo reuse: implement 1 adder and 1 multiplier and 1 latch (task interval is higher but using smaller amount resource)  

3. fir filter:
   this module implement a filter that is common used in filter low-pass, high-pass, bandpass ...etc
   if we use gcc comiler such as mb-gcc compiler to compile this code and run in microblaze,
   the assmblely code:
   we can analysis the latency its takes although its have been already optimized by the compiler, it stll need load and store operation because its von neumann architecture trasfer to hls:  
   
4. dataflow test  



5. deadlock test:
   
//////////////////////////////////////////////////////////////////////////////  
// ERROR!!! DEADLOCK DETECTED at 10210000 ns! SIMULATION WILL BE STOPPED!       
//////////////////////////////////////////////////////////////////////////////  
/////////////////////////  
// Dependence cycle 1:  
// (1): Process: example.proc_1_U0.proc_1_2_U0  
//      Blocked by empty input FIFO 'example.proc_1_U0.data_channel2_U' written by process 'example.proc_1_U0.proc_1_1_U0'  
// (2): Process: example.proc_1_U0.proc_1_1_U0  
//      Blocked by full output FIFO 'example.proc_1_U0.data_channel1_U' read by process 'example.proc_1_U0.proc_1_2_U0'  
////////////////////////////////////////////////////////////////////////  
// Totally 1 cycles detected!  
////////////////////////////////////////////////////////////////////////  
$finish called at time : 10260 ns : File "/home/joshua/work/HLSIP/ntu_boledulab/labA/Dataflow_Debug_and_Optimization/deadlock/example/solution1/sim/verilog/AESL_deadlock_report_unit.v" Line 667  

deadlocks reasons:  

Blocked Writer in Deadlocks:  
at least one writer (module or stage writing to a FIFO) is unable to make progress. This could happen when the writer is waiting for space in the FIFO to become available.  

Insufficient FIFO Depths:
especially when the rate of data production or consumption does not match the FIFO capacity. If a writer is frequently blocked due to a full FIFO, it can result in a deadlock situation.  

Design Issues with Non-Blocking Operations:  
Non-blocking reads or writes can sometimes cause unexpected behavior.   
If a writer doesn't check whether there is space available (not full()) before writing or a reader doesn't check if data is available (not empty()) before reading,   
it can lead to contention and potential deadlocks.

Conditions Based on empty() and full():    
The conditions based on the empty() and full() status of a FIFO are often used to check whether there is data to be read (not empty()) or space to write (not full()).     
Incorrectly handling these conditions can lead to situations where a writer or reader might be waiting indefinitely, contributing to deadlocks.    

