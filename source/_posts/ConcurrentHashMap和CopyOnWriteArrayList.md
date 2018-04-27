title: ConcurrentHashMap和CopyOnWriteArrayList
author: ke cao
tags: []
categories:
  - Java
date: 2018-04-27 22:20:00
---

1. ConcurrentHashMap

ConcurrentHashMap其实就是线程安全版本的hashMap。简单的解释就是通过把整个Map分为N个Segment（类似HashTable），这样每个HashTable之间就线程就不会发生冲突，可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。
![image](http://7xlune.com1.z0.glb.clouddn.com/images/%E6%B7%B1%E5%85%A5%E5%89%96%E6%9E%90ConcurrentHashMap/ConcurrentHashMap.png)

2. CopyOnWriteArrayList

2.1 CopyOnWriteArrayList是线程安全版本的ArrayList。

2.2 什么是CopyOnWrite容器（写的时候复制） 
CopyOnWrite容器即写时复制的容器。通俗的理解是当我们往一个容器添加元素的时候，不直接往当前容器添加，而是先将当前容器进行Copy，复制出一个新的容器，然后新的容器里添加元素，添加完元素之后，再将原容器的引用指向新的容器。这样做的好处是我们可以对CopyOnWrite容器进行并发的读，而不需要加锁，因为当前容器不会添加任何元素。所以CopyOnWrite容器也是一种读写分离的思想，读和写不同的容器。

2.3 CopyOnWriteArrayList的实现原理 
在使用CopyOnWriteArrayList之前，我们先阅读其源码了解下它是如何实现的。 

2.3.1 写的时候：需要加锁 
以下代码是向CopyOnWriteArrayList中add方法的实现（向CopyOnWriteArrayList里添加元素），可以发现在添加的时候是需要加锁的，否则多线程写的时候会Copy出N个副本出来。

2.3.2 读的时候：不需要加锁 
读的时候不需要加锁，如果读的时候有多个线程正在向CopyOnWriteArrayList添加数据，读还是会读到旧的数据，因为写的时候不会锁住旧的CopyOnWriteArrayList。

2.4 相对于Arraylist线程安全，相对于vector，第一不会出现迭代器异常，第二提高了效率： 

2.4.1 迭代器异常（快速失败）： 
java中，集合在遍历的时候，如果内部被修改了会抛出java.util.ConcurrentModificationException错误。list和vector都会抛出

2.4.2 快速失败 
快速失败是指某个线程在迭代vector的时候，不允许其他线程修改该vector的内容，这样迭代器迭代出来的结果就会不准确，如用iterator迭代collection的时候，iterator就是另外起的一个线程，它去迭代collection，如果此时用collection.remove(obj)这个方法修改了collection里面的内容的时候，就会出现ConcurrentModificationException异常,这时候该迭代器就快速失败。 
通俗解释：就好像有一盘饺子，你要数数有几个，在你还没数完，其他人有放入（或拿走）了几个饺子。 
你就只能重新再数了。本来你数数就很快，但是，就有人比你手更快。

2.4.3 读的效率提高了 
由于都操作没有加锁，所以没有线程冲突；但写操作由于加锁，并采取了复制，所以效率更加低。所以此方法适用于读多写少修改少的应用。
<!-- more -->
一、阻塞队列

BlockingQueue.class，阻塞队列接口
BlockingDeque.class，双端阻塞队列接口
ArrayBlockingQueue.class，阻塞队列，数组实现
LinkedBlockingDeque.class，阻塞双端队列，链表实现
LinkedBlockingQueue.class，阻塞队列，链表实现
DelayQueue.class，阻塞队列，并且元素是Delay的子类，保证元素在达到一定时间后才可以取得到
PriorityBlockingQueue.class，优先级阻塞队列
SynchronousQueue.class，同步队列，但是队列长度为0，生产者放入队列的操作会被阻塞，直到消费者过来取，所以这个队列根本不需要空间存放元素；有点像一个独木桥，一次只能一人通过，还不能在桥上停留
二、非阻塞队列：

ConcurrentLinkedDeque.class，非阻塞双端队列，链表实现 
ConcurrentLinkedQueue.class，非阻塞队列，链表实现

三、转移队列：

TransferQueue.class，转移队列接口，生产者要等消费者消费的队列，生产者尝试把元素直接转移给消费者 
LinkedTransferQueue.class，转移队列的链表实现，它比SynchronousQueue更快

四、其它容器：

ConcurrentMap.class，并发Map的接口，定义了putIfAbsent(k,v)、remove(k,v)、replace(k,oldV,newV)、replace(k,v)这四个并发场景下特定的方法 
ConcurrentHashMap.class，并发HashMap 
ConcurrentNavigableMap.class，NavigableMap的实现类，返回最接近的一个元素 
ConcurrentSkipListMap.class，它也是NavigableMap的实现类（要求元素之间可以比较），同时它比ConcurrentHashMap更加scalable——ConcurrentHashMap并不保证它的操作时间，并且你可以自己来调整它的load factor；但是ConcurrentSkipListMap可以保证O(log n)的性能，同时不能自己来调整它的并发参数，只有你确实需要快速的遍历操作，并且可以承受额外的插入开销的时候，才去使用它 
ConcurrentSkipListSet.class，和上面类似，只不过map变成了set 
CopyOnWriteArrayList.class，copy-on-write模式的array list，每当需要插入元素，不在原list上操作，而是会新建立一个list，适合读远远大于写并且写时间并苛刻的场景 
CopyOnWriteArraySet.class，和上面类似，list变成set而已