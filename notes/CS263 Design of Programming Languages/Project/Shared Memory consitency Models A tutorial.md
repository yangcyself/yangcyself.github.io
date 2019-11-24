# meta

**shared memory programming models has several advantages over the message passing model**

> 如果书里面CCS是message passing model, 那么整个shared memory model是另外一大类

The memory consistency model of a shared memory multiprocessor formally specifies how the memory system will appear to the programmer. 

this paper also analysised the memory models from the computer systems' point of view.

# CUE


# models

uniprocessor model -exentded-> **sequential consistency model**

for optimization -> **relaxed consistency model**



# the relaxed models:

**relaxing write to read**

read may read previous writes from the same processor

**relaxing write to read and write to write**

writes to different locations from
the same processor to be pipelined or overlapped

**Relaxing all program orders**


**WEAK ORDERING**
clas- sifies memory operations into two categories: data operations and synchro- nization operations

**RELEASE CONSISTENCY**

Operations are first distinguished as ordinary or special,

Special opeirations are further dis- tinguished as sync or nsync

sync operations are further distinguished as acquire or release operations