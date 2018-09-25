# Documentation

This is the documentation of the Personal Health Train.

## Architecture diagram
- [PHT.archimate](PHT.archimate) is the current view on the architecture, available online at [personalhealthtrain.github.io](https://personalhealthtrain.github.io/Documentation/).
- [PHT-original.archimate](PHT-original.archimate) is the collection of original PHT architecture diagrams, as discussed during the technical meeting in Leiden in April 2018.

## Live view of the architecture
The latest export of the architecture diagram is available at [personalhealthtrain.github.io](https://personalhealthtrain.github.io/Documentation/).

## General Information

- [PHT Tech Google Group](https://groups.google.com/a/go-fair.org/forum/#!forum/pht-tech)

### Working groups

- [PHT Architecture Working Group](https://groups.google.com/a/go-fair.org/forum/#!forum/pht-tech-architecture)
- [PHT Use Cases Working Group](https://groups.google.com/a/go-fair.org/forum/#!forum/pht-tech-usecases)
- [PHT Legal Working Group](https://groups.google.com/a/go-fair.org/forum/#!forum/pht-tech-legal)

## Contents

- [Use cases](https://github.com/PersonalHealthTrain/Documentation/wiki/Use-Cases)
    - A set of use cases highlighting key situations envisioned for the Personal Health Train



## Library
This is an overview of the PHT library components that were developed for the JVM.
This section describes all the repositories that are prefixed with `lib-`. as
these comprise all the components of the library.

### Overview
![PHT Library](https://github.com/PersonalHealthTrain/Documentation/blob/master/figures/lib.png?raw=true "PHT Library")

Each node in this image describes one Git repository.
With the version dependencies.
Note that the version describe the actual dependencies (see respective `build.gradle`), not necessarily the most
recent version of the artifact.

The green repository are part of the PHT Library
and can be found in the [Personal Health Train GitHub Organization](https://github.com/PersonalHealthTrain).

The orange repositories belong to the [JDregistry](https://github.com/jdregistry)
project, which aims to provide APIs for the [Docker Registry](https://docs.docker.com/registry/) for the JVM. The JDregistry project was retrospectively extracted from the PHT library,
as it can be developed on a larger scope.

The following table gives an overview of the green nodes for the PHT lib project:

Repository Name and URL                                     | Description
------------------------------------------------------------|-------------
[lib-data](https://github.com/PersonalHealthTrain/lib-data) | This is the root project of the library. It contains the data classes that form the basis of class interactions.
[lib-runtime](https://github.com/PersonalHealthTrain/lib-runtime) | The runtime interfaces. Currently, the `DockerRuntimeClient` interface specifies how a Docker client needs to be implemented to be used with the PHT library.
[lib-runtime-docker-spotify](https://github.com/PersonalHealthTrain/lib-runtime-docker-spotify) | This repo **implements** the `DockerRuntimeClient` interface using the JVM Docker client from [Spotify](https://github.com/spotify/docker-client).   |
[lib-api](https://github.com/PersonalHealthTrain/lib-api) | Contains the actual Train API classes. It provides the specification of the concepts **TrainArrival** and **TrainDeparture** and also the specification and default implementation of the default **TrainRegistry**.  |  

Note that the library talks about two different kind of clients that have
something to do with Docker. It is important to understand the distinction:

* The **Docker Registry client** (which is developed in the
  [JDregistry](https://github.com/jdregistry) project) is a consumer of the
  [Docker Registry V2 API](https://docs.docker.com/registry/spec/api).
  Such clients do not require a Docker daemon installed on the host system,
  as they only rely on HTTP networking.
* The client interface defined in the
  [lib-runtime](https://github.com/PersonalHealthTrain/lib-runtime) project
  defines **Docker Runtime clients**, which require a Docker host installed on the host
  system. These clients can run containers, pull images, commit new images, and
  push images to registries.

The clients overlap in their requirements. For instance, both need access to
authentication credentials. The Docker Registry clients needs those to list
repositories from certain namespaces. The Runtime Client need those to pull
images from these very namespaces.
