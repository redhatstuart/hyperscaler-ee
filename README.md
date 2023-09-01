# hyperscaler-ee
Execution environment configuration and sample playbooks for hyperscaler provisioning

Given a host running Ansible Automation Platform (AAP) Controller / Automation Hub, the default execution environment "ee-supported-rhelX:latest" includes provisioning and control modules for Amazon Web Services (AWS) resources. This module, however, does not include support for Google Cloud Platform (GCP) or Microsoft Azure installed by default.

Minimal execution environments, ee-minimal-rhelX:latest, do not include support for any hyperscalers.

This configuration assumes that you have access to registry.redhat.io and have subsequently logged in prior to building your execution environment. The new execution environment is based off of the "ee-minimal-rhel9" execution environment.

To use this repo:

1: git clone https://github.com/redhatstuart/hyperscaler-ee
2: podman login registry.redhat.io
3: Customize execution-environment.yml (if necessary)
4: ansible-builder build -v3 -t hyperscaler-ee

After the new execution environment has been built, you can push this so your Automation Hub and subsequently have your AAP controller ingest it.

5: podman tag localhost/hyperscaler-ee fqdn.of.your.automation.hub.com/hyperscaler-ee
6: podman push fqdn.of.your.automation.hub.com/hyperscaler-ee
