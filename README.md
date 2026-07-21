# Gradle & Docker Pipeline (TeamCity Samples)

This is a sample Java project for TeamCity.

Tutorials that use this project:

* [TeamCity On-Premises](https://www.jetbrains.com/help/teamcity/configure-and-run-your-first-build.html)
* [TeamCity Cloud](https://www.jetbrains.com/help/teamcity/cloud/configure-and-run-your-first-build.html)


## Dependencies and Requirements

* Java 11
* SpringBoot 2.7.18
* Gradle 7.6.2
* JUnit Jupiter 5.7.0
* DockerHub connection (optional, to push built images)

## Overview

Versioned settings stored in the `.teamcity` folder generate a TeamCity project with five build configurations:

* **Build Application** — runs the Gradle step that builds this application.
* **Build Docker Image** — runs a custom script to build a Docker image using a Dockerfile from the `/docker` folder. Requires files produced by the "Build Application" configuration (see the note below).
* **Test Suite 1** and **Test Suite 2** — configurations that execute Gradle steps to run tests from `/test1` and `/test2` folders.
* **TestReport** — a [composite build configuration](https://www.jetbrains.com/help/teamcity/composite-build-configuration.html) that does not perform any building tasks and serves as an entry point to launch the entire build chain.

> NOTE: The **Build Docker Image** build configuration does NOT have required dependencies on **Build Application** to import required `todo.jar` and use it for building an image. These dependencies should be created manually to run the pipeline, see aforementioned tutorials for more details.

## Using Versioned Settings

The `.teamcity` folder stores project settings in the [Kotlin DSL](https://www.jetbrains.com/help/teamcity/kotlin-dsl.html) format. When you create a new project from this sample repository, TeamCity detects these settings and presents you with the following options:

![](https://github.com/JetBrains/Maven-Configuration-TeamCity-Samples/blob/master/tc-settings-import.png)

* Import settings — automatically configure the TeamCity project using remote settings. Settings are applied only once, allowing you to freely modify the project afterward.

* Import settings and enable synchornization — set up the TeamCity project with remote settings and establish two-way sync. Changes you make will be committed back to the VCS, and you can also edit the `.kts` file in the remote repo to modify the project.

* Do not import settings — start with a blank project targeting this repository.

Choose option #1 or option #3 depending on a tutorial. Some tutorials guide you to manually configure a blank project, while others recommend importing initial settings to kick-start your setup.

Opt for option #2 only if your project targets a forked sample and TeamCity has write permissions to it. Without these permissions, TeamCity won’t be able to push updates, causing the UI to lock and preventing further edits to the project.

## Other Samples

* [Simple Maven application](https://github.com/JetBrains/Maven-Configuration-TeamCity-Samples)
