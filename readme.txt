<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

  <modelVersion>4.0.0</modelVersion>

  <groupId>Camel</groupId>
  <artifactId>camel-spring-boot</artifactId>
  <packaging>jar</packaging>
  <version>1.0</version>

  <name>CamelSpringBootRoute</name>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <maven.compiler.release>17</maven.compiler.release>
    <surefire.plugin.version>3.0.0-M4</surefire.plugin.version>
  </properties>

  <!-- TODO EXTRA -->
  <repositories>
    <repository>
      <id>redhat-ga-repository</id>
      <url>https://maven.repository.redhat.com/ga/</url>
    </repository>
  </repositories>
  <!-- TODO EXTRA END -->

  <dependencyManagement>
    <dependencies>
      <!-- Spring Boot BOM -->
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>3.2.0</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <!-- Camel BOM -->
      <dependency>
        <groupId>org.apache.camel.springboot</groupId>
        <artifactId>camel-spring-boot-bom</artifactId>
        <!-- TODO EXTRA -->
        <version>4.0.0.redhat-00036</version>
        <!-- TODO EXTRA END -->
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <dependencies>

    <!-- Spring Boot -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
      <exclusions>
        <exclusion>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-undertow</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-logging</artifactId>
    </dependency>


    <!-- Camel -->
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-spring-boot-starter</artifactId>
    </dependency>
    <!-- TODO -->
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-stream-starter</artifactId>
    </dependency>
    <!-- ↑↑↑しかし上記の部分、4.2.0にもある -->
    <!-- ↑↑↑ないとエラーになるので、必要 -->
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-amqp-starter</artifactId>
    </dependency>
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-servlet-starter</artifactId>
    </dependency>
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-jackson-starter</artifactId>
    </dependency>
    <!-- TODO END -->

    <!-- Test -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-test-spring-junit5</artifactId>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <version>3.2.0</version>
        <executions>
          <execution>
            <goals>
              <goal>repackage</goal>
            </goals>
          </execution>
        </executions>
      </plugin>

      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <!--<release>11</release>-->
          <source>17</source>
          <target>17</target>
        </configuration>
      </plugin>

      <!-- maven-assembly-pluginを追加 -->
      <plugin> 
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-assembly-plugin</artifactId>
        <version>3.2.0</version>
        <configuration>
          <finalName>${project.name}</finalName>
          <appendAssemblyId>false</appendAssemblyId>
          <descriptorRefs>
            <!-- アセンブリディスクリプタの設定 -->
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
          <!--<archive>
            <manifest>
              <mainClass>camel.MySpringBootApplication</mainClass>
            </manifest>
          </archive> -->
        </configuration>
        <executions>
          <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
      </plugin>

       
    </plugins>
  </build>

</project>

