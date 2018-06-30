# LRU-Algorithm-in-Postgresql
Files that were modified for the implementation of the new LRU Code:
1.	buf_init.c
2.	bufmgr.c
3.	localbuf.c
4.	freelist.c

I used comments started with    //U70331249   for all of the modification I made in those files.
Description Of the Algorithm/ Data structure Implementation:
•	We are using the files from the PostgreSQL Version: 8.2.19 and the OS type: Ubuntu 10.04
•	It uses Clock Sweep Page replacement technique. Whenever a page is referenced a bit is set by using this algorithm. This can be clock bit (or used/referenced bit) which is used to track how often a page is accessed. Clock Sweep algorithm sweeps the pages that has the usedbit=0. It replaces the pages that are not been referenced for one complete revolution of the clock.
•	In our code we use usage_count and ref_count, where usage_count is the referenced bit and ref_count defines as a pincount. Pincount returns the number of processes that works on that particular buffer.
•	Now in our project we have to change the implementation of the code to Least Recently Used scenario. This LRU Algorithm replaces the page that has not been referenced for the longest time. For this we uses queue of pointers that has a pincount 0. Here when ever the pincount becomes 0 for any frame, that frame will be added to the end of the queue. 
•	The LRU Algorithm implemented in our code uses refcount as pincount. And acts as pincount and adds these pages which has refcount=0 to the freelist. In the LRU Algorthm, the top page is replaced every time, where it is the least recently used page in the queue.


TESTING:

1. I had replaced the files that were modified and compile them.
2. For compilation we have to use sudo make clean and sudo make commands.
3. Then install using sudo make install
4. The following commands were used to run the postgresql

  /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
  /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data >log file 2>&1 &
  /usr/local/pgsql/bin/psql test
  
5. Then we have to go to /home/bhargavi/Downloads/input.sql repository and then stop the repository by using 
 /usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data stop
6. Then we can open the logfile in our system.
