# Jenkins-CI for Data Science Projects

Minimal example to setup a Jenkins-CI pipeline for data science projects on OpenShift in a couple of minutes. The goal is to have one CI/CI for each project so that we have no snowflakes.

## Getting Started

0. Start [Minishift](https://github.com/minishift/minishift) with [VirtualBox](https://www.virtualbox.org/): `minishift start --vm-driver=virtualbox`
1. Create a new project: `oc new-project data-science-ci`
2. Deploy Jenkins:
```
oc process -f jenkins-ephemeral-template.yml \
-p NAMESPACE="data-science-ci" \
-p KUBERNETES_MASTER="https://kubernetes.default:443" | oc create -f -
```
- Note: to get the Kubernetes master url do `oc version` and take the server url. In case of minishift, the url is fixed at `https://192.168.99.100:port` - remember `port`for Kubernetes is at 443
3. Deploy example application and expose route:
```
oc new-app https://github.com/idealo/ds-example-project.git \
--strategy=docker \
--name=ds-example-project
```
* Note: Don't forget to expose the route of the application: `oc expose svc/ds-example-project`
4. Log into Jenkins and run your pipeline!

## Requirements

- Minishift 1.14
- VirutalBox 5.2

## Copyright

See [LICENSE](LICENSE) for details.