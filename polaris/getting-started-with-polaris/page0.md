# Introduction

Fairwinds' Polaris keeps your clusters sailing smoothly. It runs a variety of checks to ensure that
Kubernetes pods and controllers are configured using best practices, helping you avoid
problems in the future.

Polaris can be run in three different modes:
* As a `dashboard`, so you can audit what's running inside your cluster.
* As an `admission controller`, so you can automatically reject workloads that don't adhere to your organization's policies.
* As a `command-line tool`, so you can test local YAML files, e.g. as part of a CI/CD process.

<p align="center">
  <img src="./assets/polaris-architecture.svg" alt="Polaris Architecture" width="550"/>
</p>

