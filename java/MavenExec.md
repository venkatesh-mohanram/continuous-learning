# Executing application using mvn command
The advantage of using mvn command with the plugin *exec-maven-plugin* to execute the application is that we dont have to worry about setting the classpath and finding the location of executable jar etc


We need to add the below definition inside the <build> section in pom

```xml
	<build>
    	<plugins>
    		<plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <configuration>
                    <mainClass>com.common.util.Application</mainClass>
                    <arguments>
		            	<argument>HELP</argument>
		          	</arguments>
                </configuration>
                <executions>
                    <execution>
                        <goals>
                            <goal>java</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
    	</plugins>
    </build>

```

And we need to use the below command to execute the application. We can have default argument set in the pom.xml itself and while executing if we want to change, then we can pass it via the *-Dexec.args' param

```
 mvn exec:java -Dexec.args="GET_VERSION"
```