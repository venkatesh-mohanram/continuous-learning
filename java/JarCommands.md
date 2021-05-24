# Listing files inside a jar
If we want to know the files inside the jar file then we can use the below commands

Used to display the files inside the jar with additional details 

```sh
jar tvf <jar-file>
```

To know whether particular class is present or not

```sh
jar tvf <jar-file> | grep <class-regex-pattern>
```

## Reference
[https://docs.oracle.com/javase/tutorial/deployment/jar/basicsindex.html](https://docs.oracle.com/javase/tutorial/deployment/jar/basicsindex.html)