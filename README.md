ITKDoxygen
==========

[![][doxygen-img]][doxygen-link] [![][deployment-img]][deployment-link]

[doxygen-img]: https://github.com/InsightSoftwareConsortium/ITKDoxygen/actions/workflows/Doxygen.yml/badge.svg
[doxygen-link]: https://github.com/InsightSoftwareConsortium/ITKDoxygen/actions/workflows/Doxygen.yml

[deployment-img]: https://github.com/InsightSoftwareConsortium/ITKDoxygen/actions/workflows/pages/pages-build-deployment/badge.svg
[deployment-link]: https://insightsoftwareconsortium.github.io/ITKDoxygen/

Overview
--------

This dockerfile has been created to facilitate the creation of
[ITK](https://github.com/InsightSoftwareConsortium/ITK)
[Doxygen](https://doxygen.nl/) documentation in a reproducible way.

The documentation is built nightly on the current/latest ITK commit, and
deployed to GitHub pages at:
https://insightsoftwareconsortium.github.io/ITKDoxygen/

To create the the documentation locally, run the following commands:

```shell
docker build --build-arg TAG=v1.1.0 . -f Dockerfile -t itk-doxygen
docker build -f Dockerfile -t itk-doxygen .

export TAG=v1.2.0
docker run --env TAG --name itk-dox itk-doxygen
```

or

```shell
docker run \
  --env TAG \
  --mount type=bind,source=!ITK,destination=/work/ITK,readonly \
  --name itk-dox itk-doxygen

docker cp itk-dox:/ITKDoxygen.tar.gz SimpleITKDoxygen${TAG:+-${TAG}}.tar.gz
docker cp itk-dox:/ITKDoxygenXML.tar.gz SimpleITKDoxygenXML${TAG:+-${TAG}}.tar.gz
docker rm itk-dox
```
