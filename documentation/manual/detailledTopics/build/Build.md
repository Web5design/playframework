# The Build System

The Play build system is based on [sbt](http://www.scala-sbt.org/), a minimally non-intrusive build tool for Scala and Java projects.

## The `/project` directory

All the build configuration is stored in the `project` directory. This folder contains 3 main files:

- `build.properties`: This is a marker file that describes the sbt version used.
- `Build.scala`: This is the application project build description.
- `plugins.sbt`: SBT plugins used by the project build.

> Note that `build.properties` and `plugins.sbt` have to be manually updated when you are changing the play version.

## Default build for a Play application

The default build description generated by the `play new` command looks like this:

```scala
import sbt._
import Keys._
import play.Project._

object ApplicationBuild extends Build {

  val appName         = "Your application"
  val appVersion      = "1.0"

  val appDependencies = Seq(
    // Add your project dependencies here,
  )

  val main = play.Project(appName, appVersion, appDependencies).settings(
    // Add your own project settings here      
  )

}
```

It is written this way to make it easy to define standard options like application name, version and dependencies. 

> Note that every sbt feature is available in a Play project. 

## Play plugin for sbt

The Play console and all development features like live reloading are implemented via an sbt plugin. It is registered in the `plugins.sbt` file:

```scala
addSbtPlugin("play" % "sbt-plugin" % "2.1.1")
```

You might need to add the Typesafe repository in your list of resolvers, see: [[Repositories]]

## Adding dependencies and resolvers

Adding dependencies is simple:

```scala
val appDependencies = Seq(
  "group" % "name" % "version number",
)
```

So is adding resolvers:

```scala
val main = play.Project(
  appName, appVersion, appDependencies).settings(
  // Add custom repository: 
  resolvers += "Repository name" at "http://url.to/repository" 
)
```



> **Next:** [[About SBT Settings | SBTSettings]]
