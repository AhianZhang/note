
# Java Concurrency JDK1.8
### Thread
***
``Thread.yield()``

>[A hint to the scheduler that the current thread is willing to yield
its current use of a processor.](https://docs.oracle.com/javase/8/docs/api/)

 提醒任务调度系统当前线程能够让出正在使用的线程

 这个方法很少使用，但是有助于复现在竞态条件时出现的错误

 《Thinking in Java》4th P1117 中有如下解释：
 >The call to the static method **Thread.yield()** inside **run()** is a suggestion
 to the thread scheduler(the part of the Java threading mechanism that moves
 the CPU from one thread to the next) that says,"I've done the important parts
 of my cycle and this would be a good time to switch to another task for a while."

 [与 join()方法的区别](http://www.importnew.com/14958.html) 写的很好，仔细阅读。

***
http://group.jobbole.com/33336/
http://blog.jobbole.com/113952/?utm_source=group.jobbole.com&utm_medium=relatedArticles
