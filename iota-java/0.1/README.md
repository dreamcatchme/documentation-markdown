# IOTA Java Library

This is the **official** Java library for the IOTA Core.
It's a simple Java wrapper around IOTA node’s [_JSON-REST HTTP interface_][iota-api]
and allows to connect to a _local_ or a _remote_ IOTA node easily using it's Java API interface.

[IOTA Java GitHub repository](https://github.com/iotaledger/iota-java).

The IOTA Java wrapper is designed to be **thread-safe** and kept as simple as possible in order to be **easily maintainable**, accordingly with the ongoing natural evolution of IOTA’s API.
All the boilerplate code for connecting to the node REST interface has been hidden as implementation detail (using Retrofit 2) — you'll only interact with **pure Java**.

## Table of Contents

- [IOTA Java Library](#iota-java-library)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
    - [Gradle Dependency](#gradle-dependency)
    - [Maven Dependency](#maven-dependency)
    - [Manual](#manual)
        - [Linking library](#linking-library)
        - [Linking jar](#linking-jar)
  - [Documentation](#documentation)
    - [Getting Started](#getting-started)
    - [Threading](#threading)
    - [Javadoc](#javadoc)
    - [API](#api)
      - [**`IotaAPI`**](#iotaapi)
      - [**`IotaUnitConverter`**](#iotaunitconverter)
      - [**`Checksum`**](#checksum)
      - [**`InputValidator`**](#inputvalidator)
      - [**`Transaction`**](#transaction)
      - [**`Converter`**](#converter)
      - [**`Signing`**](#signing)
      - [**`Multisig`**](#multisig)
    - [Examples](#examples)
  - [Technologies & dependencies](#technologies--dependencies)
    - [Dependencies:](#dependencies)
  - [Changes:](#changes)
  - [Warning / Disclaimer](#warning--disclaimer)
  - [Supporting the project](#supporting-the-project)
    - [Join the Discussion](#join-the-discussion)

## Installation

The IOTA Java library is available on [**jitpack.io**][jitpack].

### Gradle Dependency

To use the IOTA Java library in your Gradle build add this in your root `build.gradle` file (**not** your module `build.gradle` file):
```gradle
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```

Add this in your module `build.gradle` file:
```gradle
dependencies {
    compile 'com.github.iotaledger:iota-java:1.0.0-beta3'
}
```

### Maven Dependency

To use the IOTA Java library in your Maven build add this to your root `pom.xml` file:
```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```

Add this in your module `pom.xml` file:
```xml
<dependency>
    <groupId>com.github.iotaledger.iota-java</groupId>
    <artifactId>jota</artifactId>
    <classifier>jar-with-dependencies</classifier>
    <version>[VERSION_INFORMATION]</version>
</dependency>
```
For the [VERSION_INFORMATION], you can choose to set it to a release number, or the first 10 characters of a commit hash.
`<version>a98de8ea50</version>` or `<version>1.0.0-beta3</version>`
Or check it out at [Jitpack](https://jitpack.io/#iotaledger/iota-java) for more specific information

### Manual

To use the IOTA Java library by building the library yourself, the following steps can be used.

##### Linking library
Clone or download the project and import it into your favorite IDE. This will result in two projects; `jota` and `jota-parent`.
Reference your new project to the "jota" project.

##### Linking jar
In order to build the jar; the following command should be run on the "jota" project:
'mvn clean install'

This will generate a jar with the following format: `jota-[VERSION]-jar-with-dependencies.jar`


## Documentation

It should be noted that this is a temporary home for the official documentation. We are currently transitioning to a new developer hub, where we will have a dedicated website for the API documentation with concrete examples. The below documentation should be sufficient in enabling you to get started in the meantime.

### Getting Started

After you've successfully installed the library dependency, it is fairly easy to get started by simply creating a new **`IotaAPI` instance** using the `IotaAPI.Builder`.

Connecting to your device's _local node_ with the _default settings_ and fetching the node info is quite straightforward:

```java
IotaAPI api = new IotaAPI.Builder().build();
GetNodeInfoResponse response = api.getNodeInfo();
```

It doesn't get much more complicated if you need to connect to a _remote node_:

```java
IotaAPI api = new IotaAPI.Builder()
        .protocol("http")
        .host("somewhere_over_the_rainbow")
        .port("14265")
        .build();
GetNodeInfoResponse response = api.getNodeInfo();
```

In order to separate your node configuration from the implementation, you can also specify node configuration using a [**Java `.properties` file**](https://en.wikipedia.org/wiki/.properties) or command line properties which is very useful if you develop an open-source app which is deployed on a CI and don't want contributors to see the internal node configuration:

```java
iota.node.protocol=http
iota.node.host=127.0.0.1
iota.node.port=14265
```

### Threading

It should be noted that most API calls are done **synchronously**.
What this means is that you have to call the API from a background or worker thread, **not** from the main or UI thread!

### Javadoc

A hosted version of the complete [**Javadoc**][javadoc] for the latest release can be found [**here**][javadoc].
If you think there's something missing in the Javadoc, submit an [issue][new-issue] or open a [pull request][new-pull-request].

### API

The IOTA Java library implements both the [**official API**][iota-api], as well as some newly proposed functionality (such as _signing_, _bundles_, _utilities_ and _conversion_).

A full list of all IOTA JSON-REST API commands currently supported by the IOTA Java library can be found in the [commands enum](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPICommands.html#enum.constant.summary).

Here are some of the most commonly used API functions. Each list item below links to its corresponding [**Javadoc**][javadoc] where you can find _method signatures_, _preconditions_, _side-effects_ and _invariants_.

#### [**`IotaAPI`**](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html)

- [`getTransactionsObjects()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getTransactionsObjects-java.lang.String:A-)
- [`findTransactionObjects()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#findTransactionObjects-java.lang.String:A-) - [`getTransactionsObjects()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getTransactionsObjects-java.lang.String:A-)
- [`getLatestInclusion()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getLatestInclusion-java.lang.String:A-)
- [`broadcastAndStore()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#broadcastAndStore-java.lang.String...-)
- [`getNewAddress()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getNewAddress-java.lang.String-int-int-boolean-int-boolean-)
- [`getInputs()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getInputs-java.lang.String-int-int-int-long-)
- [`prepareTransfers()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#prepareTransfers-java.lang.String-int-java.util.List-java.lang.String-java.util.List-boolean-)
- [`sendTrytes()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#sendTrytes-java.lang.String:A-int-int-)
- [`sendTransfer()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#sendTransfer-java.lang.String-int-int-int-java.util.List-jota.model.Input:A-java.lang.String-)
- [`replayBundle()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#replayBundle-java.lang.String-int-int-)
- [`getBundle()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getBundle-java.lang.String-)
- [`getTransfers()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getTransfers-java.lang.String-int-java.lang.Integer-java.lang.Integer-java.lang.Boolean-)
- [`initiateTransfer()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#initiateTransfer-int-java.lang.String-java.lang.String-java.util.List-boolean-)
- [`getAccountData()`](https://iotaledger.github.io/iota-java/javadoc/jota/IotaAPI.html#getAccountData-java.lang.String-int-int-boolean-int-boolean-int-int-boolean-long-)

#### [**`IotaUnitConverter`**](https://iotaledger.github.io/iota-java/javadoc/jota/utils/IotaUnitConverter.html)

- [`convertUnits()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/IotaUnitConverter.html#convertUnits-long-jota.utils.IotaUnits-jota.utils.IotaUnits-)

#### [**`Checksum`**](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Checksum.html)

- [`addChecksum()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Checksum.html#addChecksum-java.lang.String-)
- [`removeChecksum()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Checksum.html#removeChecksum-java.lang.String-)
- [`isValidChecksum()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Checksum.html#isValidChecksum-java.lang.String-)

#### [**`InputValidator`**](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html)
- [`checkAddress()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#checkAddress-java.lang.String-)
- [`isAddress()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isAddress-java.lang.String-)
- [`isArrayOfHashes()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isArrayOfHashes-java.lang.String:A-)
- [`isArrayOfTrytes()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isArrayOfTrytes-java.lang.String:A-)
- [`inNinesTrytes()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isNinesTrytes-java.lang.String-int-)
- [`isTransfersCollectionValid()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isTransfersCollectionValid-java.util.List-)
- [`isTrytes()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isTrytes-java.lang.String-int-)
- [`isValidSeed()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isValidSeed-java.lang.String-)
- [`isValidTransfer()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isValidTransfer-jota.model.Transfer-)
- [`isValue()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/InputValidator.html#isValue-java.lang.String-)

#### [**`Transaction`**](https://iotaledger.github.io/iota-java/javadoc/jota/model/Transaction.html)

- [`toTrytes()`](https://iotaledger.github.io/iota-java/javadoc/jota/model/Transaction.html#toTrytes--)

#### [**`Converter`**](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Converter.html)

- [`trytes()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Converter.html#trytes-int:A-int-int-)
- [`trits()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Converter.html#trits-java.lang.String-int-)

#### [**`Signing`**](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Signing.html)

- [`validateSignatures()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Signing.html#validateSignatures-jota.model.Bundle-java.lang.String-)

#### [**`Multisig`**](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Multisig.html)

- [`getKey()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Multisig.html#getKey-java.lang.String-int-int-)
- [`getDigest()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Multisig.html#getDigest-java.lang.String-int-int-)
- [`finalizeAddress()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Multisig.html#finalizeAddress-java.lang.String-)
- [`validateAddress()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Multisig.html#validateAddress-java.lang.String-int:A:A-)
- [`addSignature()`](https://iotaledger.github.io/iota-java/javadoc/jota/utils/Multisig.html#addSignature-jota.model.Bundle-java.lang.String-java.lang.String-)

### Examples

There's an extensive list of **test cases** on the [`src/test/java` directory][tests] that can be used as reference when developing apps with IOTA.
A good starter is the [`IotaAPITest` case](https://github.com/iotaledger/iota-java/blob/master/jota/src/test/java/jota/IotaAPITest.java).

## Technologies & dependencies

The IOTA Java library has been designed to be used with **Java 6** or higher, in order to promote full **compatibility with Android**.

### Dependencies:

The following third party library dependencies and versions are used by the IOTA Java library internally:

- [Retrofit 2](https://square.github.io/retrofit/) type-safe HTTP client: `2.3.0`
- [Simple Logging Facade for Java](http://www.slf4j.org/): `1.7.25`
- [Apache Commons Lang](http://commons.apache.org/proper/commons-lang/): `3.6`
- [Apache Commons IO](http://commons.apache.org/proper/commons-io/): `2.5`
- [Legion of the Bouncy Castle](https://www.bouncycastle.org/java.html) Java cryptography APIs: `1.58`

## Changes:
- Changes in [**1.0.0-beta3**](https://github.com/iotaledger/iota-java/compare/1.0.0-beta2...1.0.0-beta3)
- Changes in [**1.0.0-beta2**](https://github.com/iotaledger/iota-java/compare/1.0.0-beta1...1.0.0-beta2)
- Changes in [**1.0.0-beta1**](https://github.com/iotaledger/iota-java/compare/0.9.10...1.0.0-beta1)
- Changes in [**v0.9.10**](https://github.com/iotaledger/iota-java/compare/v0.9.6...0.9.10)
- Changes in [**v0.9.6**](https://github.com/iotaledger/iota-java/compare/v0.9.5...v0.9.6)
- Changes in [**v0.9.5**](https://github.com/iotaledger/iota-java/compare/v0.9.4...v0.9.5)
- Changes in [**v0.9.4**](https://github.com/iotaledger/iota-java/compare/v0.9.3...v0.9.4)
- Changes in [**v0.9.3**](https://github.com/iotaledger/iota-java/compare/v0.9.2...v0.9.3)
- Changes in [**v0.9.2**](https://github.com/iotaledger/iota-java/compare/v0.9.1...v0.9.2)
- Changes in [**v0.9.1**](https://github.com/iotaledger/iota-java/commits/v0.9.1)

## Warning / Disclaimer

- This is _pre-release_ software!
- There may be _performance and stability issues_.
- You may loose all your money :)
- Please report any issues using our [**issue tracker**][issues].

## Supporting the project

If the IOTA Java library has been useful to you and you feel like contributing, consider posting a [**bug report**][new-issue], [**feature request**][new-issue] or a [**pull request**][new-pull-request].  
We have some [basic contribution guidelines][contribution-guidelines] to keep our code base stable and consistent.

### Join the Discussion

If you want to get involved in the community, need help with getting setup, have any issues related with the library or just want to discuss Blockchain, Distributed Ledgers and IoT with other people, feel free to join our [**Discord**][iota-discord].  
You can also ask questions on our dedicated [**IOTA Forum**][iota-forum].