# mvn build with multiple threads
From Maven 3.0+ onwards we have this additional arguments to the mvn command that tells how many number thread should be used for building the mvn project. This is very useful in saving the overall build time and noticed 50% improvement.

```sh
mvn clean install -T 2    # Builds with 2 threads
mvn clean install -T 1C   # 1 thread per cpu core
mvn clean install -T 1.5C # 1.5 thread per cpu core
```
More info in [https://cwiki.apache.org/confluence/display/MAVEN/Parallel+builds+in+Maven+3](https://cwiki.apache.org/confluence/display/MAVEN/Parallel+builds+in+Maven+3) 