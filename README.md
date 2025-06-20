# 🚀 Node.js CI/CD Workflow with Docker

This repository demonstrates a GitHub Actions workflow that automates the CI/CD process for a Node.js project, including Docker image build and push to a private container registry.

---

## 🔧 What This Workflow Does

This CI/CD workflow is triggered on:
- Push to the `dev` branch
- Pull requests targeting the `dev` branch

The workflow performs the following steps:
1. **Checks out the latest code**
2. **Installs Node.js dependencies**
3. **Builds a Docker image** using the project source
4. **Pushes the Docker image** to a custom container registry

---

## 📄 Workflow File Location

`.github/workflows/node-ci.yml`

```yaml
name: Node.js CI

on:
  push:
    branches: [ "dev" ]
  pull_request:
    branches: [ "dev" ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Install Node.js dependencies
      run: npm install

    - name: Build Docker image
      uses: docker/build-push-action@v2
      with:
        context: .
        push: false
        tags: registry.sofit.ltd/delete-me:dev

    - name: Push Docker image to registry
      uses: docker/build-push-action@v2
      with:
        context: .
        push: true
        tags: registry.sofit.ltd/delete-me:dev
