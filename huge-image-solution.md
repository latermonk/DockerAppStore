# ImagePolicyWebhook admission controller

```
The ImagePolicyWebhook admission controller is a Kubernetes admission controller that enforces image policy rules on container images used in Kubernetes workloads. It allows Kubernetes cluster administrators to define custom policies that determine which container images are allowed to be deployed in the cluster.

When a new pod is created or updated, the ImagePolicyWebhook admission controller intercepts the request and sends an admission review to a webhook endpoint specified in the configuration. The webhook endpoint is responsible for evaluating the image policy rules and returning an admission response indicating whether the pod should be allowed or denied.

The webhook endpoint can be implemented using any HTTP server that can receive and respond to admission review requests. The webhook endpoint must implement the Kubernetes AdmissionReview API, which includes a request object containing information about the pod being created or updated, and a response object indicating whether the admission request should be allowed or denied.

The ImagePolicyWebhook admission controller is useful for enforcing security policies on container images, such as ensuring that only signed and verified images are used, or that images come from trusted sources. It can also be used to enforce other policies, such as ensuring that certain images are always used for specific workloads.

Note that the ImagePolicyWebhook admission controller is only available in Kubernetes clusters that have the admissionregistration.k8s.io/v1 API enabled. It is also important to configure the webhook endpoint securely, as it has the ability to block all pod deployments in the cluster.
```
