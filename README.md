# 🌥️ **Azure Cloud Complete Guide (Beginner → Advanced)**

**Author:** *Atul Kamble – Cloud Solutions Architect*
**Brand:** *Cloudnautic Training*
**Updated:** December 2025

---

## 📘 **1. Introduction to Microsoft Azure**

Azure is Microsoft’s cloud platform offering **Compute, Storage, Networking, Database, DevOps, AI/ML, and Security** services on-demand.

### 🚀 Why Azure?

* Global data centers
* Pay-as-you-go pricing
* Enterprise-grade security
* Strong DevOps & hybrid cloud support
* Rich ecosystem: ARM, Bicep, CLI, PowerShell, Terraform, AKS, ACR, Azure DevOps

---

## 🧱 **2. Azure Building Blocks**

| Resource          | Description            |
| ----------------- | ---------------------- |
| Subscription      | Billing boundary       |
| Resource Group    | Logical container      |
| Region            | Physical location      |
| VNet              | Private network        |
| Subnet            | Segments of VNet       |
| NSG               | Network firewall rules |
| Service Principal | Identity for apps      |
| ARM/Bicep         | IaC deployments        |

---

## 🛠️ **3. Setup & Tools**

### Install Azure CLI

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Login:

```bash
az login
az account show
```

Set default:

```bash
az account set --subscription "<SUB-ID>"
```

---

## 🧩 **4. Azure Compute**

### Create VM (CLI)

```bash
az vm create \
  --name MyVM \
  --resource-group RG1 \
  --image UbuntuLTS \
  --admin-username atul \
  --admin-password "Password@123"
```

### List VM

```bash
az vm list -o table
```

### Start/Stop VM

```bash
az vm start -n MyVM -g RG1
az vm stop -n MyVM -g RG1
```

---

## 🌐 **5. Azure Networking**

### Create VNet + Subnet

```bash
az network vnet create \
  --resource-group RG1 \
  --name VNet1 \
  --subnet-name Subnet1
```

### Public IP

```bash
az network public-ip create \
  -g RG1 \
  -n MyPublicIP \
  --sku Standard
```

### NSG Rules

```bash
az network nsg rule create \
  --resource-group RG1 \
  --nsg-name MyNSG \
  --name AllowSSH \
  --protocol tcp \
  --priority 1000 \
  --destination-port-range 22 \
  --access allow
```

---

## 🗃️ **6. Azure Storage**

### Create Storage Account

```bash
az storage account create \
  --name atulstorage \
  --resource-group RG1 \
  --location eastus \
  --sku Standard_LRS
```

### Create a Container (Blob)

```bash
az storage container create \
  --name mycontainer \
  --account-name atulstorage \
  --auth-mode login
```

---

## 🧪 **7. Azure DevOps Essentials**

### Repos

* Git clone
* Branching
* PR
* Service Connections
* YAML Pipelines

### Classic Pipeline – Variables

```yaml
variables:
  appName: myapp
  environment: dev
```

### YAML Pipeline Example

```yaml
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- script: echo "Building app"
- task: Docker@2
  inputs:
    command: build
    Dockerfile: Dockerfile
```

---

## 📦 **8. Azure Container Services**

### 🐳 **ACR (Azure Container Registry)**

```bash
az acr create -n atulacr -g RG1 --sku Basic
az acr login -n atulacr
docker build -t atulacr.azurecr.io/app:v1 .
docker push atulacr.azurecr.io/app:v1
```

---

## ☸️ **9. AKS (Azure Kubernetes Service)**

### Create AKS Cluster

```bash
az aks create \
  --resource-group RG1 \
  --name AtulAKS \
  --node-count 2 \
  --enable-addons monitoring \
  --generate-ssh-keys
```

### Get Credentials

```bash
az aks get-credentials -g RG1 -n AtulAKS
kubectl get nodes
```

---

## 🧱 **10. Infrastructure as Code — ARM, Bicep, Terraform**

### ARM Deployment

```bash
az deployment group create \
  -g RG1 \
  -f azuredeploy.json \
  -p vmName=MyVM
```

### Bicep Deployment

```bash
az deployment group create \
  -g RG1 \
  -f main.bicep
```

### Terraform Init → Plan → Apply

```bash
terraform init
terraform plan
terraform apply -auto-approve
```

---

## 🔒 **11. Azure Identity & Security**

* Azure AD / Entra ID
* MFA, Conditional Access
* Managed Identity
* Key Vault (Secrets, Keys, Certificates)

### Create Key Vault

```bash
az keyvault create -n AtulKV -g RG1
```

---

## 🗄️ **12. Azure Databases**

### Azure SQL

```bash
az sql server create \
  -g RG1 \
  -n atulsqlserver \
  -u atuladmin \
  -p Password@123
```

### Cosmos DB

```bash
az cosmosdb create -g RG1 -n atulcosmos
```

---

## 📡 **13. Azure Monitoring**

* Azure Monitor
* Log Analytics
* Alerts
* Metrics
* Application Insights

### Enable Monitoring on AKS

```bash
az aks enable-addons -n AtulAKS -g RG1 --addons monitoring
```

---

## 🔄 **14. Azure DevOps CI/CD End-to-End**

### Build:

* Build .NET/Node/Python container
* Push to ACR

### Release:

* Deploy to AKS using manifests
* Service Connection with Kubernetes

### YAML Example for AKS Deploy

```yaml
- task: KubernetesManifest@1
  inputs:
    action: deploy
    manifests: |
      k8s/deployment.yaml
      k8s/service.yaml
```

---

## 🧮 **15. Azure Pricing & Cost Optimization**

* Use Cost Management + Billing
* Right-size VM
* Use Spot Instances
* Auto-shutdown dev/test VMs
* Reservations (1-year / 3-year)

---

## 📜 **16. Azure Interview Questions**

### Basic

* What is a Resource Group?
* Difference between ARM & Bicep?

### Intermediate

* Explain NSG vs Firewall
* Public vs Private Endpoints

### Advanced

* How AKS integrates with ACR?
* How does Azure handle high availability?

---

## 🏁 **17. Complete Azure Project Structure**

```
azure-guide/
 ├── docs/
 ├── bicep/
 ├── terraform/
 ├── pipelines/
 ├── kubernetes/
 ├── src/
 ├── diagrams/
 └── README.md
```
