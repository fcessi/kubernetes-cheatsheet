Kubectl is the command line configuration tool for Kubernetes that communicates with a Kubernetes API server. Using kubectl allows you to create, inspect, update, and delete Kubernetes objects. We've created this cheatsheet as a quick reference to make commands on many common Kubernetes components and resources. You can use the full command for an object, like pod, the plural form (pods) or the shortcode variation we mention in parantheses in the heading of each section. They will all generate the same outcome. You'll need to follow up most of the commands with the specific <name> of the resource you are managing.

## Cluster Management

Display endpoint information about the master and services in the cluster

```json
kubectl cluster-info
```

Display the Kubernetes version running on the client and server

```json
kubectl version
```

Get the configuration of the cluster

```json
kubectl config view
```

List the API resources that are available

```json
kubectl api-resources
```

List the API versions that are available

```json
kubectl api-versions
```

List everything

```json
kubectl get all --all-namespaces
```

## Daemonsets

**Shortcode = ds**

List one or more daemonsets

```json
kubectl get daemonset
```

Edit and update the definition of one or more daemonset

```json
kubectl edit daemonset <daemonset_name>
```

Delete a daemonset

```json
kubectl delete daemonset <daemonset_name>
```

Create a new daemonset

```json
kubectl create daemonset <daemonset_name>
```

Manage the rollout of a daemonset

```json
kubectl rollout daemonset
```

Display the detailed state of daemonsets within a namespace

```json
kubectl describe ds <daemonset_name> -n <namespace_name>
```

## Deployments

**Shortcode = deploy**

List one or more deployments

```json
kubectl get deployment
```

Display the detailed state of one or more deployments

```json
kubectl describe deployment <deployment_name>
```

Edit and update the definition of one or more deployment on the server

```json
kubectl edit deployment <deployment_name>
```

Create one a new deployment

```json
kubectl create deployment <deployment_name>
```

Delete deployments

```json
kubectl delete deployment <deployment_name>
```

See the rollout status of a deployment

```json
kubectl rollout status deployment <deployment_name>
```

## Events

**Shortcode = ev**

List recent events for all resources in the system

```json
kubectl get events
```

List Warnings only

```json
kubectl get events --field-selector type=Warning
```

List events but exclude Pod events

```json
kubectl get events --field-selector involvedObject.kind!=Pod
```

Pull events for a single node with a specific name

```json
kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name>
```

Filter out normal events from a list of events

```json
kubectl get events --field-selector type!=Normal
```

## Logs

Print the logs for a pod

```json
kubectl logs <pod_name>
```

Print the logs for the last hour for a pod

```json
kubectl logs --since=1h <pod_name>
```

Get the most recent 20 lines of logs

```json
kubectl logs --tail=20 <pod_name>
```

Get logs from a service and optionally select which container

```json
kubectl logs -f <service_name> [-c <$container>]
```

Print the logs for a pod and follow new logs

```json
kubectl logs -f <pod_name>
```

Print the logs for a container in a pod

```json
kubectl logs -c <container_name> <pod_name>
```

Output the logs for a pod into a file named ‘pod.log’

```json
kubectl logs <pod_name> > pod.log
```

