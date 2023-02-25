# green_digletto

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/green_digletto-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Related Guides

- Quarkus Extension for Spring Web API ([guide](https://quarkus.io/guides/spring-web)): Use Spring Web annotations to create your REST services

## Provided Code

### Spring Web

Spring, the Quarkus way! Start your RESTful Web Services with a Spring Controller.

[Related guide section...](https://quarkus.io/guides/spring-web#greetingcontroller)

## Docker

To create docker image, first of all execute
```shell script
quarkus extension add 'container-image-docker'
```

This should add following dependency to the pom.xml
```xml
    <dependency>
      <groupId>io.quarkus</groupId>
      <artifactId>quarkus-container-image-docker</artifactId>
    </dependency>
```

Remember to actually build appliation with:
```shell
./mvnw package
```

Now it is possible to simply build docker images using provided Dockerfiles (in /src/main/docker) with:

```shell
docker buildx build -t green_digletto:latest -f ./src/main/docker/Dockerfile.jvm .
```

And then just run container with
```shell
docker run -d --name green_digletto -p 127.0.0.0:8080:8080 green_digletto:latest
```

Test if everything is right with simple curl:
```shell
curl 127.0.0.0:8080/greeting 
Hello Spring%                                                
```

TODO: what builds when no file specified during building?
TODO: other build engines?
TODO: other containers?

Sources:
https://docs.docker.com/engine/reference/commandline/buildx/
https://docs.docker.com/build/buildkit/