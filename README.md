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
oc new-app jenkins-persistent
```
3. Add custom Jenkins configuration for data science projects:
```
oc create -f config-map.yaml
```
4. Deploy [example application](https://github.com/idealo/ds-example-project) and expose route:
```
git clone https://github.com/idealo/ds-example-project.git
cd ds-example-project
oc new-app -f build-config.yml \
    -p APPLICATION_NAME=ds-example-project \
    -p GIT_URL=https://github.com/idealo/ds-example-project.git
oc new-app -f deployment-config.yml \
    -p APPLICATION_NAME=ds-example-project
oc start-build ds-example-project-pipeline
oc expose svc/ds-example-project
```
#### Notes

If you want to delete Jenkins and all the related resources then do:
```
oc delete all,configmaps,networkpolicy,rolebinding,serviceaccount -l app=jenkins-persistent
```

## Requirements

- Minishift 1.17 / OpenShift 3.9
- VirutalBox 5.2

## Copyright

See [LICENSE](LICENSE) for details.