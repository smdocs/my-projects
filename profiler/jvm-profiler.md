# Write a JVM profiler from scratch

####Problem Statement

1) How do we profile a number of jvms that are all running in a distributed environment?   Moreover, storing and transferring the snapshot 
files produced by some profilerscan be problematic due to the large size of the snapshots and effectively collecting and analyzing these files.

2) I would also like to learn how to implement a java agent into a jvm that can collect information and send it out.


####Notes on JVM agent implementation

1) Define a class that has a premain method with this signature

2) The agent class should be packaged in a JAR whose manifest specifies the Premain-Class attribute
```shell
  Premain-Class: com.sm.agent.ExampleAgent
```
3) Use Maven to build the agent, in order to use maven-shade-plugin’s ManifestResourceTransformer to set this property, 
but other build tools have similar facilities. Need to know how this works in gradle?

4) Use JVM’s management interface to actually obtain the profiling data.  java.lang.management.ManagementFactory provides a number of 
MXBeans that expose information about various components of the JVM, including memory usage, the garbage collector, and running threads.  

#### Features

1) Profiler should profile heap and non-heap memory usage, garbage collection, and the aggregate time spent executing each function.

#### Questions
1. What happens to the agent when the main jvm thread exits? 

If the profiler runs as a non deamon thread then when the main thread of the jvm exits, it will still keep the jvm alive. This is not the ideal behaviour of a profiler. 

2. How to deal with jvm [safepoints](http://psy-lob-saw.blogspot.com/2014/03/where-is-my-safepoint.html)?

[Code as creaft](https://codeascraft.com/2015/01/14/introducing-statsd-jvm-profiler-a-jvm-profiler-for-hadoop/)

```java

public abstract class Profiler {

   /** Start profiling the target jvm. */
   public void profile();
   
   /** Start reporting metrics.*/
   public void report();
   
   /** Start recording metrics */
   public void record();
}

```


