# Introduction

Polaris can function as an admission controller that uses a webhook to validate incoming workloads. It uses the same configuration as the dashboard and can perform the same checks. Any workloads that fail a danger-level check will be rejected by the webhook, emphasizing Polaris's goal of not only promoting better configuration through visibility but also enforcing it through validation.

# Installation

> A valid TLS certificate is necessary for the Polaris Validating Webhook to function.

- Install cert-manager

`kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml`{{exec}}


- Install Polaris as Admission Controller

```plain
helm repo add fairwinds-stable https://charts.fairwinds.com/stable
helm upgrade --install polaris fairwinds-stable/polaris --namespace polaris  --create-namespace \
  --set image.tag="7"
  --set webhook.enable=true \
  --set dashboard.enable=false
```{{exec}}

- Make sure Polaris Webhook pods are up and running properly.

`kubectl wait --for=condition=ready pod -l app=polaris -n polaris`{{exec}}

- Check validating webhooks

`kubectl get validatingwebhookconfigurations.admissionregistration.k8s.io`{{exec}}

> We can see that Polaris has created validating webhooks in the cluster. 

- Check mutating webhooks

`
kubectl get mutatingwebhookconfigurations.admissionregistration.k8s.io
`{{exec}}

> No Polaris Mutate Webhook found as the mutating webhook is disabled by default. Let not enable it for now.
