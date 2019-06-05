# CI build Docker: Vuepress

CI Docker image for performing Markdown to HTML rendering based upon project [Vuepress](https://vuepress.vuejs.org/).

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

In order to develop / test, you need the following tools installed:

* [Docker](https://docs.docker.com/docker-for-mac/install/)
* [GNU Make](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/) 3.8 or higher

## Built With

* Docker

### Build Docker

~~~bash
# Build the Docker locally
#  -- see output how to run this Docker on your machine
$ make image

# Push Docker to the Docker Registry
$ make push
~~~

## Deployment

Use the Docker image in your CI tooling, an examples for have been provided below.

### CircleCI

Just copy the YAML into your build definition:

~~~yaml
# Build and verify the generated HTML
  build:
    docker:
      - image: rdclda/ci-vuepress:latest
    working_directory: ~/my-project
    steps:
      # Checkout the repository
      - checkout

      # Build with Vuepress
      - run:
          name: Build the Vuepress static content
          command: vuepress build docs

      - persist_to_workspace:
          # Must be an absolute path, or relative path from working_directory
          root: ~/my-project
          # Must be relative path from root
          paths:
             - dist/

~~~

...and enable to validate step after the build phase in the overall flow:

~~~yaml
# Glue the jobs together
workflows:
  version: 2
  build_and_publish:
    jobs:
      - build
~~~

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/rdc-lda/fintech-blogs/tags).

## Authors

* **Robin Huiser** - *Initial work* - [robinhuiser](https://github.com/robinhuiser)

See also the list of [contributors](CONTRIBUTORS.md) who participated in this project.

## License

This project is licensed under the Apache License - see the [LICENSE](LICENSE) file for details
