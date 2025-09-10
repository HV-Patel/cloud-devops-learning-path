# ☁️ EKS Setup - AWS Managed Kubernetes

<div align="center">

![EKS](https://img.shields.io/badge/EKS-AWS-orange?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Production](https://img.shields.io/badge/Production-Ready-green?style=for-the-badge&logo=check&logoColor=white)

**🎯 Install eksctl | ☁️ Create EKS Cluster | 🚀 Deploy Apps**

</div>

---

## 🎯 When to Use EKS vs k3s

| Feature | k3s (Local) | EKS (AWS) |
|---------|-------------|-----------|
| **Use Case** | Learning, Development | Production, LoadBalancer services |
| **Cost** | Free | ~$0.10/hour + EC2 costs |
| **Setup Time** | 2 minutes | 15-20 minutes |
| **AWS Integration** | None | Full (ALB, EBS, IAM, etc.) |

**Use EKS when you need:**
- AWS LoadBalancer services (ALB/NLB)
- Production-grade security and scaling
- AWS service integrations

---

## 🚀 Quick EKS Setup

### **Prerequisites**
```bash
# Install AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip && sudo ./aws/install

# Configure AWS credentials
aws configure
# Enter: Access Key, Secret Key, Region (us-east-1), Format (json)
```

### **Install eksctl**
```bash
# Download and install eksctl
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin

# Verify installation
eksctl version
```

### **Create EKS Cluster**
```bash
# Create cluster (takes 15-20 minutes)
eksctl create cluster \
  --name my-cluster \
  --region us-east-1 \
  --nodes 2 \
  --node-type t3.medium

# Verify cluster
kubectl get nodes
```

---

## ✅ Test EKS Setup

```bash
# Deploy test app
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=LoadBalancer

# Wait for LoadBalancer (2-3 minutes)
kubectl get services -w

# Get external URL
kubectl get service nginx
# Note the EXTERNAL-IP

# Test
curl http://<EXTERNAL-IP>

# Clean up
kubectl delete deployment nginx
kubectl delete service nginx
```

---

**References:**
- [EKS Getting Started](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)
- [AWS Load Balancer Controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)
- [eksctl Documentation](https://eksctl.io/)
