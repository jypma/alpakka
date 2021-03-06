# MQTT Connector

The MQTT connector provides Akka Stream sources to connect to AMQP servers.

## Artifacts

sbt
:   @@@vars
    ```scala
    libraryDependencies += "com.typesafe.akka" %% "akka-stream-alpakka-mqtt" % "$version$"
    ```
    @@@

Maven
:   @@@vars
    ```xml
    <dependency>
      <groupId>com.typesafe.akka</groupId>
      <artifactId>akka-stream-alpakka-mqtt_$scala.binaryVersion$</artifactId>
      <version>$version$</version>
    </dependency>
    ```
    @@@

Gradle
:   @@@vars
    ```gradle
    dependencies {
      compile group: "com.typesafe.akka", name: "akka-stream-alpakka-mqtt_$scala.binaryVersion$", version: "$version$"
    }
    ```
    @@@

## Usage

First we need to define various settings, that are required when connecting to an MQTT server.

Scala
: @@snip (../../../../mqtt/src/test/scala/akka/stream/alpakka/mqtt/scaladsl/MqttSourceSpec.scala) { #create-settings }

Java
: @@snip (../../../../mqtt/src/test/java/akka/stream/alpakka/mqtt/javadsl/MqttSourceTest.java) { #create-settings }

Here we used @scaladoc[MqttSourceSettings](akka.stream.alpakka.mqtt.MqttSourceSettings$) factory to set the address of the server, client ID, which needs to be unique for every client, and client persistence implementation (@extref[MemoryPersistence](paho-api:org/eclipse/paho/client/mqttv3/persist/MemoryPersistence)) which allows to control reliability guarantees.

Then let's create a source that is going to connect to the MQTT server upon materialization and receive messages that are sent to the subscribed topics.

Scala
: @@snip (../../../../mqtt/src/test/scala/akka/stream/alpakka/mqtt/scaladsl/MqttSourceSpec.scala) { #create-source }

Java
: @@snip (../../../../mqtt/src/test/java/akka/stream/alpakka/mqtt/javadsl/MqttSourceTest.java) { #create-source }

And finally run the source.

Scala
: @@snip (../../../../mqtt/src/test/scala/akka/stream/alpakka/mqtt/scaladsl/MqttSourceSpec.scala) { #run-source }

Java
: @@snip (../../../../mqtt/src/test/java/akka/stream/alpakka/mqtt/javadsl/MqttSourceTest.java) { #run-source }

This source has a materialized value (@scaladoc[Future](scala.concurrent.Future) in Scala API and @extref[CompletionStage](java-api:java/util/concurrent/CompletionStage) in Java API) which is completed when the subscription to the MQTT broker has been completed.

### Running the example code

The code in this guide is part of runnable tests of this project. You are welcome to edit the code and run it in sbt.

Scala
:   ```
    sbt
    > mqtt/testOnly *.MqttSourceSpec
    ```

Java
:   ```
    sbt
    > mqtt/testOnly *.MqttSourceTest
    ```
