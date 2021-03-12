# Exclude Jar from Test classpath
If for reasons where there are duplicate definition of classes in two jars and you want to exclude one of them while building and running the test code then we can use *surefire-plugin* with *classpathDependencyExcludes* option

## Error
If error similar to this is thrown while building the test code

```
the package org.w3c.dom is accessible from more than one module: <unnamed>, java.xml
```

## Solution

Add the below defintion in the pom.xml

```xml
<project>
  </dependencies>
       <dependency>
            <groupId>com.artifactory</groupId>
            <artifactId>saxon-dom4j</artifactId>
            <version>3.4.4</version>            
        </dependency>       
  </dependencies>
  ..
  ...
  ..
	<build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.0.0-M5</version>
        <configuration>
          <classpathDependencyExcludes>
            <classpathDependencyExclude>com.artifactory:saxon-dom4j</classpathDependencyExclude>
          </classpathDependencyExcludes>
        </configuration>
      </plugin>
    </plugins>
  </build>
<project>  
```