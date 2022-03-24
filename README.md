# Stacks core-cqrs module

## Module Overview

This module provides functionality to implement a basic CQRS functionality, by using the 
`ApplicationCommand` and `CommandHandler` classes. Please refer to sny of the [CQRS](https://github.com/amido/stacks-java-cqrs/)
and [CQRS with Events](https://github.com/amido/stacks-java-cqrs-events/) Stacks workload templates.

## Module Structure

In the following diagram, you can see all the relevant files of this module. Be aware, pulling from
the repository will have some extra files that are not relevant to the logic but required to build and
deploy.

### Project structure

    java
    \_.mvn
    : |_settings.xml
    |_archetype.properties
    |_pom.xml
    \_src
    : \_main
    :   \_java
    :    \_com.amido.stacks.core.cqrs
    :     \_command
    :      |CommandHandler.java
    :     \_handler
    :      |_CommandHandler.java

## How to use

There are four ways to integrate this module into your project:

-  Use it as a [dependency](#use-it-as-a-dependency)
-  Create a localized solution using [Maven Archetypes artifacts](#localized-solution-using-maven-archetypes) available in our Artifactory repo
-  Clone this repo, [locally build](#building-the-module-locally-from-this-repository) and use it as a Maven dependency
-  Clone this repo, create a [custom archetype](#creating-an-archetype-from-this-repository) and then use it as a Maven dependency

### Use it as a dependency

#### Maven

In the `dependencies` section of your application's `pom.xml` add:

```xml
<dependency>
    <groupId>com.amido.stacks.modules</groupId>
    <artifactId>stacks-core-commons</artifactId>
    <version>1.0.0</version>
</dependency>
```

Then you can do a `./mvnw clean compile` to fetch it; after that, you can use it like any other dependency.

```bash
./mvnw clean compile
```

#### Others

Use it as you'd use any dependency in your build tool.

### Localized solution using Maven Archetypes

If you wish to customise the module and use your organisation's namespaces instead of Amido's. You can create a
[Maven archetype](https://maven.apache.org/archetype/index.html). Archetype is Maven's tool for
scaffolding and offers lots of extra functionality. We suggest spending some time looking into them. We use Archetype to create a template and enable you to adopt this module under your organisation's namespace.
To use the deployed archetypes:

1.  Make and move to a new folder
2.  Then run

    ``` bash
    mvn archetype:generate \
        -DarchetypeGroupId='com.amido.stacks.modules' \
        -DarchetypeArtifactId='stacks-core-cqrs-archetype' \
        -DarchetypeVersion='<archetype version>' \
        -DgroupId='<your-group-id>' \
        -DartifactId='<your-artifact-id>' \
        -Dversion='<your-version>' \
        -Dpackage='<package-name>'
    ```

    -  `<your-group-id>` is a placeholder for your group ID
    -  `<your-artifact-id>` is a placeholder for your artefact ID
    -  `<your-version>` is a placeholder for your version
    -  `<package-name>` is a placeholder for the root package name and structure. It should start with your `groupdId` and continue with the name of the root package.

    > For example, using `-DgroupId=com.test` and `-Dpackage=com.test.stacks` will instruct Maven to place the code in `src/main/java/com/test/stacks` and update all the relevant references accordingly (i.e. `imports`)

3.  Go to the `pom.xml` file of the project you'll be using this module in and add it as a [dependency](#use-it-as-a-dependency)

**Example**: Using `-DgroupId=com.test` and `-Dpackage=com.test.stacks` will instruct Maven to place the code in `src/main/java/com/test/stacks` and update all the relevant references accordingly (i.e. `imports`)

> **If you previously had used this module under different namespace (i.e. the default `com.amido.stacks.core-cqrs`):**
>
> Maven ONLY updates the imports for the module you generated. Any references in other projects will remain to the previous namespace.
>
> You will need to
>
>-  Update them manually
>-  Re-create the relevant `import` statements to use the new-made module instead
>-  If you plan to use this with Amido Stacks, include your namespace in the `@ComponentScan` annotation of the `Application` class.

### Building the module locally from this repository

To build the module locally:

1.  Clone this repo
2.  Navigate to the `java` folder
3.  run `./mvnw clean install` to install the module locally.
4.  Add it as any other [dependency](#use-it-as-a-dependency)

### Creating an Archetype from this repository

If you wish to customise the module and use your organisation's namespaces instead of Amido's. You can create a
[Maven archetype](https://maven.apache.org/archetype/index.html). Archetype is Maven's tool for
scaffolding and offers lots of extra functionality. We suggest spending some time looking into them. We use Archetype to create a template and enable you to adopt this module under your organisation's namespace.
To use the deployed archetypes:
To build, install and use the archetype follow these steps:

1.  Clone this repo
2.  Navigate to the `<directory you cloned the project into>/java` in the terminal
3.  Then issue the following Maven commands, using the included wrapper:
    1.  Create the archetype from the existing code

        ```bash
        ./mvnw archetype:create-from-project -DpropertyFile='./archetype.properties'
        ```

    2.  Navigate to the folder it was created in

        ```bash
        cd target/generated-sources/archetype
        ```

    3.  Install the archetype locally

        ```bash
        ..\..\..\mvnw install
        ```

4.  Make and navigate to a directory in which you'd like to create the localized project, ideally outside this project's root folder
5.  To create the project, use the command below:

    ```bash
    <path-to-mvn-executable>/mvnw archetype:generate \
        -DarchetypeGroupId='com.amido' \
        -DarchetypeArtifactId='stacks-core-cqrs' \
        -DarchetypeVersion='1.0.0-SNAPSHOT' \
        -DgroupId='<your-group-id>' \
        -DartifactId='<your-artifact-id>' \
        -Dversion='<your-version>' \
        -Dpackage='<package-name>'`
    ```

    1.  `<your-group-id>` is a placeholder for your group ID
    2.  `<your-artifact-id>` is a placeholder for your artefact ID
    3.  `<your-version>` is a placeholder for your version
    4.  `<package-name>` is a placeholder for the root package name and structure. It should start with your `groupdId` and continue with the name of the root package.
    > For example, using `-DgroupId=com.test` and `-Dpackage=com.test.stacks` will instruct Maven to place the code in `src/main/java/com/test/stacks` and update all the relevant references accordingly (i.e. `imports`)
6.  Go to the `pom.xml` file of the project you'll be using this module in and add it as a [dependency](#use-it-as-a-dependency)

**Example**: Using `-DgroupId=com.test` and `-Dpackage=com.test.stacks` will instruct Maven to place the code in `src/main/java/com/test/stacks` and update all the relevant references accordingly (i.e. `imports`)

> **If you previously had used this module under different namespace (i.e. the default `com.amido.stacks.core-cqrs`):**
>
> Maven ONLY updates the imports for the module you generated. Any references in other projects will remain to the previous namespace.
>
> You will need to
>
>-  Update them manually
>-  Re-create the relevant `import` statements to use the new-made module instead
>-  If you plan to use this with Amido Stacks, include your namespace in the `@ComponentScan` annotation of the `Application` class.