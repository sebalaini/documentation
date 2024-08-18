# SRE

## k9s

Install [K9s](https://k9scli.io/) via `brew` as specified in the installation documentation `brew install derailed/k9s/k9s`

Run the below commands to move the configuration into `.config/k9s` instead of `Library/Application Support/`, refer to the GitHub [issues #1273](https://github.com/derailed/k9s/issues/1273), `XDG_CONFIG_HOME` is unset in MAC OS X.

```bash
mkdir -p ~/.config/k9s
mv ~/Library/Application\ Support/k9s/config.yaml ~/.config/k9s/
rm -rf ~/Library/Application\ Support/k9s/
ln -s ~/.config/k9s/ ~/Library/Application\ Support/k9s
```

Create a `monokai.yaml` file inside `~/.config/k9s/skins` and copy the [monokai theme](https://github.com/derailed/k9s/blob/master/skins/monokai.yaml)

Add the `skin` setting under the `ui` key

```
k9s:
  ui:
    skin: monokai
```

## Kubernetes

Refer also to the official [kubectl Quick Reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/) documentation.

Kubernetes Objects and Kubectl Command Cheatsheet

### Common Options

In kubectl you can specify optional flags for use with various commands.

`-o=json` – Output format in JSON. It can be pipe with `jq` to filter the result.

```bash
kubectl get pods -o=json

kubectl get deploy -o json | jq “.items[] | {name:.metadata.name} + .spec.strategy.rollingUpdate”
```

`-o=yaml` – Output format in YAML.

```bash
kubectl get pods -o=yaml
```

`-o=wide` – Output in the plain-text format with any additional information, and for pods, the node name is included.

```bash
kubectl get pods -o=wide
```

`-n` – Alias for namespace.

```bash
kubectl get pods -n=<namespace_name>
```

`-f` – Filename, directory, or URL to files to use to create a resource.

```bash
kubectl create -f ./<file name>
```

`-l` – Filter using a specified label.

```bash
kubectl logs -l name=<label name>
```

`-w` – watch a specific service.

```bash
kubectl get pods -w
```

### Configuration Files (Also referred to as Manifest or YAML Files)

Configuration Files (Also referred to as Manifest or YAML Files.) – Kubernetes objects can be created, updated, and deleted by storing multiple object configuration files in a directory and using kubectl apply to recursively create and update those objects as needed. This method retains writes made to live objects without merging the changes back into the object configuration files. kubectl diff also gives you a preview of what changes apply will make.

```bash
kubectl apply -f <configuration file>
kubectl apply -f <configuration file> -n <namespace name> # if the configuration doesn't include the namespace where to deploy
```

`kubectl create -f <configuration file>` – Create objects.

`kubectl create -f <configuration file directory>` – Create objects in all manifest files in a directory.

`kubectl create -f <‘url’>` – Create objects from a URL.

`kubectl delete -f <configuration file>` – Delete an object.

### Cluster Management and Context

Cluster management refers to querying information about the K8S cluster itself.

`kubectl cluster-info` – Display endpoint information about the master and services in the cluster.

`kubectl version` – Display the Kubernetes version running on the client and server.

`kubectl config view` – Get the configuration of the cluster.

`kubectl config view -o jsonpath='{.users[*].name}'` – Get a list of users.

`kubectl config current-context` – Display the current context.

`kubectl config get-contexts` – Display a list of contexts.

`kubectl config use-context <cluster name>` – Set the default context.

`kubectl api-resources` – List the API resources that are available.

`kubectl api-versions` – List the API versions that are available.

`-A` – List pods, services, daemonsets, deployments, replicasets, statefulsets, jobs, and CronJobs in all namespaces, not custom resource types. Note the alias for `--all-namespaces` is `-A`

```bash
kubectl get all --all-namespaces
```

AWS

`aws eks update-kubeconfig --region eu-west-2 --name <cluster name> --profile <AWS profile>` - Update the local Kubernetes configuration with an AWS cluster.

### Daemonsets

Daemonsets – A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

`kubectl get daemonset` – List one or more daemonsets.

`kubectl edit daemonset <daemonset_name>` – Edit and update the definition of one or more daemonset.

`kubectl delete daemonset <daemonset_name>` – Delete a daemonset.

`kubectl create daemonset <daemonset_name>` – Create a new daemonset.

`kubectl rollout daemonset` – Manage the rollout of a daemonset.

`kubectl describe ds <daemonset_name> -n <namespace_name>` – Display the detailed state of daemonsets within a namespace.

### Deployments

Deployments – A Deployment provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments. See StatefulSet vs. Deployment.

`kubectl get deployment` – List one or more deployments.

`kubectl -n <namespace name> get deployments` – List all deployments in a given namespace.

`kubectl describe deployment <deployment_name>` – Display the detailed state of one or more deployments.

`kubectl edit deployment <deployment_name>` – Edit and update the definition of one or more deployments on the server.

`kubectl create deployment <deployment_name>` – Create a new deployment.

`kubectl delete deployment <deployment_name>` – Delete deployments.

`kubectl rollout status deployment <deployment_name>` – See the rollout status of a deployment.

`kubectl set image deployment/<deployment name> <container name>=image:<new image version>` – Perform a rolling update (K8S default), set the image of the container to a new version for a particular deployment.

`kubectl rollout undo deployment/<deployment name>` – Rollback a previous deployment.

`kubectl replace --force -f <configuration file>` – Perform a replace deployment — Force replace, delete and then re-create the resource.

### Events

`kubectl get events` – List recent events for all resources in the system.

`kubectl get events --field-selector type=Warning` – List Warnings only.

`kubectl get events --sort-by=.metadata.creationTimestamp` – List events sorted by timestamp.

`kubectl get events --field-selector involvedObject.kind!=Pod` – List events but exclude Pod events.

`kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name>` – Pull events for a single node with a specific name.

`kubectl get events --field-selector type!=Normal` – Filter out normal events from a list of events.

### Logs

Logs – System component logs record events happening in cluster, which can be very useful for debugging. You can configure log verbosity to see more or less detail. Logs can be as coarse-grained as showing errors within a component, or as fine-grained as showing step-by-step traces of events (like HTTP access logs, pod state changes, controller actions, or scheduler decisions).

`kubectl logs <pod_name>` – Print the logs for a pod.

`kubectl logs --since=6h <pod_name>` – Print the logs for the last 6 hours for a pod.

`kubectl logs --tail=50 <pod_name>` – Get the most recent 50 lines of logs.

`kubectl logs -f <service_name> [-c <$container>]` – Get logs from a service and optionally select which container.

`kubectl logs -f <pod_name>` – Print the logs for a pod and follow new logs.

`kubectl logs -c <container_name> <pod_name>` – Print the logs for a container in a pod.

`kubectl logs <pod_name> pod.log` – Output the logs for a pod into a file named ‘pod.log’.

`kubectl logs --previous <pod_name>` – View the logs for a previously failed pod.

### Namespaces

Namespaces – In Kubernetes, namespaces provides a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc).

`kubectl create namespace <namespace_name>` – Create a namespace.

`kubectl get namespace <namespace_name>` – List one or more namespaces.

`kubectl describe namespace <namespace_name>` – Display the detailed state of one or more namespaces.

`kubectl delete namespace <namespace_name>` – Delete a namespace.

`kubectl edit namespace <namespace_name>` – Edit and update the definition of a namespace.

`kubectl top namespace <namespace_name>` – Display Resource (CPU/Memory/Storage) usage for a namespace.

### Nodes

Nodes – Kubernetes runs your workload by placing containers into Pods to run on Nodes. A node may be a virtual or physical machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods. Typically you have several nodes in a cluster; in a learning or resource-limited environment, you might have only one node. The components on a node include the kubelet, a container runtime, and the kube-proxy.

`kubectl taint node <node_name>` – Update the taints on one or more nodes.

`kubectl get node` – List one or more nodes.

`kubectl delete node <node_name>` – Delete a node or multiple nodes.

`kubectl top node <node_name>` – Display Resource usage (CPU/Memory/Storage) for nodes.

`kubectl get pods -o wide | grep <node_name>` – Pods running on a node.

`kubectl annotate node <node_name>` – Annotate a node.

`kubectl cordon node <node_name>` – Mark a node as unschedulable.

`kubectl uncordon node <node_name>` – Mark node as schedulable.

`kubectl drain node <node_name>` – Drain a node in preparation for maintenance.

`kubectl label node` – Add or update the labels of one or more nodes.

### Pods

Pods – Pods are the smallest deployable units of computing that you can create and manage in Kubernetes. A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. A Pod’s contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific “logical host”: it contains one or more application containers which are relatively tightly coupled. In non-cloud contexts, applications executed on the same physical or virtual machine are analogous to cloud applications executed on the same logical host. As well as application containers, a Pod can contain init containers that run during Pod startup. You can also inject ephemeral containers for debugging if your cluster offers this.

`kubectl get pod` – List one or more pods.

`kubectl get pods --sort-by='.status.containerStatuses[0].restartCount'` – List pods Sorted by Restart Count.

`kubectl get pods --field-selector=status.phase=Running` – Get all running pods in the namespace.

`kubectl -n <namespace name> get pods | grep <pod name>` - Get pods in a given namespace and filter the result with `grep`

`kubectl delete pod <pod_name>` – Delete a pod.

`kubectl describe pod <pod_name>` – Display the detailed state of a pods.

`kubectl create pod <pod_name>` – Create a pod.

`kubectl exec <pod_name> -c <container_name> <command>` – Execute a command against a container in a pod. Read more: Using Kubectl Exec: Connect to Your Kubernetes Containers

`kubectl exec -it <pod_name> /bin/sh (or -- bash)` – Get an interactive shell on a single-container pod.

`kubectl port-forward <pod name> <port number to listen on>:<port number to forward to>` – Listen on a port on the local machine and forward to a port on a specified pod.

`kubectl top pod` – Display Resource usage (CPU/Memory/Storage) for pods.

`kubectl annotate pod <pod_name> <annotation>` – Add or update the annotations of a pod.

`kubectl label pods <pod_name> new-label=<label name>` – Add or update the label of a pod.

`kubectl get pods --show-labels` – Get pods and show labels.

```yaml
labels:
  app: guestbook
  tier: backend
  role: replica
```

`kubectl get pods -Lapp -Ltier -Lrole` - Get pods with given labels

`kubectl get pods -lapp=guestbook,role=replica` - Get pods with given labels & value

### Replication Controllers

Replication Controllers – Note: A Deployment that configures a ReplicaSet is now the recommended way to set up replication. A ReplicationController ensures that a specified number of pod replicas are running at any one time. In other words, a ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available.

`kubectl get rc` – List the replication controllers.

`kubectl get rc --namespace=”<namespace_name>”` – List the replication controllers by namespace.

### ReplicaSets

ReplicaSets – A ReplicaSet’s purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

`kubectl get replicasets` – List ReplicaSets.

`kubectl describe replicasets <replicaset_name>` – Display the detailed state of one or more ReplicaSets.

`kubectl scale --replicas=[x]` – Scale a ReplicaSet.

### Horizontal Pod Autoscaling

In Kubernetes, a `HorizontalPodAutoscaler` automatically updates a workload resource (such as a Deployment or StatefulSet), with the aim of automatically scaling the workload to match demand.

`kubectl -n <namespace name> get hpa` - list autoscalers in a given namespace.

`kubectl describe hpa` - get detailed description.

`kubectl delete hpa` - delete an autoscaler.

### Secrets

Secrets – A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don’t need to include confidential data in your application code.

`kubectl create secret` – Create a secret.

`kubectl get secrets` – List secrets.

`kubectl describe secrets` – List details about secrets.

`kubectl delete secret <secret_name>` – Delete a secret.

### Services

Services – An abstract way to expose an application running on a set of Pods as a network service. With Kubernetes you don’t need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.

`kubectl get services` – List one or more services.

`kubectl describe services` – Display the detailed state of a service.

`kubectl expose deployment [deployment_name]` – Expose a replication controller, service, deployment, or pod as a new Kubernetes service.

`kubectl edit services` – Edit and update the definition of one or more services.

### Service Accounts

Service Accounts – A service account provides an identity for processes that run in a Pod.

Note: This document is a user introduction to Service Accounts and describes how service accounts behave in a cluster set up as recommended by the Kubernetes project. Your cluster administrator may have customized the behavior in your cluster, in which case this documentation may not apply.

When you (a human) access the cluster (for example, using `kubectl`), you are authenticated by the apiserver as a particular User Account (currently this is usually `admin`, unless your cluster administrator has customized your cluster). Processes in containers inside pods can also contact the apiserver. When they do, they are authenticated as a particular Service Account (for example, `default`).

`kubectl get serviceaccounts` – List service accounts.

`kubectl describe serviceaccounts` – Display the detailed state of one or more service accounts.

`kubectl replace serviceaccount` – Replace a service account.

`kubectl delete serviceaccount <service_account_name>` – Delete a service account.
