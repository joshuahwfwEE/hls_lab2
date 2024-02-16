# hls_lab2
datafow and deadlock  

   
1. foo:  
   this module implement an adder and a multplier and a latch in this circuit,
   adder takes l2 and Latch's output as its inputs and then multiplier takes adder's output and l1 as its inputs

   given an example design of testing the combination logic of above 2 module:    
    ![alt text](https://github.com/joshuahwfwEE/HLS_ATP/blob/main/design1_pattern_plus_foo.png?raw=true)    

5. double foo:  
   this module implement use 2 foo module,  
   double foo: implement 2 adder and 2 multiplier and 2 latch (task interval is lower but using larger amount resource)  
   foo reuse: implement 1 adder and 1 multiplier and 1 latch (task interval is higher but using smaller amount resource)  

6. fir filter:
   this module implement a filter that is common used in filter low-pass, high-pass, bandpass ...etc
   if we use gcc comiler such as mb-gcc compiler to compile this code and run in microblaze,
   the assmblely code:
   we can analysis the latency its takes although its have been already optimized by the compiler, it stll need load and store operation because its von neumann architecture trasfer to hls:
