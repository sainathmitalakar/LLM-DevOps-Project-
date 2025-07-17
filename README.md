# LLM DevOps Project

This project is a demo of deploying a GPT-2-based LLM API using DevOps tools like Jenkins, Docker, Kubernetes, and optionally Helm.

## Tech Stack
- Python (Flask + Huggingface Transformers)
- Docker
- Jenkins
- Kubernetes
- Helm (optional)

## Steps to Run

### 1. Build Locally
```bash
docker build -t llm-devops .
docker run -p 5000:5000 llm-devops
```

### 2. Kubernetes Deployment
```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### 3. Jenkins Pipeline
Setup credentials and run Jenkinsfile for CI/CD.

### 4. Helm (Optional)
```bash
helm install llm-chart helm-chart/
```

## API Endpoint

POST /generate
Payload:
{
  "prompt": "Once upon a time"
}
