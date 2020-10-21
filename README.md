# cekit-custom-builder

This repository contains a Base Container Image to support a Custom Build Strategy on OCP 4 using CEKit and Buildah.

It is expected that you will use `buildah` to build the container image.

### Developing the Custom Build Container Image

If developing on a RHEL environment, you will find the `Dockerfile` for the Custom Builder Image in `/container`.
You can simply modify the `Dockerfile` and build it with `buildah bud -t cekit-custom-builder .`

#### If your local development environment is not RHEL

This repository additionally contains a Vagrant definition that will provision a RHEL 7 VM with `buildah` installed.
This will allow you to use the Vagrant VM as a RHEL 7 development environment. You will need to install:

* [Vagrant](https://vagrantup.com)
* [Ansible](https://ansible.com)

In addition you will require a hypervisor provider. The current configuration is in place for VirtualBox on Mac. Mac
users should install the latest version of [VirtualBox](https://virtualbox.org). 

Other O/S users should install a Vagrant supported provider and extend the `Vagrantfile` configuration accordingly.

#### Configuring Ansible to provision the Vagrant VM

There is a simple Ansible playbook in [ansible/main.yml](ansible/main.yml) that configures the RHEL 7 Guest. This playbook
will register the VM with subscription-manager and therefore requires you to put your credentials into `ansible/vars/subscription-manager.yml`.

Simply copy the `ansible/vars/subscription-manager.yml.example` to `ansible/vars/subscription-manager.yml` and provide a valid subscription.
You should *NOT* check the `subscription-manager.yml` containing your details into Git and the `.gitignore` file for this
repository is configured to explicitly ignore it.

#### Running the Vagrant VM

Use the following to start the Vagrant Guest:

```shell script
vagrant up
vagrant ssh
```

Once connected to the Vagrant Guest, you will find the `Dockerfile` mounted at `/containers/Dockerfile` and can therefore
use the following to build the image:

```shell script
cd /container
buildah build -t cekit-custom-builder .
```     

You can edit the `Dockerfile` from your local environment and then simply re-run the above command to ensure your changes
are valid.