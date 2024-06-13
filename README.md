# hyperscaler-ee
## Execution environment configuration and sample playbooks for hyperscaler provisioning

Given a host running Ansible Automation Platform (AAP) Controller / Automation Hub, the default execution environment "ee-supported-rhelX:latest" includes provisioning and control modules for Amazon Web Services (AWS) resources. This execution environment, however, does not include support for Google Cloud Platform (GCP) or Microsoft Azure installed by default.

Minimal execution environments, ee-minimal-rhelX:latest, do not include support for any hyperscalers.

This configuration assumes that you have access to registry.redhat.io and have subsequently logged in prior to building your execution environment. The new execution environment is based off of the "ee-minimal-rhel9" execution environment.

To use this repo:

1. git clone https://github.com/redhatstuart/hyperscaler-ee
2. podman login registry.redhat.io
3. Customize execution-environment.yml (if necessary)
4. ansible-builder build -v3 -t hyperscaler-ee

After the new execution environment has been built, you can push this image to your Automation Hub and subsequently have your AAP controller ingest it.

5. podman tag localhost/hyperscaler-ee fqdn.of.your.automation.hub.com/hyperscaler-ee
6. podman push fqdn.of.your.automation.hub.com/hyperscaler-ee

The following text files will show you the Ansible modules that are present in each of the execution-enviroments we have discussed:

* [ee-supported-modules.txt](ee-supported-modules.txt)
* [ee-minimal-modules.txt](ee-minimal-modules.txt)
* [ee-hyperscaler-modules.txt](ee-hyperscaler-modules.txt) <-- This is the EE you should end up with after ansible-builder is complete

## AAP Configuration

The following variables will be needed for each of your templates (sample values have been provided):

<strong>Amazon EC2</strong>
* ami: "ami-0ef50c2b2eb330511"
* cidr: "10.10.0.0/24"
* cidr_block: "10.10.0.0/16"
* instance_type: "t3.small"
* prefix: "mytestdemo"
* region: "us-east-2"

<strong>Azure</strong>
* admin_username: "azureuser"
* admin_password: "Ins3cur3passw0rd!"
* azure_region: "eastus"
* prefix: "mytestdemo"
* vmSize: "Standard_D4s_v3"

<strong>GCP</strong>
* disk_size: "20"
* machine_type: "f1-micro"
* prefix: "mytestdemo"
* region: "northamerica-northeast2"
* source_image: "projects/rhel-cloud/global/images/rhel-9-v20240611"
* subnet_cidr: "10.10.0.0/24"
* zone: "northamerica-northeast2-a"

