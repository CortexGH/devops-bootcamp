# Maven

This section is designed to give you an introduction to Maven with a focus on the Maven approach of software building, package handling, and more.

<center>

  ![](img4/compile.svg ':size=125px')

</center>

## Introduction

Maven is a build automation tool, primarily used with Java projects.
Maven allows developers to describe project structure and dependencies, and
it's capable of building, testing, packaging, and deploying the project
automatically.

Starting out, you should read the following articles:
 - [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
 - [Introduction to the POM](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)
 - [Introduction to the Dependency Mechanism](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)
 - [Introduction to the Build Lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)

## Convention over Configuration

Read about [The Maven Way](https://www.cloudbees.com/blog/maven-way%E2%84%A2) over at cloudbees.com.
>"Ant is simply a toolbox whereas Maven is about the application of patterns in order to achieve an infrastructure which displays the characteristics of visibility, reusability, maintainability, and comprehensibility."
>
> \- [Philosophy of Maven, maven.apache.org](https://maven.apache.org/background/philosophy-of-maven.html)

The primary key to The Maven Way is convention over configuration. This means
that sticking to the standard way of setting up a project will be easy with
Maven, but the more you deviate from the norm the more additional configuration
will be required.

Maven is capable of a significant amount of work with only minor changes to
the POM file. This is thanks to the principle of convention over configuration.
Maven has some idea of how to build a project with only minimal information,
and additional configuration isn't always needed.

## Maven Lifecycle

Maven has a simple, standard lifecycle which is defined by several phases.
Listed here are some important phases in the default lifecycle.

| Phase    | Description                                                                        |
|----------|------------------------------------------------------------------------------------|
| Validate | Validate the Maven configuration                                                   |
| Compile  | Compile the project code                                                           |
| Test     | Unit test the compiled code                                                        |
| Package  | Package the compiled code into a distributable format, such as JAR                 |
| Verify   | Run checks to verify the package is correct                                        |
| Install  | Install the package on the local machine, making it available for projects locally |
| Deploy   | Copy the package to a remote repository, making it available to other developers   |

Each phase is the lifecycle runs one after another, in order. This means that
when `mvn package` is run, the prior phases will also run. Understanding that
these phases occur in any Maven project helps give developers an understanding
of Maven conventions, and makes it easy to understand the build process for
any Maven project.

## Group, Artifact, Version

Maven identifies artifacts using a simple combination of three values, each
of which is defined in the POM file. Projects can share some values, but in
general Maven requires that no two builds share all of the following.

| Identifier | Description                                                   |
|------------|---------------------------------------------------------------|
| groupId    | Identifies the group or organization that created the project |
| artifactId | Provides the name of project and the artifact that is built   |
| version    | Denotes the version number of the project                     |


```xml
<groupId>org.springframwork.samples</groupId>
<artifactId>spring-petclinic</artifactId>
<version>1.0.0-SNAPSHOT</version>
```

Read [guide to naming conventions](https://maven.apache.org/guides/mini/guide-naming-conventions.html)
to learn common strategies for naming Maven projects.

## Exercise

In this exercise you will create a skeleton web application using Maven, add a plugin to help with local development, update the version number and create a release.

 1. Create a new application using the archetype.
```
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-webapp
```
 2. Add Jetty to `pom.xml`.
```
<build>
        <plugins>
            <plugin>
                <groupId>org.mortbay.jetty</groupId>
                <artifactId>maven-jetty-plugin</artifactId>
                <version>6.1.10</version>
                <configuration>
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <connectors>
                        <connector implementation="org.mortbay.jetty.nio.SelectChannelConnector">
                            <port>8080</port>
                            <maxIdleTime>60000</maxIdleTime>
                        </connector>
                    </connectors>
                </configuration>
            </plugin>
        </plugins>
</build>
```
 3. Run Jetty.
```
mvn jetty:run
```
 4. Investigate the Maven Internal (local) repo. What does it contain? What is its purpose?
 5. What changes occur in the project directory and the local repo when running `mvn package` and when running `mvn install`?
 6. Update the project version in the pom.xml and run `mvn package` and `mvn install` again. What has been updated in the local repo?

# Deliverable

Discuss the significance of the POM, dependencies and where they are sourced, and versions from a Maven perspective with your group.