# Kubernetes Advanced Commands

To prepare for the Certified Kubernetes Application Developer (CKAD) exam, you'll want to be familiar with a specific set of kubectl commands that cover the core areas emphasized in the exam. These areas include application deployment, observability, configuration, multi-container pods, pod design, and troubleshooting. Below is a list of key commands and examples relevant to the CKAD.

## Resource Management

- Set Resource Requests and Limits for a Pod/Container:

    ```
    apiVersion: v1
    kind: Pod
    metadata:
    name: resource-pod
    spec:
    containers:
    - name: nginx
        image: nginx
        resources:
        requests:
            memory: "64Mi"
            cpu: "250m"
        limits:
            memory: "128Mi"
            cpu: "500m"
    ```

    Apply with:
    ```
    kubectl apply -f resource-pod.yaml
    ```

- View Resource Usage:
    ```
    kubectl top pod
    kubectl top node
    ```

## Application and Pod Design

- Create and Expose a Deployment:
    ```
    kubectl create deployment my-deployment --image=nginx
    kubectl expose deployment my-deployment --type=ClusterIP --port=80
    ```

- Rolling Update for a Deployment:
    ```
    kubectl set image deployment/my-deployment nginx=nginx:1.18
    ```

- Rollback a Deployment:
    ```
    kubectl rollout undo deployment/my-deployment
    ```

- List All Running Containers in a Pod:
    ```
    kubectl get pod my-pod -o jsonpath='{.spec.containers[*].name}'
    ```

## Configuration and Secrets Management

- Create a ConfigMap from Literal Values:

    ```
    kubectl create configmap app-config --from-literal=APP_COLOR=blue --from-literal=APP_MODE=production
    ```

- Create a Secret from Literal Values:
    ```
    kubectl create secret generic app-secret --from-literal=password=secret123
    ```
- Mount a ConfigMap as an Environment Variable:

    ```
    apiVersion: v1
    kind: Pod
    metadata:
    name: env-config-pod
    spec:
    containers:
    - name: nginx
        image: nginx
        envFrom:
        - configMapRef:
            name: app-config
    ```

    Apply with:
    ```
    kubectl apply -f env-config-pod.yaml
    ```

- Mount a Secret as a Volume:

    ```
    apiVersion: v1
    kind: Pod
    metadata:
    name: secret-volume-pod
    spec:
    containers:
    - name: nginx
        image: nginx
        volumeMounts:
        - name: secret-volume
        mountPath: "/etc/secret"
        readOnly: true
    volumes:
    - name: secret-volume
        secret:
        secretName: app-secret
    ```
    Apply with:
    ```
        kubectl apply -f secret-volume-pod.yaml
    ```

## Observability and Logging

- Get Pod Logs:
    ```
    kubectl logs my-pod
    ```

- Get Logs for a Specific Container in a Pod:
    ```
    kubectl logs my-pod -c my-container
    ```

- Stream Logs:
    ```
    kubectl logs -f my-pod
    ```

- Describe a Resource (Pod, Node, etc.):
    ```
    kubectl describe pod my-pod
    ```

## Multi-Container Pods

- Create a Pod with Multiple Containers (Sidecar Pattern):

    ```
    apiVersion: v1
    kind: Pod
    metadata:
    name: multi-container-pod
    spec:
    containers:
    - name: main-app
        image: nginx
    - name: sidecar
        image: busybox
        command: ["sh", "-c", "while true; do echo hello from the sidecar; sleep 5; done"]
    ```
    Apply with:
    ```
    kubectl apply -f multi-container-pod.yaml
    ```

## Troubleshooting

- Run a Debugging Pod:
    ```
    kubectl run debug-pod --image=busybox -it --rm -- /bin/sh
    ```

- Check Events:
    ```
    kubectl get events --sort-by='.metadata.creationTimestamp'
    ```

- Get Detailed Pod Status:
    ```
    kubectl describe pod my-pod
    ```

- Access Pod Network to Test Connectivity:
    ```
    kubectl exec -it my-pod -- ping <other-pod-ip>
    ```

- Attach to a Running Container:
    ```
    kubectl attach my-pod -c my-container
    ```

- Port-Forward a Pod Port to a Local Machine Port:
    ```
    kubectl port-forward pod/my-pod 8080:80
    ```

## Scaling Applications

- Scale a Deployment:
    ```
    kubectl scale deployment my-deployment --replicas=5
    ```

- Horizontal Pod Autoscaler (HPA):
    ```
    kubectl autoscale deployment my-deployment --cpu-percent=50 --min=1 --max=10
    ```

## Networking

- Expose a Deployment as a Service:
    ```
    kubectl expose deployment my-deployment --type=NodePort --port=80
    ```
- Get Services:
    ```
    kubectl get services
    ```
- Create a Network Policy from YAML:
    ```
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
    name: allow-access
    spec:
    podSelector:
        matchLabels:
        app: my-app
    policyTypes:
    - Ingress
    ingress:
    - from:
        - podSelector:
            matchLabels:
            access: allowed
    ```
    Apply with:

    ```
    kubectl apply -f network-policy.yaml
    ```

## Quick Creation and Editing of Resources

- Generate YAML for Quick Editing:
    ```
    kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > deployment.yaml
    ```
- Edit an Existing Resource:
    ```
    kubectl edit deployment my-deployment
    ```
- Delete Resources by Label:
    ```
    kubectl delete pods -l app=my-app
    ```

- Imperative Creation with Labels and Annotations:
    ```
    kubectl run nginx --image=nginx --labels="app=my-app,env=prod"
    ```

These commands cover the core areas for CKAD, emphasizing resource management, application deployment, configuration management, observability, troubleshooting, and networking. Practice these commands on a Kubernetes cluster to gain hands-on experience, as practical skills are crucial for success in the CKAD exam.
