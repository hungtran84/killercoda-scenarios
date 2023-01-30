# Polaris configuration

In this section we will have a quick look into the default configuration of Polaris and how to customize it to meet your security requirement.

- Download the default policy which automatically loaded with helm as default value.

` wget https://raw.githubusercontent.com/FairwindsOps/polaris/master/examples/config.yaml`{{exec}}

## Check settings

Validation checks in Polaris can be assigned a severity level of "danger" or "warning." Only checks with these severity levels will be validated, and the results can be viewed on the dashboard. If using a validating webhook, only failures with a severity of "danger" will cause a change to be rejected.

Polaris validation checks include categories

- Security.
- Reliability.
- Efficiency.

## Custom Check

If the default/build-in checks are not satisfy your need, you can write your own checks.

## Excemptions

When certain workloads require actions that Polaris deems as insecure, exceptions can be made to allow them to pass the checks. This can occur with workloads such as kube-system, which need to run as root or access the host network. Exemptions can be applied in various methods: by editing the Polaris config at the namespace level, annotating a controller, or editing the Polaris config at the container level.

Let's deep dive into polaris configuration and customization in the upcoming tasks
