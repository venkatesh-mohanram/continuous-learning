# Decompile a class file in Linux
If we want to decompile the whole jar of the application then we have very good GUI tool [http://java-decompiler.github.io/](http://java-decompiler.github.io/). In this document I am going to cover the steps that we can follow to decompile just one class inside the jar

 * Download the decompiler, for latest version [http://www.benf.org/other/cfr/index.html](http://www.benf.org/other/cfr/index.html)

```bash
bash$ wget http://www.benf.org/other/cfr/cfr_0_151.jar
```
 * Retrieve the particular class which we want to decompile

```bash
bash$ unzip services-designtime-LATEST-SNAPSHOT.jar "mtms/infra/metadata/impl/MetadataClient.class"
```
 * Decompile the class using this command

```bash
bash$ cd mtms/infra/metadata/impl/
bash$ java -jar cfr-0.151.jar MetadataClient.class
```

