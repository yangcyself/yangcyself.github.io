# meta

How to make a multiprocessor computer that correctly executes multiprocess programs


# CUE




# a quite nice example

process 1

```txt
a = 1;
if b = 0 then critical section;
        a := 0
    else ..   fi
```

process 2

```txt
b = 1;
if a = 0 then ciritcal section
        b := 0;
    else .... fi
```

this is a good exercise for the assertion technique

> 为啥举这个例子的时候没有考虑ab同时被赋值了1的情况，虽然原文里面提到...是一些让它保证不会死锁的机制

## two requirments

Requirement Rl: Each processor issues memory requests in the
order specified by its program.

Requirement R2: Memory requests from all processors issued to
an individual memory module are serviced from a single FIFO queue. Issuing a memory request consists of entering the request on this queue.

> Note 这两个说的其实是一个发指令的按顺序，一个处理指令的按顺序