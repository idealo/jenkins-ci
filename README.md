# Jenkins-CI for Data Science Projects

Minimal example to setup a Jenkins-CI pipeline for data science projects on OpenShift in a couple of minutes. The goal is to have one CI/CI for each project so that we have no snowflakes.

## Getting Started

1. Create a new project: `oc new-project data-science-ci`
2. Log into project: `oc project data-science-ci`
3. Add Jenkins-CI image: `oc new-build git@github.com:idealo/ds-example-project.git`
* Note: wait until image is built on OpenShift
4. Deploy Jenkins:
```
oc process -f jenkins-ephemeral-template.json \
-p NAMESPACE="data-science-ci" \
-p JENKINS_IMAGE_STREAM_TAG="jenkins-ci:latest" | oc create -f -
```
5. Deploy example application and expose route:
```
oc new-app git@github.com:idealo/ds-example-project.git \
--strategy=docker \
--name=ds-example-project
```
* Note: Don't forget to expose the route of the application: `oc expose svc/ds-example-project`
6. Log into Jenkins and run your pipeline!

## Copyright

See [LICENSE](LICENSE) for details.