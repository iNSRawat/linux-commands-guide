# ⚓ Standalone Kubernetes (K8s) Guide

Welcome! If you have just heard about Kubernetes and are wondering what it does, why it is used alongside Docker, and how to configure it like a seasoned cloud engineer—you are in the right place. 

This guide breaks down Kubernetes into clear, beginner-friendly terms and scales up to advanced cluster deployment, YAML manifest creation, and production-level optimizations on Windows, macOS, and Linux.

---

## ⚓ What is Kubernetes? (For Complete Beginners)

In our [Docker Guide](docs/docker-guide.md), we talked about the shipping container analogy. Docker solves the packaging problem. It puts your app and its dependencies inside a standard container.
- That works beautifully when you have a single container running.
- But what happens in a real-world system when your application grows to 50, 100, or 1,000 containers?
  - What if a container crashes in the middle of the night? Who restarts it?
  - How do you scale up your web containers to handle a sudden surge in traffic?
  - How do containers discover and talk to each other across different servers?
  - How do you deploy new features without taking your website offline?

### The Solution: The Harbor Master / Port Director
**Kubernetes (often abbreviated as K8s)** is the **Harbor Master** of your container shipping yard. 
- While Docker builds and runs the individual containers, Kubernetes manages the entire port.
- It directs which cargo ship (server) should hold which containers, monitors container health, automatically spawns replacement containers if one crashes, scales containers up or down depending on traffic, and routes external network traffic to the right container inside the port.

### 🆚 Virtual Machines vs. Containers in Orchestration
Orchestrating raw Virtual Machines requires booting complete operating systems, which takes minutes and requires massive CPU and memory reserves. Because Kubernetes orchestrates lightweight **Containers**, it can scale services or recover from crashes in a matter of seconds, making the system highly responsive.

### 🧠 The Core Architecture of a Cluster
A Kubernetes cluster consists of two main types of resources:

```
                  ┌──────────────────────────────────────┐
                  │            CONTROL PLANE             │
                  │  (The Brain: API Server, Scheduler)  │
                  └──────────────────┬───────────────────┘
                                     │ (Manages)
                  ┌──────────────────┴───────────────────┐
                  │            WORKER NODES              │
                  │    (The Servers: Running Pods)       │
                  └──────────────────────────────────────┘
```

1. **Control Plane (The Brain)**: A collection of services that manage the cluster. It decides where to run applications, tracks cluster health, and responds to scaling demands.
2. **Worker Nodes (The Muscle)**: Physical or virtual machines that run your applications.
3. **Kubelet**: A tiny system agent running on each worker node that communicates with the Control Plane and ensures the containers are running properly.
4. **Pod**: The absolute smallest building block in Kubernetes. A Pod is a wrapper that hosts one or more containers (usually just one) sharing the same network IP address and storage volume.

---

## 💻 Complete Local Cluster Setup & Expert Configuration

To interact with a Kubernetes cluster, you need **kubectl** (pronounced "kube-control" or "kube-cuttle"), the official command-line tool. Choose your OS below to set up `kubectl` and a local sandbox cluster.

### 🪟 1. Windows Setup (Minikube + WSL2)

#### Beginner Step-by-Step Installation:
1. **Install kubectl**: Open PowerShell as Administrator and run:
   ```powershell
   winget install Kubernetes.kubectl
   ```
   *Restart your terminal and type `kubectl version --client` to verify.*
2. **Install Minikube**: Minikube runs a single-node local Kubernetes cluster inside a VM or Docker container. Run:
   ```powershell
   winget install -e --id Kubernetes.minikube
   ```
3. **Start the Cluster**: Ensure Docker Desktop is running and execute:
   ```powershell
   minikube start --driver=docker
   ```
4. **Verify connection**:
   ```powershell
   kubectl get nodes
   ```

---

#### 🛠️ Windows Expert-Level Optimization:
- **Resource Constraints**: Avoid letting Minikube drain your computer's RAM. Start it with specific limits:
  ```powershell
  minikube start --cpus=2 --memory=4096 --driver=docker
  ```
- **Terminal Autocomplete (PowerShell/CMD)**:
  To get command completion in PowerShell, add this to your PowerShell Profile (`$PROFILE`):
  ```powershell
  if (Get-Command kubectl -ErrorAction SilentlyContinue) {
      kubectl completion powershell | Out-String | Invoke-Expression
  }
  ```

