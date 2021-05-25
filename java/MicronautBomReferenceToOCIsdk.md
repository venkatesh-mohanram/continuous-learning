# Micronaut BOM and OCI SDK
The bom or Bill Of Material in the maven is really a cool way to manage the bunch of dependencies. In this notes, I am going to mention how we can find what version of OCI SDK is being used by a particular version of Micronaut

**Step 1:** Identify which version of Micronaut is used in the application (eg: 2.5.4)

**Step 2:** Open its corresponding POM [https://repo1.maven.org/maven2/io/micronaut/micronaut-bom/2.5.4/micronaut-bom-2.5.4.pom](https://repo1.maven.org/maven2/io/micronaut/micronaut-bom/2.5.4/micronaut-bom-2.5.4.pom)

**Step 3:** It will have too many properties, look for *micronaut.oraclecloud.version*

```xml
<micronaut.data.version>2.4.3</micronaut.data.version>
<micronaut.oraclecloud.version>1.3.5</micronaut.oraclecloud.version>
<micronaut.r2dbc.version>1.1.1</micronaut.r2dbc.version>
<micronaut.cache.version>2.4.0</micronaut.cache.version>

```
**Step 4:** Open the corresponding version of micronaut-oraclecloud-bom [https://repo1.maven.org/maven2/io/micronaut/oraclecloud/micronaut-oraclecloud-bom/1.3.5/micronaut-oraclecloud-bom-1.3.5.pom](https://repo1.maven.org/maven2/io/micronaut/oraclecloud/micronaut-oraclecloud-bom/1.3.5/micronaut-oraclecloud-bom-1.3.5.pom)

**Step 5:** Look for the group *com.oracle.oci.sdk* and checks its version and that is the OCI SDK version used by the Micronaut 2.5.4. 

```xml
<dependency>
<groupId>com.oracle.oci.sdk</groupId>
<artifactId>oci-java-sdk-addons-resteasy-client-configurator</artifactId>
<version>1.34.0</version>
</dependency>
```