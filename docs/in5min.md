# Getting Started in 5 Minutes

The cluster.tools core is a _cloud_ orchestration tool for Lambda and ETL functions. The process called the **core** is responsible for orchestrating a distributed number of **processors**. 

The **processors** are responsible for the compute while the **core** handles resource management.

## Before We Begin

```shell
export PATH=$(go env GOPATH)/bin:$PATH
```

## Installation

```shell
# create a local copy of the threads
git clone https://github.com/GabeCordo/cluster-tools
go install
   
# add $(go env GOPATH)/bin to your environment PATH
   
# generate global files used by the threads when run
cluster-tools init
```

## Installing a Processor

```shell
# create a local copy of the threads
git clone https://github.com/GabeCordo/processor-framework
go install
   
# generate global files used by the threads when run
processor-framework init
```

## Running the Core

```shell
cluster-tools start
```

## Running the Processor

```shell
processor-framework connect http://localhost:8137
```

## Provision