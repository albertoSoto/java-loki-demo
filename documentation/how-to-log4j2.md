## Configuration Log4J2

### 1 - add dependencies

```
  <!--Using log4j-->
  <dependency>
    <groupId>pl.tkowalcz.tjahzi</groupId>
    <artifactId>log4j2-appender-nodep</artifactId>
    <version>0.9.31</version>
  </dependency>
```

### 2 - modify logger config

Example (for magnolia) at src/main/resources/log4j2-loki.xml

```
<Appenders>
    <Console name="console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d %-5p %-50.50c: %encode{%m}{CRLF}%n"/>
    </Console>
    
    <Loki name="loki-appender">
      <!--<host>${sys:loki.host}</host>
      <port>${sys:loki.port}</port>-->
      <url>http://localhost:3100/loki/api/v1/push</url>
      <PatternLayout>
        <Pattern>%X{tid} [%t] %d{MM-dd HH:mm:ss.SSS} %5p %c{1} - %m%n%exception{full}</Pattern>
      </PatternLayout>
      <Label name="server" value="${sys:hostname}"/>
    </Loki>
    ...
```

Modify it the general appender at the roo level 

````
<Root level="ALL">
  <AppenderRef ref="log-error"/>
  <AppenderRef ref="log-debug"/>
  <!--  debug  -->
  <AppenderRef ref="console"/>
  <AppenderRef ref="loki-appender"/>
</Root>
````

### 3 - Pickup the config file

As in magnolia, either change the .properties associate or link the new log configuration with the followin

```
-Dlog4j.config=/<mydata-folder>/src/main/resources/log4j2-loki.xml
```