---

### 🍎 2. macOS Setup (Homebrew & Fast Clusters)

#### Beginner Step-by-Step Installation:
1. **Install kubectl and Minikube**: Open Terminal and run:
   ```bash
   brew install kubectl minikube
   ```
2. **Start Minikube**:
   ```bash
   minikube start
   ```

---

#### 🛠️ macOS Expert-Level Optimization:
- **OrbStack (Ultimate macOS Alternative)**: 
  Instead of running Minikube (which uses a heavy virtual machine backend on macOS), download [OrbStack](https://orbstack.dev/).
  - Go to **OrbStack Settings** -> **Kubernetes**.
  - Toggle **Enable Kubernetes** on.
  - OrbStack starts a local cluster natively in less than 2 seconds, uses 0% CPU when idle, and integrates directly with your system DNS. It is the gold standard for Mac developers.
- **Colima (FOSS Command-line alternative)**:
  ```bash
  brew install colima docker kubectl
  colima start --kubernetes --cpu 2 --memory 4
  ```

---

### 🐧 3. Linux Setup (kubectl + Lightweight k3s)

#### 🟠 Ubuntu/Debian kubectl Installation:
```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

#### 🔵 Fedora/RHEL kubectl Installation:
```bash
# Add Kubernetes YUM repository
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/repodata/repomd.xml.key
EOF
sudo dnf install -y kubectl
```

---

#### 🛠️ Linux Expert-Level Configuration (k3s for Production-ready Dev):
Minikube is designed for testing, not production. For home-labs, testing servers, or edge deployments, use **k3s** by Rancher. It is a fully-compliant Kubernetes engine packaged in a single <100MB binary.

1. **Install k3s in one command**:
   ```bash
   curl -sfL https://get.k3s.io | sh -
   ```
2. **Establish Access (No sudo)**:
   By default, kubectl commands for k3s must be run with `sudo`. Let's configure it for your user:
   ```bash
   mkdir -p ~/.kube
   sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
   sudo chown $USER:$USER ~/.kube/config
   chmod 600 ~/.kube/config
   export KUBECONFIG=~/.kube/config
   ```
3. **Verify the node**:
   ```bash
   kubectl get nodes
   ```

---

## 📄 Manifest YAML Construction & Expert Best Practices

Kubernetes is **declarative**. Instead of typing commands to start containers, you write YAML files (Manifests) describing your desired state and apply them.

### Core Kubernetes Objects
- **Pod**: Direct container wrapper.
- **Deployment**: Declares the number of Pod replicas you want, manages rolling updates, and handles scaling.
- **Service**: Assigns a stable IP address and DNS name, load-balancing requests across Pods.
  - *ClusterIP* (default): Accessible only inside the cluster.
  - *NodePort*: Opens a specific port on the Host Node's IP address (accessible externally).
  - *LoadBalancer*: Provisions a cloud provider external load balancer automatically.
- **ConfigMap / Secret**: Separates configuration parameters and sensitive API keys from container code.

---

### 🚀 Manifest Expert Best Practices

#### 1. Define Resource Requests and Limits (Mandatory!)
If you do not configure memory limits, a container with a memory leak will consume all resources on the server. The host operating system will trigger an **OOM (Out-Of-Memory) Kill**, crashing your cluster services.
- `requests`: The minimum CPU and RAM guaranteed to the Pod.
- `limits`: The absolute maximum resources the Pod can use before being throttled or terminated.

#### 2. Set Up Health Probes
- **Readiness Probe**: Tells Kubernetes when your application is fully initialized. Traffic will not be routed to the Pod until it passes this check.
- **Liveness Probe**: Monitors if the container is frozen or crashed. If the probe fails, Kubernetes destroys and restarts the Pod automatically.

---

### 📄 Production-Grade Deployment and Service Manifest
Save this file as `app-manifest.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-web-app
  namespace: default
  labels:
    app: web
spec:
  replicas: 3 # Tells K8s to keep exactly 3 copies of this container running
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web-container
        image: nginx:alpine
        ports:
        - containerPort: 80
        
        # 1. Resource Limits (Prevents container resource hogging)
        resources:
          requests:
            memory: "64Mi"
            cpu: "100m" # 100 millicores (0.1 CPU core)
          limits:
            memory: "128Mi"
            cpu: "200m"

        # 2. Readiness Probe (Traffic Routing Protection)
        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 10

        # 3. Liveness Probe (Auto-Restart Function)
        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 15
          periodSeconds: 20
---
apiVersion: v1
kind: Service
metadata:
  name: web-service
  namespace: default
spec:
  selector:
    app: web # Routes traffic to any Pods with the label app=web
  ports:
    - protocol: TCP
      port: 80         # Port exposed on the service IP
      targetPort: 80   # Port the container listens on
  type: ClusterIP      # Internal cluster communication only
```

---

## 🐚 Shell & Windows CMD Syntax Workarounds

When executing Kubernetes commands on Windows CMD vs. PowerShell vs. Linux/macOS Bash, be aware of these syntax variations.

### 1. Applying Configuration Files
Applying manifests declaratively using pipeline inputs:
- **Bash (Linux/macOS/WSL)**:
  ```bash
  cat app-manifest.yaml | kubectl apply -f -
  ```
- **PowerShell**:
  ```powershell
  Get-Content app-manifest.yaml | kubectl apply -f -
  ```
- **Windows Command Prompt (CMD)**:
  ```cmd
  type app-manifest.yaml | kubectl apply -f -
  ```

### 2. Creating CLI Aliases (Save Typing Time)
雲端工程師 (Cloud engineers) rarely type the full `kubectl` command. They set up aliases:
- **Bash (Add to `~/.bashrc`)**:
  ```bash
  alias k=kubectl
  complete -o default -F __start_kubectl k
  ```
- **PowerShell (Add to profile script)**:
  ```powershell
  Set-Alias -Name k -Value kubectl
  ```
- **Windows Command Prompt (CMD)**:
  ```cmd
  doskey k=kubectl $*
  ```
  *Note: To run commands with this alias in CMD, simply type `k get nodes`.*

### 3. Namespace Scoped Queries
Checking pods inside a specific namespace:
- **Bash / PowerShell**:
  ```bash
  kubectl get pods -n kube-system
  ```
- **Windows Command Prompt (CMD)**:
  ```cmd
  kubectl get pods --namespace kube-system
  ```

---

## 🛠️ Essential command Cheatsheet

```bash
kubectl apply -f app-manifest.yaml        # Deploy/Update resources in manifest
kubectl get deployments                    # List deployed apps
kubectl get pods                           # Check status of running pods
kubectl get services                       # View available services & their IPs
kubectl describe pod <pod_name>            # Detailed configuration & event logs of a pod
kubectl logs <pod_name>                    # View application standard output logs
kubectl logs -f <pod_name>                 # Live stream application output logs
kubectl exec -it <pod_name> -- sh          # Open interactive shell inside a running pod
kubectl delete -f app-manifest.yaml        # Remove resources defined in manifest
```

---

## 📚 Educational & Execution Resources

### 📖 Learning Resources
1. **[Kubernetes Official Docs](https://kubernetes.io/docs/)**: Comprehensive tutorials, standard manifests, and conceptual guides.
2. **[Killercoda K8s Playgrounds](https://killercoda.com/playgrounds)**: A free, web-based, pre-configured Kubernetes cluster terminal environment. Great for practicing cluster configurations.
3. **[Interactive K8s Roadmap](https://roadmap.sh/kubernetes)**: The developer roadmap mapping out the pathway to becoming a Kubernetes administrator (CKA).
4. **[Kubernetes Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)**: The ultimate official reference table of kubectl commands.

### ⚙️ Executing & Managing Resources
1. **[k9s Terminal GUI (TUI)](https://github.com/derailed/k9s)**: The absolute best terminal-based cluster management client. Instead of writing shell queries, navigate through pods, read logs, edit configurations, and restart deployments with simple keystrokes.
2. **[Lens Desktop IDE](https://k8slens.dev/)**: A beautiful visual desktop application that shows performance graphs, workload metrics, networking tables, and lets you manage multiple clusters.
3. **Managed Production Runtimes (Cloud Provider Managed)**:
   - **[Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine)**: High-performance, fully managed environment.
   - **[Amazon Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/)**: Standard corporate environment.
   - **[Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service)**: Highly integrated Microsoft ecosystem engine.
