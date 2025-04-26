# Todo App - Kubernetes Deployment

Welcome to my first Kubernetes project! 🚀  
In this project, I deployed a simple **Todo Application** on a local Kubernetes cluster using **Minikube**, and exposed it globally using **ngrok**.

---

## 📦 Project Structure

```
.
├── pod.yaml            # Kubernetes Pod configuration for the todo-app
├── service.yaml        # Kubernetes Service to expose the Pod internally
├── ingress.yaml        # Ingress resource to expose the Service externally
├── deployment.yaml     # Kubernetes Deployment (optional if you use Pod only)
├── README.md           # Project documentation
```

---

## 🛠️ Technologies Used

- **Kubernetes**
- **Minikube**
- **ngrok** (for tunneling)
- **YAML** for Kubernetes manifests
- **Docker** (optional, if you build your own app image)

---

## 🚀 How to Run Locally

1. **Start Minikube**

```bash
minikube start
```

2. **Deploy the Pod**

```bash
kubectl apply -f pod.yaml
```

3. **Expose the Pod with a Service**

```bash
kubectl apply -f service.yaml
```

4. **Set up Ingress Controller (Minikube)**

```bash
minikube addons enable ingress
```

5. **Deploy the Ingress Resource**

```bash
kubectl apply -f ingress.yaml
```

6. **Update `/etc/hosts` (Optional for local domain)**

Add this line to your `/etc/hosts` file:

```
127.0.0.1 todo-app.example.com
```

7. **Access Locally**

You can now access your app via:

```
http://todo-app.example.com
```

*(Note: if using NodePort service, you can also access it via Minikube IP and assigned port.)*

---
## 🌎 Make It Public Using ngrok

If you want to expose your local app to the internet using **ngrok**, follow these steps:

1. **Download and Install ngrok**

Run the following command to download and install ngrok on your machine:

```bash
curl -sSL https://ngrok-agent.s3.amazonaws.com/ngrok.asc   | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null   && echo "deb https://ngrok-agent.s3.amazonaws.com buster main"   | sudo tee /etc/apt/sources.list.d/ngrok.list   && sudo apt update   && sudo apt install ngrok
```

2. **Set ngrok Authentication Token**

To authenticate ngrok, use your ngrok authtoken. Run the following command:

```bash
ngrok config add-authtoken XXXXXXXXXXXXXXXX
```

Replace `XXXXXXXXXXXXXXXXXXX` with your personal **ngrok authentication token**. You can get it by signing up on [ngrok's website](https://ngrok.com/) and navigating to the "Auth" section.

3. **Start an ngrok Tunnel**

Start an ngrok tunnel to your local Minikube service:

```bash
ngrok http 192.168.49.2:30004
```

ngrok will generate a public URL like:

```
https://abc1234.ngrok.io
```

Now your Todo App is accessible globally at that URL!

---



## 🧠 What I Learned

- Deploying standalone Pods and Services in Kubernetes
- Setting up Ingress resources for clean external access
- Exposing local services globally using ngrok
- Managing networking and routing inside Kubernetes clusters

---

## 📢 Future Improvements

- Migrate from standalone Pod to Deployment for better scaling
- Add SSL/TLS certificates to Ingress (Let's Encrypt)
- Use ConfigMaps and Secrets for environment management
- Deploy on a cloud Kubernetes service (AWS EKS, Azure AKS, GCP GKE)
- Implement a full CI/CD pipeline for deployments

---


