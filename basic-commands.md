# Kubernetes Basic Commands
Here’s a comprehensive list of essential Kubernetes commands with examples. The commands use kubectl, the command-line interface for interacting with Kubernetes clusters.

## Cluster Management

- Display clusters defined in the kubeconfig: `kubectl config get-clusters`
- Delete the specified cluster from the kubeconfig: `kubectl config delete-cluster NAME`
- Get cluster details: `kubectl describe cluster <cluster-name>`
- Get Cluster Resource Quotas: `kubectl get resourcequotas`
- View Cluster Info: `kubectl cluster-info`
- List Nodes in Cluster: `kubectl get nodes`
- View Detailed Node Info: `kubectl describe node <node-name>`

## Namespace Management

- List All Namespaces: `kubectl get namespaces`
- Create a New Namespace: `kubectl create namespace my-namespace`
- Delete a Namespace: `kubectl delete namespace my-namespace`
- Get namespace details: `kubectl describe namespace <namespace-name>`

## Pod Management

- List All Pods: `kubectl get pods`
- List Pods in a Specific Namespace: `kubectl get pods -n my-namespace`
- Create a Pod from YAML: `kubectl apply -f pod.yaml` or `kubectl create -f <pod-yaml-file>`
- Delete a Pod: `kubectl delete pod my-pod`
- Describe a Pod: `kubectl describe pod my-pod`
- Delete Resources by Label: `kubectl delete pods -l app=my-app`
- View Logs for a Pod: `kubectl logs my-pod`
- Execute a Command in a Pod: `kubectl exec -it my-pod -- /bin/bash`

## Deployment Management

- Create a Deployment: `kubectl create deployment my-deployment --image=nginx`
- List All Deployments: `kubectl get deployments`
- Update Deployment Image: `kubectl set image deployment/my-deployment nginx=nginx:latest`
- Scale a Deployment: `kubectl scale deployment my-deployment --replicas=5`
- Create a deployment: `kubectl create -f <deployment-yaml-file>`
- Delete a Deployment: `kubectl delete deployment my-deployment`
- Get deployment details: `kubectl describe deployment <deployment-name>`

## Service Management

- List All Services: `kubectl get services`
- Get service details: `kubectl describe service <service-name>`
- Create a Service from YAML: `kubectl apply -f service.yaml` or `kubectl create -f <service-yaml-file>`
- Delete a Service: `kubectl delete service my-service`

## ConfigMap and Secret Management

- Create a ConfigMap: `kubectl create configmap my-config --from-literal=key=value`
- List ConfigMaps: `kubectl get configmaps`
- View ConfigMap Details: `kubectl describe configmap my-config`
- Create a Secret: `kubectl create secret generic my-secret --from-literal=password=mypassword`
- List Secrets: `kubectl get secrets`

## Persistent Volume and Persistent Volume Claim Management

- List Persistent Volumes (PVs): `kubectl get pv`
- List Persistent Volume Claims (PVCs): `kubectl get pvc`
- Create a Persistent Volume from YAML: `kubectl apply -f pv.yaml`
- Create a Persistent Volume Claim from YAML: `kubectl apply -f pvc.yaml`

## ReplicaSet Management

- List ReplicaSets: `kubectl get replicasets`
- Scale a ReplicaSet: `kubectl scale --replicas=3 replicaset my-replicaset`
- Delete a ReplicaSet: `kubectl delete replicaset my-replicaset`

## StatefulSet Management

- List StatefulSets: `kubectl get statefulsets`
- Scale a StatefulSet: `kubectl scale statefulset my-statefulset --replicas=3`
- Delete a StatefulSet: `kubectl delete statefulset my-statefulset`

## DaemonSet Management

- List DaemonSets: `kubectl get daemonsets`
- Delete a DaemonSet: `kubectl delete daemonset my-daemonset`

## Job and CronJob Management

- Create a Job from YAML: `kubectl apply -f job.yaml`
- List Jobs: `kubectl get jobs`
- Create a CronJob from YAML: `kubectl apply -f cronjob.yaml`
- List CronJobs: `kubectl get cronjobs`
- Delete a Job or CronJob: `kubectl delete job my-job`
`kubectl delete cronjob my-cronjob`

## Network Policy Management

- Create a Network Policy from YAML: `kubectl apply -f network-policy.yaml`
- List Network Policies: `kubectl get networkpolicies`
- Delete a Network Policy: `kubectl delete networkpolicy my-network-policy`

## Taints and Tolerations

- Add a Taint to a Node: `kubectl taint nodes <node-name> key=value:NoSchedule`
- Remove a Taint from a Node: `kubectl taint nodes <node-name> key=value:NoSchedule-`

## Affinity and Anti-Affinity

- Set Node Affinity in Pod YAML:

    ```
    affinity:
    nodeAffinity:
        requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
            - key: disktype
            operator: In
            values:
            - ssd
    ```

- Set Pod Anti-Affinity in Pod YAML:

    ```
    affinity:
        podAntiAffinity:
        requiredDuringSchedulingIgnoredDuringExecution:
        - labelSelector:
            matchLabels:
                app: my-app
            topologyKey: "kubernetes.io/hostname"
    ```

## Logs

- Get logs from a pod: `kubectl logs <pod-name>`
- Get logs from a container within a pod: `kubectl logs <pod-name> -c <container-name>`

## Exec

- Execute a command in a pod: `kubectl exec <pod-name> -- <command>`
- Execute a command in a container within a pod: `kubectl exec <pod-name> -c <container-name> -- <command>`

## Labels

- Add a label to a pod: `kubectl label pod <pod-name> <label-key>=<label-value>`
- Remove a label from a pod: `kubectl label pod <pod-name> <label-key>-`

## Annotations

- Add an annotation to a pod: `kubectl annotate pod <pod-name> <annotation-key>=<annotation-value>`
- Remove an annotation from a pod: `kubectl annotate pod <pod-name> <annotation-key>-`

## Config

- Get the current context: `kubectl config current-context`
- Get the current namespace: `kubectl config view --minify | grep namespace`
- Set the current namespace: `kubectl config set-context --current --namespace=<namespace-name>`

These commands cover a wide range of Kubernetes operations and can help you manage almost all resources in a Kubernetes cluster.
