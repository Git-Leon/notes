# Creating an Uber Jar with Maven
## Creating a Shaded JAR
* The goals for the Shade Plugin are bound to the package phase in the build lifecycle.

## Configuring your Shade Plugin
* Add this body to your `pom.xml` to ensure the `mvn package` command will generate an uber jar upon build.
  * **To skip testing** upon build execute `mvn -Dmaven.test.skip=true package`.

```xml
<project>
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>3.1.1</version>
        <configuration>
          <!-- put your configurations here -->
        </configuration>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
  ...
</project>
```

## Creating Uber Jar using Shade plugin
* Navigate to the root of the project and execute `mvn package` to generate a `.jar` of the project
* Execute `mvn package Dmaven.test.skip=true` to skip tests upon packaging.

## Checking the contents of a `.jar` File
* You can check the contents of a jar file via the `jar tf jar-name` commmand.


-
# Uploading `.jar` to `packagecloud.io` for Private/Custom Dependency Imports
## Install Ruby

## Install `package_cloud` Ruby gem
* Install `package_cloud` Ruby gem by running `sudo gem install package_cloud `

## Push the `.jar` to your repository
* Navigate to the directory of your `.jar`
* Push the `.jar` to your repository.



### Generified command:
* **Multi-line view:**

```
package_cloud push
username/repositoryname
jar-name.jar
--coordinates=groupid:artifactid:version
```

* **Single-line view:**

```
package_cloud push username/repositoryname jar-name.jar --coordinates=groupid:artifactid:version
```


### Sample command:
* **Multi-line view:**

```
package_cloud push
git-leon/utils
project-assembly-generator-1.0.jar
--coordinates=com.github.git-leon:project-assembly-generator:1.0
```

* **Single-line view**

```
package_cloud push git-leon/utils project-assembly-generator-1.0.jar --coordinates=com.github.git-leon:project-assembly-generator:1.0
```
