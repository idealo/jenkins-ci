# Jenkins-CI for Data Science Projects

Minimal example to setup a Jenkins-CI pipeline for data science projects on OpenShift in a couple of minutes. The goal is to have one CI/CI for each project so that we have no snowflakes.

## Getting Started

0. Start [Minishift](https://github.com/minishift/minishift) with [VirtualBox](https://www.virtualbox.org/): `minishift start --vm-driver=virtualbox`
1. Create a new project:
```
oc new-project <project-name>
```
2. Deploy Jenkins:
```
oc new-app jenkins-persistent -p MEMORY_LIMIT="2Gi"
```
3. Add custom Jenkins configuration for data science projects:
```
oc create -f config-map.yaml
```
4. Deploy example application and expose route:
```
oc new-app https://github.com/idealo/ds-example-project.git \
--strategy=docker \
--name=ds-example-project
```
* Note: Don't forget to expose the route of the application: `oc expose svc/ds-example-project`
4. Log into Jenkins and run your pipeline!

## Requirements

- Minishift 1.17 / OpenShift 3.9
- VirutalBox 5.2

## Copyright

See [LICENSE](LICENSE) for details.