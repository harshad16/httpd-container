# Apache HTTP Server Customized Container Images

[![Docker Repository on Quay](https://quay.io/repository/aicoe/s2i-httpd-tensorflow-index/status "Docker Repository on Quay")](https://quay.io/repository/aicoe/s2i-httpd-tensorflow-index)

This repository contains Dockerfiles for AICOE Tensorflow host Apache HTTP Server images for OpenShift and general usage.

## Versions

Apache HTTPD versions currently provided are:

- [httpd-2.4](2.4)

CentOS versions currently supported are:

- CentOS 7

## Deploy and Run httpd-aicoe-container

This repository has the Custom **assemble** script for performing additional requirements.

- Assemble script: Downloads wheel files from releases of AICoE/tensorflow-wheels repository and updates the index.html with list of wheel files.
- The Apache HTTP Server image is built with the centos7 Dockerfile and push to quay.io/aicoe repository.

Developer can deploy and run the httpd-aicoe-container Apache HTTP Server image for the AICoE/tensorflow-wheels respository using following commands:

1. Fetch the image from quay.io : `oc tag quay.io/aicoe/s2i-httpd-tensorflow-index:latest s2i-httpd-tensorflow-index:latest`
2. Start the application: `oc new-app s2i-httpd-tensorflow-index~https://github.com/AICoE/tensorflow-wheels.git` -this will start bc(assemble), dc(run).
3. Set the github token for assemble: `oc set env bc/tensorflow-wheels SESHETA_GITHUB_ACCESS_TOKEN=<provide your Github oauth token>`
4. Expose the route: `oc expose svc/tensorflow-wheels`

## Installation

- **CentOS7 based image**

  This image is available on DockerHub. To download it run:

  ```
   $ docker pull centos/httpd-24-centos7
  ```

  To build a CentOS based Apache HTTP Server image from scratch run:

  ```
   $ git clone --recursive https://github.com/sclorg/httpd-container.git
   $ cd httpd-container
   $ git submodule update --init
   $ make build TARGET=centos7 VERSIONS=2.4
  ```

For using other versions of Apache HTTP Server, just replace the `2.4` value by particular version in the commands above.

**Notice: By omitting the `VERSIONS` parameter, the build/test action will be performed on all provided versions of Apache HTTP Server, which must be specified in `VERSIONS` variable. This variable must be set to a list with possible versions (subdirectories).**

## Usage

For information about usage of Dockerfile for Apache HTTP Server 2.4, see [usage documentation](2.4).<br>
Please have look at [additional docs](docs)
