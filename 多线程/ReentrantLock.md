## ReentrantLock

#### state

```java
    AbstractQueuedSynchronizer
    /**
     * The synchronization state.
     */
    private volatile int state;
```

线程

```java
AbstractOwnableSynchronizer    
/**
 * The current owner of exclusive mode synchronization.
 */
private transient Thread exclusiveOwnerThread;
```



#### CLH FIFO双端队列

AQS使用一个Volatile的int类型的成员变量来表示同步状态，通过内置的FIFO队列来完成资源获取的排队工作，通过CAS完成对State值的修改

![CLH队列](./pic/CLH队列.png)

阻塞线程

```java
private final boolean parkAndCheckInterrupt() {
    LockSupport.park(this);
    return Thread.interrupted();
}
```

```java
public static void park(Object blocker) {
    Thread t = Thread.currentThread();
    setBlocker(t, blocker);
    unsafe.park(false, 0L);
    setBlocker(t, null);
}
```

唤醒线程

```java
private void unparkSuccessor(Node node) {
      /*
       * Try to clear status in anticipation of signalling.  It is
       * OK if this fails or if status is changed by waiting thread.
      */
     compareAndSetWaitStatus(node, Node.SIGNAL, 0);
 
     /*
      * Thread to unpark is held in successor, which is normally
      * just the next node.  But if cancelled or apparently null,
      * traverse backwards from tail to find the actual
      * non-cancelled successor.
      */
     Node s = node.next;
     if (s == null || s.waitStatus > 0) {
         s = null;
         for (Node t = tail; t != null && t != node; t = t.prev)
             if (t.waitStatus <= 0)
                 s = t;
    }
     if (s != null)
         LockSupport.unpark(s.thread);
 }
```

