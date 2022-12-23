# IPC
&emsp; The purpose of this programming assignment is to compare the performance of various
IPC methods during the exchange of data between the client and the server. The code was
modified from the first programming assignment by creating a flag that will take two different
signals which will execute the varying IPC methods. This is done by using a base class known
as the Request queue, which will be implemented in a form of polymorphism.\
&emsp; There were a few modifications made to the server in the program. The first change that
was made was to change the FIFO request channel to ensure both methods could be used.
Next, the if else-if else statement was added to the end to act as a selector for which channel
will execute. This will be done by adding a case for the i flag in the getopt() function. If the
argument is q then the message queue will be used, if the argument is s then the shared
memory will be used, and by default, the FIFO channel will be used. Finally, the same branch
was added to the process of new channel requests.\
&emsp; Next, the client was modified similarly to how the server was modified. The FIFO request
channels were changed, an i case was added to the getopt() function, and a branch of
conditions in regards to the channels were added. The execvp() system call was also modified
to accept the i case and the method being passed as well. If the user decides to create multiple
channels the channels would be appended to a vector which will store the individual channels. If
The user decides to create multiple channels with time being zero and person being greater
than zero, then there will be a for loop executing the thousand data point requests for each
channel.\
&emsp; If q is passed then the message Queue method will be used to perform the IPC. This is
implemented through a class that is based on the request class. First, a constructor was
implemented which will use the mq_open() function for the appropriate connection for a certain
condition passed. The purpose of the constructor is to establish a connection between the
processes. The destructor was also implemented by using the mq_close() and the mq_unlink()
functions which will remove the connection between the processes. The cread function was
implemented by using the mq_recieved() function. The cwrite function was implemented by
using the mq_send() function.\
&emsp; The shared memory queue was implemented by using polymorphism by nesting the
SHMQueue into the SHMQRequest channel. The SHMQueue data structure was implemented
using a constructor/destructor along with both a sending and receiving function. The
SHMQueue constructor was implemented by using a file descriptor to open the shared memory
using the shm_open() function. This file descriptor was then truncated at a given amount of
length that was passed using the ftruncate() function. Then an if-else statement was used to
map the memory with given permissions that could either be read or write using the mmap()
function. Finally, the file descriptor was closed and two semaphores were created using the
sem_open() function.\
&emsp; The destructor was implemented by first using the numap() function to unmap the
memory along with shm_unlink to disconnect the memory. Then the semaphores were unlinked
as well using the sem_unlink() function along with closing them with sem_close(). The
shm_receive and shm_send functions were both implemented similarly. Both functions used the
sem_wait() function on each semaphore and the sem_post() function as well to signal their
semaphore when to allow the critical section to be executed.\
&emsp; The SHM request channel was implemented similarly to the other channel classes with a
constructor, destructor, cread, and cwrite function. The class used the Request channel base
class just like the message queue class. The constructor function initialized my_name,
passed_side, passed_lenght. It also initialized the two SHMQueue member variables by
dynamically allocating memory using the SHMQueue constructor with appropriate arguments.
The destructor was implemented by deleting the SHMQueue variables and setting them to a
nullptr. The cread used the shm_recieve() function from the SHMQueue class. This was then
assigned to one of the member variables and the data was returned. The cwrite function was
implemented exactly like cread only the shm_send() function was used instead.
