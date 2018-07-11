# Spring-Boot Camel and JSON logging for EFK

This example demonstrates how you can use Apache Camel with Spring Boot and log in JSON for EFK

### Code generation
Project is generated with the command:

    mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate \
      -DarchetypeCatalog=https://maven.repository.redhat.com/earlyaccess/all/io/fabric8/archetypes/archetypes-catalog/2.2.0.fuse-000092-redhat-2/archetypes-catalog-2.2.0.fuse-000092-redhat-2-archetype-catalog.xml \
      -DarchetypeGroupId=org.jboss.fuse.fis.archetypes \
      -DarchetypeArtifactId=spring-boot-camel-archetype  \
      -DarchetypeVersion=2.2.0.fuse-000092-redhat-2


### Configuration
The only changes done to the above artifact are:

Add logstash-logback-encoder dependency compatible with the logback dependencies included by Spring starters:


    <dependency>
        <groupId>net.logstash.logback</groupId>
        <artifactId>logstash-logback-encoder</artifactId>
        <version>5.1</version>
    </dependency>


Configure JSON based encoder:

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE xml>
    <configuration scan="true" scanPeriod="30 seconds" >
      <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="net.logstash.logback.encoder.LogstashEncoder"/>
      </appender>
      <root level="info">
        <appender-ref ref="STDOUT" />
      </root>
    </configuration>

### Building

The example can be built with

    mvn clean install
    mvn spring-boot:run
    
    mvn fabric8:deploy
    oc get pods
    oc logs <name of pod>


