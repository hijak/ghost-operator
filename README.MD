# Ghost Operator

A kubernetes operator for ghost blog [Ghost](https://github.com/TryGhost)

## Summary

  - [Getting Started](#getting-started)
  - [Deployment](#deployment)
  - [Built With](#built-with)
  - [Authors](#authors)
  - [License](#license)
  - [Acknowledgments](#acknowledgments)

## Getting Started

After installing edit `examples/ghost.yml` to fit your requirements 

```yaml
apiVersion: apps.exnet.systems/v1alpha1
kind: Ghost
metadata:
  name: ghost-sample # name used in resources
  namespace: default
spec:
  size: 1 # replica size you will have to choose a rwx storage class if you want replicas
  hostname: example.com # url env and ingress hostname
  container_tag: 3-alpine # ghost container tags
  storageclass: local-path # pvc storage class
  storageclass_accessmode: rwo # rwo or rwx
  storagesize: 2Gi # storage class size for /var/lib/ghost/content mount
  certmanager_issuer: letsencrypt-issuer # Clusterissuer for letsencrypt
```

### Prerequisites

This assumes you have a working ingress, a storage class avaialble for pvc and a working cert-manager install

Kubernetes version at least 1.17

### Installing

Create the custom resource definitions:
```
kubectl apply -f examples/01-crd.yml
```

And deploy the ghost operator
```
kubectl apply -f examples/02-deploy.yml
```

## Deployment

The operator will create the following resources:
  * deployment
  * service
  * pvc
  * ingress

## Built With

  - [Contributor Covenant](https://www.contributor-covenant.org/) - Used
    for the Code of Conduct
  - [Creative Commons](https://creativecommons.org/) - Used to choose
    the license
  - [Operator SDK Framework](https://sdk.operatorframework.io/) - Used to
    generate the operator via ansible

## Authors

  - **Jack Cowey** -
    [HiJak](https://github.com/hijak)

See also the list of
[contributors](https://github.com/hijak/ghost-operator/contributors)
who participated in this project.

## License

This project is licensed under the [CC0 1.0 Universal](LICENSE.md)
Creative Commons License - see the [LICENSE.md](LICENSE.md) file for
details

## Acknowledgments

  - [Operator SDK Framework](https://sdk.operatorframework.io/)
  - [Ansible](https://www.ansible.com)
