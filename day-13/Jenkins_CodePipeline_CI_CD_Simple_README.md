# 🧾 CI/CD Notes — Jenkins & AWS CodePipeline (Very Simple)

This is a **super simple** guide to understand **CI** and **CD** with **Jenkins** and **AWS CodePipeline**.

---

## 🧠 Quick Definitions

- **CI (Continuous Integration)**: Automatically **build + test** code whenever you push.
- **CD (Continuous Delivery/Deployment)**: Automatically **deploy** code to **dev/stage/prod** after CI passes.

---

## 🔧 Jenkins (focus on CD)

**Jenkins** is a server that runs jobs (pipelines) you define in a **Jenkinsfile**.

### What we do in Jenkins
- **Implementing CD**: Jenkins connects to your servers/cloud and **deploys** the app.
- **Invoke CD**: Press a button or trigger after CI to run the **deploy stage**.

### Super simple Jenkins pipeline (CD idea)
```groovy
pipeline {
  agent any
  stages {
    stage('Deploy') {
      steps {
        echo 'Deploying to production...'
        // e.g., kubectl apply -f k8s.yaml
        // or aws deploy create-deployment ...
      }
    }
  }
}
```

> Tip: Jenkins can also do CI, but many teams use it mainly to **deploy** (CD), especially if CI happens in GitHub/GitLab.

---

## ☁️ AWS CodePipeline (CI + CD)

**CodePipeline** is AWS’s managed pipeline service. It can run both **CI** and **CD**.

### What we do in CodePipeline
- **Invoking CI**: Pull code from **Source** (GitHub/CodeCommit) → run **Build** (CodeBuild) → run tests.
- **Invoking CD**: After build/tests pass, **Deploy** to **Lambda/ECS/EC2/CloudFormation**.

### Super simple CodePipeline flow
```
Source  →  Build  →  Deploy
 (Git)     (CI)      (CD)
```

### Minimal example (concept)
- **Source**: GitHub repo
- **Build**: CodeBuild (runs `npm test`, `mvn package`, etc.)
- **Deploy**: CloudFormation stack or ECS service update

---

## ✅ When to use what? (simple view)

| Task | Jenkins | CodePipeline |
|-----|---------|--------------|
| Run deployment steps to servers / K8s | ✅ Great (CD) | ✅ Good (via CodeDeploy/ECS/CFN) |
| Managed service (no server to maintain) | ❌ You manage Jenkins | ✅ AWS manages |
| Easy connect to AWS services | ⚠️ Needs plugins/creds | ✅ Native integration |
| CI builds & tests | ✅ Can do | ✅ Built-in with CodeBuild |

---

## 🧩 Common Triggers

- **On push to branch** (main/dev)
- **On PR merge**
- **Manual approve step** before production deploy

---

## 🏁 TL;DR

- **Jenkins** → Think **CD**: run your **deploy** steps reliably.
- **CodePipeline** → Think **CI + CD** in AWS: **build**, **test**, and **deploy** in one place.

That’s it. Keep it simple: **Build → Test → Deploy**.
