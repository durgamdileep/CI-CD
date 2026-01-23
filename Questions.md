## ❓ Q1. Can we run Jenkins pipelines without using Docker agents, directly on an EC2 instance?

- ✅ Yes, we can.
- Jenkins pipelines can be executed directly on EC2 instances by installing:
  - ☕ Java
  - 🛠️ Required build tools (Maven, Node, etc.)
  - 🤖 Jenkins agent on the EC2 instance

## ❓ Q2. What architecture is used when pipelines run directly on EC2 instances?

- 🏗️ This is called the **Jenkins Master–Agent (Controller–Agent) architecture**
- Architecture:

### 🧠 Jenkins Master (Controller):

- 📅 Schedules jobs  
- 🧩 Manages pipeline execution  
- 🚫 Does NOT run builds  

### ⚙️ Jenkins Worker Nodes (Agents):

- ☁️ Separate EC2 instances  
- 🏃 Execute the pipeline jobs  

## ❓ Q3. How does this architecture work in large organizations?

- 🏢 In large organizations (for example, 25 teams):
- 🤖 Jenkins Master distributes jobs to worker nodes
Example:
  - 🖥️ Worker Node 1 → Teams 1–10
  - 🖥️ Worker Node 2 → Teams 11–20
  - 🖥️ Worker Node 3 → Teams 21–25  
- 📌 The master only assigns jobs, while execution happens on worker nodes.

## ❓ Q4. What are the disadvantages of using EC2-based Jenkins worker nodes?

### 1️⃣ Idle Resource Wastage

- ⏸️ If no code changes occur:
  - Worker nodes remain idle
  - EC2 instances still running
- 💸 Leads to higher infrastructure cost

### 2️⃣ Dependency Version Conflicts

- 🧰 Each worker node has tools installed manually
Example:
  - Worker Node has Maven 3.6  
  - Jenkinsfile expects Maven 3.9  
  - ❌ Pipeline fails due to version mismatch

### 3️⃣ High Maintenance Effort

- 🔧 To fix dependency issues:
  - SSH into worker node (login into ec2 worknode)
  - Update tools manually
- 😓 Difficult to maintain across many nodes

### 4️⃣ Scalability Issues

- 📈 Adding more teams requires:
  - New EC2 instances
  - Manual setup
  - Tool installation and patching

## ❓ Q5. Why is this approach considered inefficient?

- ❌ Because it:
  - Wastes compute resources
  - Increases operational cost
  - Requires manual maintenance
  - Causes environment inconsistency
  - Does not scale efficiently

## ❓ Q6. Why is using Docker agents in Jenkins a better approach?

- 🐳 Docker agents solve all the above problems.

## ❓ Q7. How does a Jenkins Docker agent work?

- 📦 Docker image (e.g., Maven with a specific version) is defined in the Jenkinsfile
- During pipeline execution:
  - 🔍 Jenkins checks if the image exists
  - ♻️ If yes → reuse it
  - ⬇️ If no → pull/create a new container
  - 🏃 Pipeline runs inside the container
  - 🗑️ Container is destroyed after execution

## ❓ Q8. Advantages of using Docker agents

### 1️⃣ No Worker Node Maintenance

- 🧹 No need to manage tool versions on EC2
- 📄 Everything defined in Jenkinsfile

### 2️⃣ Version Consistency

- 📦 Same Docker image → same environment
- ✅ No “works on my machine” issues

### 3️⃣ Cost Effective

- ▶️ Containers start only when needed
- ⏹️ Stop after pipeline completion
- 💰 No idle EC2 instances

### 4️⃣ Easy Scalability

- 🔄 Spin containers on demand
- 🧩 Perfect for microservices and multiple teams

### 5️⃣ Faster Setup

- 🚫 No SSH, no manual installs
- ✍️ Change dependencies directly in Jenkinsfile

## 🧾 Final Conclusion

- ⚠️ Running Jenkins pipelines directly on EC2 worker nodes is possible but inefficient.
- ✅ Using Docker agents is the preferred and modern approach because it provides consistency, scalability, lower cost, and minimal maintenance.
