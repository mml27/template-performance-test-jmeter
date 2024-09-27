<h1 align="center"><img src="https://jmeter.apache.org/images/logo.svg" alt="Apache JMeter logo" /></h1>

Github: https://github.com/apache/jmeter/tree/master

An Open Source Java application designed to measure performance and load test applications.

By The Apache Software Foundation

[![codecov](https://codecov.io/gh/apache/jmeter/branch/master/graph/badge.svg)](https://codecov.io/gh/apache/jmeter)
[![License](https://img.shields.io/:license-apache-brightgreen.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![Stack Overflow](https://img.shields.io/:stack%20overflow-jmeter-brightgreen.svg)](https://stackoverflow.com/questions/tagged/jmeter)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.apache.jmeter/ApacheJMeter/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.apache.jmeter/ApacheJMeter)
[![Twitter](https://img.shields.io/twitter/url/https/github.com/apache/jmeter.svg?style=social)](https://twitter.com/intent/tweet?text=Powerful%20load%20testing%20with%20Apache%20JMeter:&url=https://jmeter.apache.org)

## What Is It?

Apache JMeter can measure performance and load test static and dynamic web applications.

It can be used to simulate a heavy load on a server, group of servers,
network or object to test its strength or to analyze overall performance under different load types.

![JMeter screen](https://raw.githubusercontent.com/apache/jmeter/master/xdocs/images/screenshots/jmeter_screen.png)

## Features

Complete portability and 100% Java.

Multi-threading allows concurrent sampling by many threads and
simultaneous sampling of different functions by separate thread groups.

### Protocols

Ability to load and performance test many applications/server/protocol types:

- Web - HTTP, HTTPS (Java, NodeJS, PHP, ASP.NET,...)
- SOAP / REST Webservices
- FTP
- Database via JDBC
- LDAP
- Message-oriented Middleware (MOM) via JMS
- Mail - SMTP(S), POP3(S) and IMAP(S)
- Native commands or shell scripts
- TCP
- Java Objects

### IDE

Fully featured Test IDE that allows fast Test Plan **recording**
 (from Browsers or native applications), **building** and **debugging**.

### Command Line

[Command-line mode (Non GUI / headless mode)](https://jmeter.apache.org/usermanual/get-started.html#non_gui)
to load test from any Java compatible OS (Linux, Windows, Mac OSX, ...)

### Reporting

A complete and ready to present [dynamic HTML report](https://jmeter.apache.org/usermanual/generating-dashboard.html)

![Dashboard screenshot](https://raw.githubusercontent.com/apache/jmeter/master/xdocs/images/screenshots/dashboard/response_time_percentiles_over_time.png)

[Live reporting](https://jmeter.apache.org/usermanual/realtime-results.html)
into 3rd party databases like InfluxDB or Graphite

![Live report](https://raw.githubusercontent.com/apache/jmeter/master/xdocs/images/screenshots/grafana_dashboard.png)

### Correlation

Easy correlation through ability to extract data from most popular response formats,
[HTML](https://jmeter.apache.org/usermanual/component_reference.html#CSS/JQuery_Extractor),
[JSON](https://jmeter.apache.org/usermanual/component_reference.html#JSON_Extractor),
[XML](https://jmeter.apache.org/usermanual/component_reference.html#XPath_Extractor) or
[any textual format](https://jmeter.apache.org/usermanual/component_reference.html#Regular_Expression_Extractor)

### Highly Extensible Core

- Pluggable Samplers allow unlimited testing capabilities.
- **Scriptable Samplers** (JSR223-compatible languages like Groovy).
- Several load statistics can be chosen with **pluggable tiers**.
- Data analysis and **visualization plugins** allow great extensibility and personalization.
- Functions can be used to provide dynamic input to a test or provide data manipulation.
- Easy Continuous Integration via 3rd party Open Source libraries for Maven, Gradle and Jenkins.

## The Latest Version

Details of the latest version can be found on the
[JMeter Apache Project web site](https://jmeter.apache.org/)

## Requirements

The following requirements exist for running Apache JMeter:

- Java Interpreter:

  A fully compliant Java 8 Runtime Environment is required
  for Apache JMeter to execute. A JDK with `keytool` utility is better suited
  for Recording HTTPS websites.

- Optional jars:

  Some jars are not included with JMeter.
  If required, these should be downloaded and placed in the lib directory
  - JDBC - available from the database supplier
  - JMS - available from the JMS provider
  - [Bouncy Castle](https://www.bouncycastle.org/) -
  only needed for SMIME Assertion

- Java Compiler (*OPTIONAL*):

  A Java compiler is not needed since the distribution includes a
  precompiled Java binary archive.
  > **Note** that a compiler is required to build plugins for Apache JMeter.

## Installation Instructions

> **Note** that spaces in directory names can cause problems.

- Release builds

  Unpack the binary archive into a suitable directory structure.


## Project layout 

```
performance-test
│   TestPlanCTTI.jmx            -> JMX file with performance test configuration
│   user.properties             -> porperties file
│
└───.devcontainer               -> IDE VSCode container definition
    │   devcontainer.json

```

## Clon repository
```bash
git clone http://git.ctti-eks.aws/devsecops/performance-test.git
```
If use VS Code & Docker the project might be executed inside a container

## Set Up Vars

1. Open user.properties 
2. Change values where needed

- `threadCount` is number of users
- `rampup` is ramp up
- `testDuration` is duration of the test
- `thresholdTime` és el temps máx permès per a cada mostra (millisegons)
- `failures` és el nombre de mostres fallades
- `maxErrors` és el màxim d'errors permesos

## Running JMeter

1. Change to the `bin` directory or set PATH with jmeter bin folder
2. Create folder where HTML Reports will be stored  `HTMLReports`
3. Run the `jmeter.sh` (Unix) file
```bash
jmeter  -n -t TestPlanCTTI.jmx  -e -o HTMLReports -l log.jtl -q user.properties -JinfluxdbUrl="http://.../api/v2/write?org=[token]&bucket=[bucketName]" -Jjira_pk="[Jira Proyect Key]" -Jenvironment="[environment]" -JinfluxdbToken="[Token]" -Jbucket="[bucket]" -Jthresold=[max time per sample(ms)] -Jfailures=[nº failed samples] -JmaxErrors=[max nº errors]
```
4. or `jmeter.bat`(Windows) file
```bash
jmeter.bat  -n -t TestPlanCTTI.jmx  -e -o HTMLReports -l log.jtl -q user.properties -JinfluxdbUrl="http://.../api/v2/write?org=[token]&bucket=[bucketName]" -Jjira_pk="[Jira Proyect Key]" -Jenvironment="[environment]" -JinfluxdbToken="[Token]" -Jbucket="[bucket]" -Jthresold=[max time per sample(ms)] -Jfailures=[nº failed samples] -JmaxErrors=[max nº errors]
```

*In case any parameter is sent in duplicate in the user.properties file and by -J commands, the one sent by the -J command shall take precedence.

*In case one of the parameters (for example, threadCount) is only sent in the user.properties file and not with the -J command, the test will be performed with the parameters sent with the -J command, except for the threadCount, which will be taken from the user.properties file.

*If the threadCount, testDuration and rampup parameters are not declared either in the user.properties file or with the -J command, JMeter will default to a value of 1. 

## Developer Information

Building and contributing is explained in details at
[building JMeter](https://jmeter.apache.org/building.html)
and [CONTRIBUTING.md](CONTRIBUTING.md). More information on the tasks available for
building JMeter with Gradle is available in [gradle.md](gradle.md).

The code can be obtained from:

- https://github.com/apache/jmeter
- https://gitbox.apache.org/repos/asf/jmeter.git

## Licensing and Legal Information

For legal and licensing information, please see the following files:

- [LICENSE](LICENSE)
- [NOTICE](NOTICE)



