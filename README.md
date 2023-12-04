# Maven Test Project for JDK 21
Following this guide: https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

- Maven compiler plugin version: `3.11.0`

Generated with `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false`
Did not work out of the box. Applied this change
```xml
<project>
  [...]
  <build>
    [...]
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <source>21</source>
          <target>21</target>
        </configuration>
      </plugin>
    </plugins>
    [...]
  </build>
  [...]
</project>
```
The source java version ($JAVA_HOME) must be <= the target version. I think...
Also, this overrides the `properties` section. If you want to use properties instead, use:
```xml
<project>
  [...]
  <properties>
    <maven.compiler.source>21</maven.compiler.source>
    <maven.compiler.target>21</maven.compiler.target>
  </properties>
  [...]
</project>
```
Alternatively, it might be better to just use `release` option as in `javac --release <option>`
```xml
<project>
  [...]
  <properties>
    <maven.compiler.release>21</maven.compiler.release>
  </properties>
  [...]
</project>
```
https://stackoverflow.com/questions/43102787/what-is-the-release-flag-in-the-java-9-compiler

Build with `mvn package`

Then run with `java -cp target/maven-app-1.0-SNAPSHOT.jar com.mycompany.app.App`
