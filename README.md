# Docker Image Pipeline with AWS ECR

Automated pipeline for building Docker images and pushing them to AWS Elastic Container Registry (ECR). Demonstrates a production-ready container image management workflow integrated with AWS.

---

## 🛠️ Tech Stack

- **Docker** — container image building
- **AWS ECR** — private Docker image registry
- **AWS CLI** — authentication and registry interaction
- **Bash** — pipeline scripting

---

## 🏗️ Pipeline Overview

```
Code Change → Docker Build → Tag Image → Authenticate to ECR → Push Image → Image Available in ECR
```

---

## 📁 Project Structure

```
docker-aws-ecr-pipeline/
├── Dockerfile              # Container image definition
└── push-to-ecr.sh          # Automation script (optional)
```

---

## ☁️ AWS ECR Workflow

### 1. Create ECR Repository (one-time)

```bash
aws ecr create-repository --repository-name my-app --region us-east-1
```

### 2. Authenticate Docker to ECR

```bash
aws ecr get-login-password --region us-east-1 | \
  docker login --username AWS --password-stdin \
  <account-id>.dkr.ecr.us-east-1.amazonaws.com
```

### 3. Build Docker Image

```bash
docker build -t my-app .
```

### 4. Tag for ECR

```bash
docker tag my-app:latest \
  <account-id>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
```

### 5. Push to ECR

```bash
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
```

---

## 💡 Key Concepts Demonstrated

- **Private container registry** — images stored securely in AWS ECR, not public Docker Hub
- **IAM authentication** — uses AWS credentials to authenticate Docker, no static passwords
- **Image tagging strategy** — using `latest` and version tags for controlled deployments
- **ECR lifecycle policies** — can be configured to auto-expire old images and manage storage costs
- **Integration point** — ECR images consumed directly by ECS Fargate or Kubernetes deployments

---

## 🔗 Related Projects

- [AWS-ECS](https://github.com/tahoorshah/AWS-ECS) — Full-stack deployment on ECS Fargate using ECR images
- [jenkins-docker](https://github.com/tahoorshah/jenkins-docker) — Jenkins pipeline that builds and pushes Docker images

---

## 📝 Author

**Syed Tahoor Ali Shah**
- GitHub: [@tahoorshah](https://github.com/tahoorshah)
- Medium: [@tahoorshah](https://medium.com/@tahoorshah)
- LinkedIn: [syedtahooralishah](https://linkedin.com/in/syedtahooralishah)
