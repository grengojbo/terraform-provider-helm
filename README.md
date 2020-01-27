Terraform Provider for Helm
[![Build Status](https://travis-ci.org/terraform-providers/terraform-provider-helm.svg?branch=master)](https://travis-ci.org/terraform-providers/terraform-provider-helm)
[![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/terraform-providers/terraform-provider-helm?label=release)](https://github.com/terraform-providers/terraform-provider-helm/releases)
[![license](https://img.shields.io/github/license/terraform-providers/terraform-provider-helm.svg)]()
===========================

This is a [Helm](https://github.com/kubernetes/helm) provider for [Terraform](https://www.terraform.io/).

The provider manages the installed [Charts](https://github.com/kubernetes/charts) in your Kubernetes cluster, in the same way of Helm does, through Terraform. It will also install Tiller automatically if it is not already present.

⚠️ Project Update
---

This provider currently only supports Helm 2. The next release of this project (`v1.0.0`) will be a major version bump bringing the upgrade to Helm 3. Helm 2 and tiller support will be removed in this release.

Users wishing to continue to use Helm 2 and tiller can continue to use the previous version (`v0.10.x`) of the provider. We will continue to accept bug fixes for `v0.10.x` of this provider as long as the Helm project continues to support Helm 2, after which Helm 2 support will be fully deprecated from this terraform provider.

Contents
--------

* [Developing the Provider](#developing-the-provider)
* [Example](#example)
* [Documentation](https://www.terraform.io/docs/providers/helm/index.html)
  * [Resource: helm_release](https://www.terraform.io/docs/providers/helm/release.html)
  * [Resource: helm_repository](https://www.terraform.io/docs/providers/helm/repository.html)


Developing the Provider
------------

### Installation from sources

If you wish to compile the provider from source code, you'll first need [Go](http://www.golang.org) installed on your machine (version >=1.9 is *required*). You'll also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `$GOPATH/bin` to your `$PATH`.

Clone repository to: `$GOPATH/src/github.com/terraform-providers/terraform-provider-helm`

```sh
> mkdir -p $GOPATH/src/github.com/terraform-providers
> git clone https://github.com/terraform-providers/terraform-provider-helm.git $GOPATH/src/github.com/terraform-providers/terraform-provider-helm
```

Enter the provider directory and build the provider

```sh
> cd $GOPATH/src/github.com/terraform-providers/terraform-provider-helm
> make build
```

Now copy the compiled binary to the Terraform's plugins folder, if is your first plugin maybe isn't present.

```sh
> mkdir -p ~/.terraform.d/plugins/
> mv terraform-provider-helm ~/.terraform.d/plugins/
```

Example
-------

This is a small example of how to install the mariadb chart on your default
kubernetes cluster, since the provider was initialized, all the configuration
is retrieved from the environment. Please read the [documentation](https://www.terraform.io/docs/providers/helm/index.html) for more
information.

You should have a local configured copy of kubectl.

```hcl
resource "helm_release" "my_database" {
    name      = "my-database"
    chart     = "stable/mariadb"

    set {
        name  = "mariadbUser"
        value = "foo"
    }

    set {
        name = "mariadbPassword"
        value = "qux"
    }

    set_string {
        name = "image.tags"
        value = "registry\\.io/terraform-provider-helm\\,example\\.io/terraform-provider-helm"
    }
}
```

License
-------

Mozilla Public License 2.0, see [LICENSE](LICENSE)
