<!-- markdownlint-disable MD033 -->
<h1>
    <img src="https://github.com/sighupio/fury-distribution/blob/main/docs/assets/fury-epta-white.png?raw=true" align="left" width="90" style="margin-right: 15px"/>
    Kubernetes Fury vSphere
</h1>
<!-- markdownlint-enable MD033 -->

![Release](https://img.shields.io/badge/Latest%20Release-v1.1.0-blue)
![License](https://img.shields.io/github/license/sighupio/fury-kubernetes-vsphere?label=License)
![Slack](https://img.shields.io/badge/slack-@kubernetes/fury-yellow.svg?logo=slack&label=Slack)

<!-- <KFD-DOCS> -->

**Kubernetes Fury vSphere** is an add-on module for the [Kubernetes Fury Distribution (KFD)][kfd-repo] that provides
packages to integrate vSphere with Kubernetes.

If you are new to KFD please refer to the [official documentation][kfd-docs] on how to get started with KFD.

## Overview

**Kubernetes Fury vSphere** uses a collection of open source tools to install Kubernetes in an vSphere environment.

## Packages

The following packages are included in the Fury Kubernetes vSphere module:

| Package                                        | Version  | Description                                                                   |
| ---------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| [vsphere-cm](katalog/vsphere-cm)               | `1.27.0` | Kubernetes Cloud Provider for vSphere                                         |
| [vsphere-csi](katalog/vsphere-csi)             | `3.1.2`  | vSphere storage Container Storage Interface (CSI) plugin                      |

Click on each package to see its full documentation.

## Compatibility

Check the [compatibility matrix][compatibility-matrix] for additional information about the compatibility of the module.

## Usage

### Prerequisites

| Tool                    | Version   | Description                                                                                                                                                |
| ----------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [furyctl][furyctl-repo] | `>=0.25.0` | The recommended tool to download and manage KFD modules and their packages. To learn more about `furyctl` read the [official documentation][furyctl-repo]. |

### Download the packages

List the bases in a `Furyfile.yml` file

```yaml
bases:
  - name: vsphere
    version: v1.1.0
```

> See `furyctl` [documentation][furyctl-repo] for additional details about `Furyfile.yml` format.

1. Execute `furyctl legacy vendor -H` to download the katalog

2. Inspect the downloaded katalog inside `./vendor/katalog/vsphere`

3. Check each package documentation for the configuration with vSphere

<!-- Links -->

[furyctl-repo]: https://github.com/sighupio/furyctl
[compatibility-matrix]: https://github.com/sighupio/fury-kubernetes-vsphere/blob/master/docs/COMPATIBILITY_MATRIX.md
[kfd-repo]: https://github.com/sighupio/fury-distribution
[kfd-docs]: https://docs.kubernetesfury.com/docs/distribution/

<!-- </KFD-DOCS> -->

<!-- <FOOTER> -->

### Reporting Issues

In case you experience any problems with the module, please [open a new issue](https://github.com/sighupio/fury-kubernetes-on-premises/issues/new/choose).

## License

This module is open-source and it's released under the following [LICENSE](LICENSE).

<!-- </FOOTER> -->
