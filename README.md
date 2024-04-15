# KEDA Code Challenge

## Introduction

Welcome to the KEDA Code Challenge! This challenge is designed to evaluate your ability to integrate Kubernetes Event-Driven Autoscaling (KEDA) with AWS services. KEDA is a Kubernetes-based event-driven autoscaler that enables you to scale your applications dynamically based on various events.

## Prerequisites

Before you start the challenge, make sure you have the following installed on your development environment:

- [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/)
- [Turn on Kubernetes](https://docs.docker.com/desktop/kubernetes/)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#cli-configure-quickstart-creds)
- [Connection against the tz-dev-awe2-eks001 EKS Cluster](https://tz-cloud.atlassian.net/wiki/spaces/BD/pages/34048413/How+to+Connect+to+an+EKS+Cluster+K8s+Dashboard) (VPN connection required)

Check your connection against the cluster with the following command:
```
kubectl get pods -n platform-architecture
```

## Instructions

### Goal
The goal of this challenge is to deploy an application that uses KEDA to autoscale based on the number of messages in an Amazon Simple Queue Service (SQS) queue.

### Tasks
1. Create a SQS Queue using AWS CLI.
2. Update the [resource.yaml](./resources.yaml) file with the SQS Queue URL (customize the resource names to avoid collisions).
3. Deploy the [resource.yaml](./resources.yaml) file into the `tz-dev-awe2-eks001` EKS Cluster and namespace `platform-architecture`
4. Modify the [resource.yaml](./resources.yaml) file to scale the number of pods depending on the messages in the queue:
   - The target value for queue length will be 5.
   - Minimum number of replicas will be 1.
   - Maximum number of replicas will be 15.
   - The polling interval will be 25 seconds.
   - The period to wait after the last trigger is reported active before scaling the resource back to a minimum will be 150 seconds.
5. Deploy the [resource.yaml](./resources.yaml) file with the changes.
6. Query the Load Balancer URL of the service and send a POST to the path `send` with the body `{ "Messages":1000 }`. This endpoint will send 1000 messages to the queue.
7. Query the pods to see how they are scaling.
8. Clean up all the created resources.

### Bonus
1. Use HELM to package and deploy the application.

## Resources
- [KEDA Documentation](https://keda.sh/docs/)
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- [Getting Started with Kubernetes](https://app.pluralsight.com/library/courses/kubernetes-getting-started-2023/table-of-contents)
- [Kubernetes for the Absolute Beginners - Hands-on](https://tranzact.udemy.com/course/learn-kubernetes/)