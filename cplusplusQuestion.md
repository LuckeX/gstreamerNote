#### question 1

>  对于vector和string来说，当它们的需要更多空间时，就会自动增加空间，而每次增加空间的容量会导致很大的开销，首先必须分配新的内存块，它有容器目前容量的几倍（在大部分实现中，vector和string的容量每次变为2倍），然后把所有元素从容器的旧内存拷贝到它的新内存，接着销毁旧内存中的对象，最后回收旧内存。

---

为什么是2倍？



note

> https://www.cnblogs.com/fnlingnzb-learner/p/10411558.html
