### How does the DevBoard handle received serial messages? How does this differ from the naïve approach?
For the DevBoard it receive serial messages through an interrupt which is an event driven signal that runs the code thus when we receieve a byte the event will be triggered. This approach is different from the naive one because for the naive approach it continuously checking for incoming bytes on the serial port and wasting energy. 

### What does `detached_callback` do? What would happen if it wasn't used?
The purpose of `detached_callback` is to mark any function that we want to be spawned in a detached thread meaning that we are creating independent threads running tasks seperately from main program. If this wasn't used then any serial code would get stuck or takes a long time and our UI will freeze during that time. 

### What does `LockedSerial` do? Why is it _necessary_?
For `LockedSerial` it wraps the serial object in a lock, that allows one thread to access it and it is necessary to avoid race condition because after spawning we now have multiple threads that could try to access the serial port at the same time.
