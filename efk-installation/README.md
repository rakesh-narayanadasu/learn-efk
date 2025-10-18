# Deploying Elasticsearch and Kibana on Kubernetes (EFK Stack)

This guide walks through the steps required to deploy **Elasticsearch and Kibana** on a Kubernetes cluster as part of the **EFK (Elasticsearch, Fluentd, Kibana)** stack setup.


### Step 1. Allow scheduling on the control plane node
By default, the Kubernetes control plane node is tainted to prevent workloads from being scheduled on it.  
Run the following command to remove the taint:

```bash
kubectl taint node controlplane node-role.kubernetes.io/control-plane-:NoSchedule
```

---

### Step 2. Create a new namespace
Create a dedicated namespace for the EFK components:

```bash
kubectl create namespace efk
```

Switch your current context to the new namespace:

```bash
kubectl config set-context --current --namespace=efk
```

---

### Step 3. Clone the EFK repository

Clone the GitHub repository containing the manifests for Elasticsearch deployment:

```bash
git clone https://github.com/rakesh-narayanadasu/learn-efk.git
```

Change to the Elasticsearch deployment directory:

```bash
cd ~/learn-efk/05-deploy-elasticsearch-on-k8s
```

---

### Step 4. Deploy Elasticsearch components

#### a. Persistent Volume
Apply the Persistent Volume configuration for Elasticsearch storage:

```bash
kubectl apply -f es-pvolume.yaml
```

#### b. StatefulSet
Deploy the Elasticsearch StatefulSet:

```bash
kubectl apply -f es-statefulset.yaml
```

#### c. Service
Expose the Elasticsearch service:

```bash
kubectl apply -f es-service.yaml
```

---

### Step 5. Verify the Deployment

Check the status of Elasticsearch pods:

```bash
kubectl get pods
```



## Deploy Kibana

### Step 1: Apply the Deployment Manifest

Deploy the Kibana pod by applying the deployment manifest:

```bash
kubectl apply -f kibana-deployment.yaml
```

### Step 2: Apply the Service Manifest

Expose the Kibana service:

```bash
kubectl apply -f kibana-service.yaml
```

### Step 3: Verify the Pod Status

Check if the Kibana pod is created:

```bash
kubectl get pods
```

Example output:

```
NAME                                READY   STATUS              RESTARTS   AGE
elasticsearch-0                     1/1     Running             0          4m47s
kibana-5bf7c766b4-pgdz              0/1     ContainerCreating   0          14s
```

Wait a minute or two for the Kibana pod to transition to the **Running** state.  
You can monitor progress in real-time:

```bash
kubectl get pods -w
```

Once the pod shows as **Running**, verify your services:

```bash
kubectl get svc
```
