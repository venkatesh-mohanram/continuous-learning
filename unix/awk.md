# Awk
awk is a useful utility in Linux to play with strings

## Usecase
I used awk to parse the *junit* results know the number of tests passed and number of tests failed. 
I used along with grep command to list down all the matching tags of where tests results are available

<b>Number of tests:</b>
```shell script
tests=$(grep "testsuite .*tests=\"[0-9]\"" -R resources --include TEST*.xml --include newman*.xml | awk -F 'tests=' '{print $2}' | awk '{print $1}' | awk -F '"' '{SUM += $2}; END {print SUM}')
```   
<b>Number of failures:</b>
```shell script
failures=$(grep "testsuite .*errors=\"[0-9]\"" -R resources --include TEST*.xml --include newman*.xml | awk -F 'errors=' '{print $2}' | awk '{print $1}' | awk -F '"' '{SUM += $2}; END {print SUM}')
```
## About each step
Input is
```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites name="LookUpTests" tests="6" time="1.079">
  <testsuite name="CleanLookup" id="22689ec4-f7b2-4b0e-990c-81e70f3ff582" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.188">
    <testcase name="Status code is 404" time="0.188" classname="LookUpTests"/>
  </testsuite>
  <testsuite name="CreateLookUp" id="c0958a6f-d1dc-4dcd-8364-392611bd2056" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.078">
    <testcase name="Status code is 204" time="0.078" classname="LookUpTests"/>
  </testsuite>
  <testsuite name="GetLookUp_VerifyCreate" id="341d5817-4003-498e-a53a-8b140232a80d" timestamp="2020-05-06T17:11:16.012Z" tests="3" failures="0" errors="0" time="0.107">
    <testcase name="Status code is 200" time="0.107" classname="LookUpTests"/>
    <testcase name="Columns found and names are correct." time="0.107" classname="LookUpTests"/>
    <testcase name="Number of rows matched Create" time="0.107" classname="LookUpTests"/>
  </testsuite>
  <testsuite name="UpdateLookUp" id="602af599-7df1-47ae-b6d3-426852c8dbd4" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.555">
    <testcase name="Status code is 204" time="0.555" classname="LookUpTests"/>
  </testsuite>
  <testsuite name="GetLookUp_VerifyUpdate" id="5629640a-d140-4ccd-abba-4814458dd931" timestamp="2020-05-06T17:11:16.012Z" tests="3" failures="0" errors="0" time="0.053">
    <testcase name="Status code is 200" time="0.053" classname="LookUpTests"/>
    <testcase name="Columns found and names are correct." time="0.053" classname="LookUpTests"/>
    <testcase name="Number of rows matched" time="0.053" classname="LookUpTests"/>
  </testsuite>
  <testsuite name="DeleteLookUp" id="75ebcdfb-4036-49c3-8404-358dc22f2560" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.098">
    <testcase name="Status code is 200" time="0.098" classname="LookUpTests"/>
  </testsuite>
</testsuites>
```
### 1. Grep
The grep command takes the regex pattern and the folder to look for
```shell script
grep "testsuite .*errors=\"[0-9]\"" -R resources --include TEST*.xml --include newman*.xml
```
And the output is
```shell script
resources/newman-run-report-2020-05-06-17-11-17-475-0.xml:  <testsuite name="CleanLookup" id="22689ec4-f7b2-4b0e-990c-81e70f3ff582" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.188">
resources/newman-run-report-2020-05-06-17-11-17-475-0.xml:  <testsuite name="CreateLookUp" id="c0958a6f-d1dc-4dcd-8364-392611bd2056" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.078">
resources/newman-run-report-2020-05-06-17-11-17-475-0.xml:  <testsuite name="GetLookUp_VerifyCreate" id="341d5817-4003-498e-a53a-8b140232a80d" timestamp="2020-05-06T17:11:16.012Z" tests="3" failures="0" errors="0" time="0.107">
resources/newman-run-report-2020-05-06-17-11-17-475-0.xml:  <testsuite name="UpdateLookUp" id="602af599-7df1-47ae-b6d3-426852c8dbd4" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.555">
resources/newman-run-report-2020-05-06-17-11-17-475-0.xml:  <testsuite name="GetLookUp_VerifyUpdate" id="5629640a-d140-4ccd-abba-4814458dd931" timestamp="2020-05-06T17:11:16.012Z" tests="3" failures="0" errors="0" time="0.053">
resources/newman-run-report-2020-05-06-17-11-17-475-0.xml:  <testsuite name="DeleteLookUp" id="75ebcdfb-4036-49c3-8404-358dc22f2560" timestamp="2020-05-06T17:11:16.012Z" tests="1" failures="0" errors="0" time="0.098">
```
### 2. Awk - split with tests= 
Takes the second part after splitting the test with the string '*tests=*'
```shell script
awk -F 'tests=' '{print $2}'
```
And the output is 
```shell script
"1" failures="0" errors="0" time="0.188">
"1" failures="0" errors="0" time="0.078">
"3" failures="0" errors="0" time="0.107">
"1" failures="0" errors="0" time="0.555">
"3" failures="0" errors="0" time="0.053">
"1" failures="0" errors="0" time="0.098">
```
### 3. Awk - By default awk uses ' ' as delimiter
Takes the first part after splitting with ''
```shell script
awk '{print $1}'
``` 
And the output is
```shell script
"1"
"1"
"3"
"1"
"3"
"1"
```
### 4. Awk - Executes statement
Another feature of awk is that it will execute set of statement. Here we are summing up all the individual results
```shell script
awk -F '"' '{SUM += $2}; END {print SUM}'
```
And the output is 
```shell script
10
```
