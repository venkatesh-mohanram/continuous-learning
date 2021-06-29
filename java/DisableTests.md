# Disable all JUnit Tests in a module
Usually we can skip the execution of tests by adding ** -DskipTests ** argument along with other mvn command

Below snippet can be added to the module's pom.xml to skip all the tests in this particular module

```xml
   <!--   Disabling the tests in this module -->
   <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>        
        <configuration>
          <skipTests>true</skipTests>
        </configuration>
      </plugin>
    </plugins>
  </build>
```