For logs we also recommend using a tool developed by Johan Haleby called Kubetail. This is a bash script that will allow you to get logs from multiple pods simultaneously. You can learn more about it at its [Github repository.](https://github.com/johanhaleby/kubetail) Here are some sample commands using Kubetail.

Get logs for all pods named with pod_prefix

```json
kubetail <pod_prefix>
```

Include the most recent 5 minutes of logs

```json
kubetail <pod_prefix> -s 5m
```

## Manifest Files

Another option for modifying objects is through Manifest Files. We highly recommend using this method. It is done by using yaml files with all the necessary options for objects configured. We have our yaml files stored in a git repository, so we can track changes and streamline changes.

Apply a configuration to an object by filename or stdin. Overrides the existing configuration.

```json
kubectl apply -f manifest_file.yaml
```

Create objects

```json
kubectl create -f manifest_file.yaml
```

Create objects in all manifest files in a directory

```json
kubectl create -f ./dir
```

Create objects from a URL

```json
kubectl create -f ‘url’
```

Delete an object

```json
kubectl delete -f manifest_file.yaml
```

## Namespaces

**Shortcode = ns**

Create namespace <name>

```json
kubectl create namespace <namespace_name>
```

List one or more namespaces

```json
kubectl get namespace <namespace_name>
```

Display the detailed state of one or more namespace

```json
kubectl describe namespace <namespace_name>
```

Delete a namespace

```json
kubectl delete namespace <namespace_name>
```

Edit and update the definition of a namespace

```json
kubectl edit namespace <namespace_name>
```

Display Resource (CPU/Memory/Storage) usage for a namespace

```json
kubectl top namespace <namespace_name>
```

## Nodes

**Shortcode = no**

Update the taints on one or more nodes

```json
kubectl taint node <node_name>
```

List one or more nodes

```json
kubectl get node
```

Delete a node or multiple nodes

```json
kubectl delete node <node_name>
```

Display Resource usage (CPU/Memory/Storage) for nodes

```json
kubectl top node
```

Resource allocation per node

```json
kubectl describe nodes | grep Allocated -A 5
```

Pods running on a node

```json
kubectl get pods -o wide | grep <node_name>
```

Annotate a node

```json
kubectl annotate node <node_name>
```

Mark a node as unschedulable

```json
kubectl cordon node <node_name>
```

Mark node as schedulable

```json
kubectl uncordon node <node_name>
```

Drain a node in preparation for maintenance

```json
kubectl drain node <node_name>
```

Add or update the labels of one or more nodes

```json
kubectl label node
```

## Pods

**Shortcode = po**

List one or more pods

```json
kubectl get pod
```

Delete a pod

```json
kubectl delete pod <pod_name>
```

Display the detailed state of a pods

```json
kubectl describe pod <pod_name>
```

Create a pod

```json
kubectl create pod <pod_name>
```

Execute a command against a container in a pod

```json
kubectl exec <pod_name> -c <container_name> <command>
```

Get interactive shell on a a single-container pod

```json
kubectl exec -it <pod_name> /bin/sh
```

Display Resource usage (CPU/Memory/Storage) for pods

```json
kubectl top pod
```

Add or update the annotations of a pod

```json
kubectl annotate pod <pod_name> <annotation>
```

Add or update the label of a pod

```json
kubectl label pod <pod_name>
```

## Replication Controllers

**Shortcode = rc**

List the replication controllers

```json
kubectl get rc
```

List the replication controllers by namespace

```json
kubectl get rc --namespace=”<namespace_name>”
```

## ReplicaSets

**Shortcode = rs**

List ReplicaSets

```json
kubectl get replicasets
```

Display the detailed state of one or more ReplicaSets

```json
kubectl describe replicasets <replicaset_name>
```

Scale a ReplicaSet

```json
kubectl scale --replicas=[x] 
```

## Secrets

Create a secret

```json
kubectl create secret
```

List secrets

```json
kubectl get secrets
```

List details about secrets

```json
kubectl describe secrets
```

Delete a secret

```json
kubectl delete secret <secret_name>
```

## Services

**Shortcode = svc**

List one or more services

```json
kubectl get services
```

Display the detailed state of a service

```json
kubectl describe services
```

Expose a replication controller, service, deployment or pod as a new Kubernetes service

```json
kubectl expose deployment [deployment_name]
```

Edit and update the definition of one or more services

```json
kubectl edit services
```

## Service Accounts

**Shortcode = sa**

List service accounts

```json
kubectl get serviceaccounts
```

Display the detailed state of one or more service accounts

```json
kubectl describe serviceaccounts
```

Replace a service account

```json
kubectl replace serviceaccount
```

Delete a service account

```json
kubectl delete serviceaccount <service_account_name>
```

## StatefulSet

**Shortcode = sts**

List StatefulSet

```json
kubectl get statefulset
```

Delete StatefulSet only (not pods)

```json
kubectl delete statefulset/[stateful_set_name] --cascade=false
```

## Common Options

In Kubectl you can specify optional flags with commands. Here are some of the most common and useful ones.

-o Output format. For example if you wanted to list all of the pods in ps output format with more information.

```json
kubectl get pods -o wide 
```

-n Shorthand for --namespace. For example, if you’d like to list all the Pods in a specific Namespace you would do this command:

```json
kubectl get pods --namespace=[namespace_name]
```

```json
kubectl get pods -n=[namespace_name]
```

-f Filename, directory, or URL to files to use to create a resource. For example when creating a pod using data in a file named newpod.json.

```json
kubectl create -f ./newpod.json
```

-l Selector to filter on, supports ‘=’, ‘==’, and ‘!=’.

Help for kubectl

-h
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjQ0OTk1NjczXX0=
-->