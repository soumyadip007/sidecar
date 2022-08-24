# spaship-sidecar

This is a very lightweight Java application which 
* Reads configuration from .spaship file 
* Creates or update SPAs in http server
* Removes SPA directory fom http server
* Schedule SSI Sync

Every SPAship environment contains this sidecar container.

## Documentation

For more details on operator follow the [SPAship architecture document](https://spaship.io#sidecar)


## Configurable Properties
| Name | Description | Default value
| --- | ----------- | ----------- |
| sidecar.spadir | Parent directory where it will unpack the spas based on mapping, this must be linked with Apache2 or HTTPD  DocumentRoot directory| /app/data|
| sidecar.websitename | For kubernetes deployment every sidecar container must be associated with an website | website|
| sidecar.environmentname | Environment identifier of the sidecar container | dev|
| sidecar.website.version | Side car version, this is an optional property |v1 |
| sidecar.root.dir.identifier | this char in spaship mapping denotes the root directory |. |
| spaship.mapping.file | The name of the mapping file that contains spaship mapping | .spaship|
| curl.nocache.param | Cache-Control header  | -H~'Cache-Control: no-cache, no-store'|
| curl.proxy.param | proxy arguement for cul command | --proxy~http://squid.corp.redhat.com:3128|
| curl.command.debug | debugging the output of curl command | true|


## Running the application in dev mode

You can run your application in dev mode that enables live coding using:

```shell script
./mvnw compile quarkus:dev
```


## Packaging and running the application

The application can be packaged using:

```shell script
./mvnw package
```

It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory. Be aware that it’s not an _über-jar_ as
the dependencies are copied into the `target/quarkus-app/lib/` directory.

If you want to build an _über-jar_, execute the following command:

```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

## Creating a native executable

You can create a native executable using:

```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using:

```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/spaship-sidecar-1.0.0-SNAPSHOT-runner`

