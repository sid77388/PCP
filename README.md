Project title: Implementation of Producer and Consumer Problem using semaphore.

Introduction to Semaphore:

A semaphore is a variable or abstract data type used to control access to a common resource by multiple processes in a concurrentsystem such as a multitasking operating system. Semaphores are integer variables that are used to solve the critical section problem by using two atomic operations, wait and signal that are used for process synchronization. 

We can consider a situation where there are two people who wants to share a bike. At one time only one person can use the  bike. The one who has the bike key will get the chance to use it. And when this person gives the key to 2nd person, then only 2nd person can use the bike. Semaphore is just like this Key and the bike is the shared resource. Whenever a task wants access to the shared resource, it must acquire the semaphore first. The task should release the semaphore after it is done with the shared resource. Till this time all other tasks have to wait if they need access to shared resource as semaphore is not available. Even if the task trying to acquire the semaphore is of higher priority than the task acquiring the semaphore, it will be in wait state until semaphore is released by the lower priority task. 

Initialize a semaphore variable S.
Semaphore integer variable access only through two standard atomic functions:

1.Wait function

wait(S)

{

	while(s<=0)
  
	s-=1;
  
}



2.Signal function

signal(S)

{

	S+=1;
  
}

Types of Semaphore:

1.Binary Semaphore – This is similar to mutex lock but not the same thing. It can have only two values – 0 and 1. Its value is initialized to 1. It is used to implement the solution of critical section problem with multiple processes.

2.Counting Semaphore – Its value can range over an unrestricted domain. It is used to control access to a resource that has multiple instances.


Producer and consumer problem:

Producer consumer problem is also known as bounded buffer problem. In this problem we have two processes, producer and consumer, who share a fixed size buffer. Producer work is to produce data or items and put in buffer. Consumer work is to remove data from buffer and consume it. We have to make sure that producer do not produce data when buffer is full and consumer do not remove data when buffer is empty. The producer should go to sleep when buffer is full. Next time when consumer removes data it notifies the producer and producer starts producing data again. The consumer should go to sleep when buffer is empty. Next time when producer add data it notifies the consumer and consumer starts consuming data. This solution can be achieved using semaphores.

We will initialize some variables

S=1(for semaphore ME)

E=5(to check if buffer is empty or not)

F=0(Full or not)

Producer solution:

P1

{

	Produce(); // produce item
  
	Wait(E); //check if empty
  
	Wait(S); // check if consumer is taking
  
	append(); // append the value
  
	signal(S);
  
	signal(F);
  
}

Consumer solution:

P2

{

	wait(F); // check if value is there
  
	wait(S); //check if producer is performing action
  
	take(); //consume
  
   signal(S);
  
   signal(E);
  
}


 Real time example:
 
The most common real-life example of the Producer-Consumer algorithm is a process, called print spooling. Print spooling refers to putting jobs(in this case documents that are about to be printed) into a special location(buffer) in either computer memory, or hard disk, so that a printer could access this document whenever the printer is ready. There are couple of advantages of spooling. First of all the printer can access data from the buffer at any rate that is suitable for the printer. Secondly the work of computer is not interrupted while printing, thus a user can perform other tasks. As it was mentioned mentioned above, producer and consumer have to know about the state of each other, so they would know when each one of them can produce/consume. 
