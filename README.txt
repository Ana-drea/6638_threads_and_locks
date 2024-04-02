README --Multithreaded Hash Table


This program implements a multithreaded hash table with a fixed number of buckets and keys. It demonstrates concurrency in handling insertions and lookups in a hash table structure using pthreads. It ensures concurrency safety by utilizing `pthread_mutex_lock` and `pthread_mutex_unlock` to protect key insertion, while also maintaining efficienty by applying one mutex lock per bucket.


Features Implemented:
An array of mutex locks is declared (locks[NBUCKET]) to handle concurrency during insertions into the hash table. Each bucket is protected by its corresponding mutex lock.


Execution:
When a thread attempts to insert a key-value pair into the hash table using the put() function, it first acquires the mutex lock corresponding to the bucket where the key should be inserted. This prevents other threads from simultaneously modifying the same bucket, ensuring concurrency safety. After insertion, the mutex lock is released using pthread_mutex_unlock(), allowing other threads to access the bucket.	


Testing Process:
Run the program with different number of threads(see How to Use below), check the result with number of missing keys, if 0 missing keys, the program is concurrency safe. Also, the completion time should match the total runtime(put time + get time) for each thread, which means the program has perfect parallelism.


How to Use：
Compilation: put Makefile under same directory, compile with command "make"
Running the program: Execute the compiled binary with following commands to run with 1,2 and 4 threads.
make run1
make run2
make run4
To test the program with threads more than 4, run with command "./a2.out [number of threads]", note that number must be divisor of 100000


Error:
If you run the program with no number of threads given, or with number of threads being any number other than 1, 2, or 4(e.g.: run will "make run", "make run 3" or "make run8"), the program with break with error message: "make: *** No rule to make target 'run3'.  Stop."
If you run the program with number of threads that's not divisor of 100000, e.g.: run with command "./a2.out 15", the program will break with error message: "main: Assertion `NKEYS % nthread == 0' failed. Aborted"
