
💡 **Let's simulate a real-world GitHub Flow & Automation setup!**  

---

### **🔥 Scenario: You’re working on a real organization project!**  

✅ **Main Branch (`main`)** → Stable production code.  
✅ **Development Branch (`dev`)** → All new features/bug fixes are merged here before going to `main`.  
✅ **Feature Branches (`feature-xyz`)** → Individual work happens here.  
✅ **Automations:**  
   - **GitHub Actions** for CI/CD (Run tests automatically).  
   - **GitHub API** to automate PR reviews and issue tracking.  
   - **GitHub Secrets** to securely store API keys.  

---

### **📌 Step 1: Set Up the Repository & Branches**  
Since you've already created a repository with `README.md`, let's create the branches for GitHub Flow.  

```sh
# Ensure you are on the main branch
git checkout main  

# Create and switch to a development branch
git checkout -b dev  
git push -u origin dev  

# Create a feature branch for a new feature
git checkout -b feature-login  
git push -u origin feature-login  
```

---

### **📌 Step 2: Automate Code Quality Checks (GitHub Actions)**  
🔹 **Add CI/CD automation** using GitHub Actions to check code quality every time a PR is opened.  

📂 Create a new directory: `.github/workflows/ci.yml`  
```yaml
name: CI Check

on:
  pull_request:
    branches:
      - dev

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      - name: Run Code Linter
        run: echo "Running Code Quality Check ✅"
```

🔹 **What happens?**  
✅ Every time a developer creates a **Pull Request (PR)** to `dev`, the **CI check runs** automatically.  

---

### **📌 Step 3: Automate Issue Creation for Failed CI Tests**  
🔹 **Use GitHub API to create an issue if the test fails.**  
Add this step to the **GitHub Action (`ci.yml`)**:  

```yaml
- name: Create Issue on CI Failure
  if: failure()
  run: |
    curl -X POST -H "Authorization: token ${{ secrets.GITHUB_TOKEN }}" \
         -H "Accept: application/vnd.github.v3+json" \
         -d '{
               "title": "⚠️ CI Test Failed",
               "body": "The latest PR failed the CI check. Please investigate.",
               "labels": ["bug"]
             }' \
         https://api.github.com/repos/${{ github.repository }}/issues
```

🔹 **What happens?**  
✅ If the CI test fails, an **issue is automatically created** in the repo.  

---

### **📌 Step 4: Merge Feature Branch to Development**  
🔹 **After feature completion, merge it into `dev`**:  
```sh
git checkout dev  
git merge feature-login  
git push origin dev  
```
✅ **CI/CD will trigger and run automated tests.**  

---

### **📌 Step 5: Deploy to Production Automatically**  
🔹 **Once the `dev` branch is stable, merge it into `main` to deploy:**  
```sh
git checkout main  
git merge dev  
git push origin main  
```
🔹 **Add a GitHub Action to Deploy to Production (`deploy.yml`)**:  
```yaml
name: Deploy to Production

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Deploy Application
        run: echo "Deploying Application 🚀"
```
✅ **Every time `main` is updated, the app is deployed automatically.**  

---

### **📌 Step 6: Secure the Repository Using GitHub Secrets**  
🔹 **Store API keys securely instead of hardcoding them.**  
```sh
gh secret set API_KEY --body "your-secure-api-key"
```
🔹 **Access the secret inside workflows:**  
```yaml
run: echo "Using API Key: ${{ secrets.API_KEY }}"
```

---

### **🚀 Final Workflow Summary:**  
✔ **Developers work on `feature-*` branches and push commits.**  
✔ **Pull Requests to `dev` trigger automated CI/CD checks.**  
✔ **CI failures create issues automatically.**  
✔ **Stable `dev` branch is merged into `main`, triggering deployment.**  
✔ **GitHub Secrets store sensitive API keys securely.**  
 