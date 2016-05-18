# Write a JVM profiler from scratch

####Problem Statement

- How do we profile a number of jvms that are all running in a distributed environment?   Moreover, storing and transferring the snapshot 
files produced by some profilerscan be problematic due to the large size of the snapshots and effectively collecting and analyzing these files.

- I would also like to learn how to implement a java agent into a jvm that can collect information and send it out.


####Notes on JVM agent implementation

1. Define a class that has a premain method with this signature
2. The agent class should be packaged in a JAR whose manifest specifies the Premain-Class attribute
```shell
  Premain-Class: com.etsy.agent.ExampleAgent
```
3. Use Maven to build the agent, in order to use maven-shade-plugin’s ManifestResourceTransformer to set this property, 
but other build tools have similar facilities. Need to know how this works in gradle?
4. Use JVM’s management interface to actually obtain the profiling data.  java.lang.management.ManagementFactory provides a number of 
MXBeans that expose information about various components of the JVM, including memory usage, the garbage collector, and running threads.  

#### Questions
1. What happens to the agent when the main jvm thread exits? 
2. How to deal with jvm [safepoints](used the JVM’s management interface to actually obtain the profiling data. java.lang.management.ManagementFactory provides a number of MXBeans that expose information about various components of the JVM, including memory usage, the garbage collector, and running threads.)?


