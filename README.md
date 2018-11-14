# README

* `mkdir jhipster-microservice-template`
* `jhipster-microservice-template`

## Top level project

* `git flow init --default`
* `gradle wrapper`
* `mkdir consumer`
* `mkdir producer`

**settings.gradle**:

```gradle
rootProject.name = 'microservice-app'
include 'consumer'
include 'producer'
```

**build.gradle**:

```gradle
project(':consumer')
project(':producer')
```

## Producer subproject

**producer.jdl**:

```jdl
application {
  config {
    applicationType microservice,
    baseName producerApp,
    packageName de.infinitservices.forge.serviceplatform.producer,
    enableTranslation false,
    serverPort 8081,
    buildTool gradle,
    skipClient true
  }
}
```

`jhipster import-jdl producer-app.jdl`

**producer-model.jdl**:

```jdl
entity Producer {}
```

`jhipster import-jdl producer-domain-model.jdl`

> Since subprojects are not supposed to be run by themselves, they should not redefine the wrapper task. See [here](https://github.com/gradle/gradle/issues/5816).

**build.gradle**:

```gradle
// wrapper {
//     gradleVersion = '4.10.2'
// }
```

## Consumer subproject

**consumer.jdl**:

```jdl
application {
  config {
    applicationType microservice,
    baseName consumerApp,
    packageName de.infinitservices.forge.serviceplatform.consumer,
    databaseType no,
    cacheProvider no,
    enableHibernateCache false
    enableTranslation false,
    serverPort 8082,
    buildTool gradle,
    skipClient true
  }
}
```

`jhipster import-jdl consumer-app.jdl`

**build.gradle**:

```gradle

dependencies {
  ...
  compile project(':producer')
}
...
// wrapper {
//     gradleVersion = '4.10.2'
// }
```

## Build

`gradlew`
