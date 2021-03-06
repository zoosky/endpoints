# Installation

## Project layout

Typically, your project will be broken down into several sub-projects:

~~~ mermaid
graph BT
  endpoints
  server -.-> endpoints
  client -.-> endpoints
~~~

The `endpoints` sub-project contains the *description* of the communication
protocol. The `server` sub-project *implements* this communication protocol.
The `client` sub-project *uses* the protocol to communicate with the `server`.

This translates to the following sbt configuration:

~~~ scala
val endpoints = project

val client = project.dependsOn(endpoints)

val server = project.dependsOn(endpoints)
~~~

## Dependencies

All the artifacts are published on maven central under the organization
name `org.julienrf`.

### Endpoint descriptions

Add the following dependencies to your `endpoints` sub-project:

~~~ scala expandVars=true
libraryDependencies ++= Seq(
  // core API
  "org.julienrf" %% "endpoints-algebra" % "{{version}}",
  // (optional) JSON serialization using circe.io
  "org.julienrf" %% "endpoints-algebra-circe" % "{{version}}"
)
~~~

### Client interpreters

#### Client based on Play framework (JVM only)

Add the following dependencies to your `client` sub-project:

~~~ scala expandVars=true
libraryDependencies ++= Seq(
  // client based on Play framework
  "org.julienrf" %% "endpoints-play-client" % "{{version}}",
  // JSON serialization using circe.io
  "org.julienrf" %% "endpoints-play-client-circe" % "{{version}}"
)
~~~

#### Scala.js client using native `XMLHttpRequest`s

Add the following dependencies to your `client` sub-project:

~~~ scala expandVars=true
  // client based on JavaScript’s XMLHttpRequest
  "org.julienrf" %% "endpoints-xhr-client" % "{{version}}",
  // (optional) JSON serialization using circe.io
  "org.julienrf" %% "endpoints-xhr-client-circe" % "{{version}}"
  // (optional) uses faithful’s `Future`
  "org.julienrf" %% "endpoints-xhr-faithful" % "{{version}}"
)
~~~

### Server interpreters

#### Server based on Play framework

Add the following dependencies to your `server` sub-project:

~~~ scala expandVars=true
libraryDependencies ++= Seq(
  // server based on play framework
  "org.julienrf" %% "endpoints-play-server" % "{{version}}",
  // (optional) JSON serialization using circe.io
  "org.julienrf" %% "endpoints-play-server-circe" % "{{version}}"
)
~~~
