## 🚀 What is CI/CD?

CI/CD is a process used to automate building, testing, and delivering applications to customers.

### 🔁 CI – Continuous Integration
Continuous Integration means:

- 👨‍💻 Developers frequently push code to a shared repository  
- 🤖 Every code change is automatically built and tested  

---

## 🧩 CI Stages 

Different applications (web, mobile, backend) may have slightly different CI stages, but the core stages remain similar.

### 🛠️ Typical CI Pipeline Stages
- 📂 Source Code Management Checkout  
- 🏗️ Build & Unit Testing  
- 🔍 Static Code Analysis  
- 🛡️ Code Quality & Security Vulnerability Scan  
- 🤖 Automated Testing  
- 📊 Reports & Artifacts  
- 🐳 Docker Image Build  
- 🔐 Docker Image Security Scan  
- 🚀 Push Image and Update Helm Chart  

---

## 1️⃣ 📂 Source Code Checkout (SCM)

- Pull code from Git (GitHub, GitLab, Bitbucket)
- Triggered by:
  - ⬆️ Code push  
  - 🔀 Pull request / merge request  

---

## 🏗️ Build & Unit Testing

- 🔨 Compile the code (Java, Android, iOS, React, etc.)  
- 🧪 Run unit tests  
- ⚡ Fail fast if something breaks  

Examples:

- 🌐 Web: npm build, mvn package  
- 📱 Mobile: Gradle, Xcode build  

---

## 🧪 Unit Testing (Spring Boot)

Unit testing means:

- 🧩 Testing small pieces of code  
- 🔹 Example: one method, one class
- In Spring Boot:
  - ⚙️ We test service methods, utility methods, business logic  

### 🧰 Tools Used
- ✅ JUnit  
- ✅ Mockito  

### ❓ Why Unit Tests?

- 🐛 Catch bugs early  
- ✅ Ensure logic works correctly  
- ⚡ Fast to run  

### 🚫 What Unit Tests Do NOT Test

- 🗄️ Database  
- 🌐 API calls  
- 🔄 Full application flow  

---

## 3️⃣ 🔍 Static Code Analysis

- Analyze code without executing it
- Checks:
  - 💡 Code smells
  - 📊 Complexity
  - ♻️ Duplications
  - 📝 Coding standards  
- Tools:
  - 🔹 SonarQube
  - 🔹 ESLint
  - 🔹 Checkstyle  

- Static code analysis means:
  - 📖 Checking code without running the application . That’s why it is called static  

### ❓ How Can We Check Without Running?

- 🛠️ Tools read your source code like text and apply rules.
---

## 🧠 Code Issues Explained 

### 1️⃣ Code Issues

- Basic problems in code:
  - ❌ Unused variables
  - ❌ Unused imports
  - ❌ Duplicate code  

### 😕 Code Smells

- ⚠️ Code works, but not written in a good way.
- Examples:
  - 📝 Very large methods
  - 🔀 Too many if-else
  - 🔁 Same code repeated in many places  

- Problem:
  - 📉 Hard to read
  - 🛠️ Hard to maintain  

### ⚠️ Bad Coding Practices

- Wrong or risky ways of writing code:
  - 🔑 Hardcoding passwords
  - ❌ Not handling exceptions properly  

### ✅ Why Static Code Analysis is Important?

- 📖 Improves code readability  
- 🛠️ Makes code easy to maintain  
- 🐞 Prevents future bugs  

---

## 4️⃣ 🛡️ Code Quality & Security Vulnerability Scan

- This is usually combined or parallel with static analysis.
- Checks:
  - ✅ Code quality gates
  - 🔓 Security vulnerabilities
  - 📦 Dependency vulnerabilities (open-source libraries)  

- Tools:
  - 🔹 SonarQube
  - 🔹 Snyk
  - 🔹 OWASP Dependency Check
  - 🔹 Trivy  

---

## 🅰️ A) Code Quality – What Do We Check?

Code quality means:

- ✨ Is the code clean?  
- 🧩 Is it easy to understand?  
- 🛠️ Is it maintainable?  

### 📏 Code Quality Checks

- 📊 Code coverage (how much code is tested)  
- ♻️ Duplicate code  
- 📐 Method complexity  
- 📝 Coding standards  

Example:

- ⚠️ If coverage < 80%, pipeline fails  
 

---

## 🅱️ B) Security Vulnerability Scan

### 🔓 What is a Security Vulnerability?

A weakness that attackers can use to:

- 🕵️ Steal data  
- 💥 Break the application  

### 🧨 Common Security Issues in Spring Boot

1. 🛠️ SQL Injection  
   - Problem: Hacker can inject SQL  
2. 🔑 Hardcoded Secrets  
3. 📦 Insecure Dependencies  
   - Using old libraries with known vulnerabilities  

---

## 🔎 How Do We Find Security Issues?

### 1️⃣ Code Scan

- 🛠️ Tools analyze code patterns  
- 🔹 Example: SonarQube  

### 2️⃣ Dependency Scan

- 📄 Checks pom.xml  
- 🔍 Finds vulnerable libraries
- 🔹 OWASP Dependency Check  

---

## 5️⃣ 🤖 Automated Testing

- 🔄 Integration tests  
- 🌐 API tests  
- 🖥️ UI tests (optional in CI)  

Tools:

- 🔹 Selenium  
- 🔹 Cypress  
- 🔹 JUnit  
- 🔹 TestNG  

⚠️ These tests are often limited in CI to keep pipelines fast.

---

## ❓ Question: We already have Unit Tests. Why Automated Tests?

Answer:

- 🧩 Unit tests test small pieces  
- 🔄 Automated tests test how everything works together  

---

## ⚖️ Unit Test vs Automated Test (Very Simple)

| Unit Test | Automated Test |
|---------|---------------|
| 🧩 Tests single method | 🔄 Tests full flow |
| 🗄️ No DB | 🏗️ Uses DB |
| 🌐 No API calls | 🖥️ Calls APIs |
| ⚡ Very fast | 🐢 Slower |
| 👨‍💻 Developer focused | 🧑‍💻 User flow focused |

---

## 🧪 What Do We Test in Automated Testing?

In Spring Boot:

- 🌐 REST APIs  
- ⚙️ Service + Repository + DB  
- 🔄 End-to-end application flow  

### 🧑‍💻 Example

User Flow:

- 👤 User calls Create User API  
- 🗄️ Data saved in database  
- 📤 Response returned  

Automated test checks:

- 🌐 API response  
- 🗄️ DB entry  
- 📊 HTTP status code  

Tools Used:

- 🔹 Spring Boot Test  
- 🔹 REST Assured  
- 🔹 TestContainers  

---

## ❓ Why Can’t We Do This in Unit Tests?

Because unit tests:

- ❌ Do NOT start full application  
- ❌ Do NOT test DB and API together  
- ❌ Do NOT test real user flow  

---

## 📊 Reports & Artifacts

- 📄 Test reports  
- 📊 Code coverage reports  
- 📦 Build artifacts (WAR, APK, IPA, Docker image)  

Artifacts are stored in:

- 🗄️ Nexus  
- 🗄️ Artifactory  
- 🐳 Container registry  

---

## 📑 A report is a result or summary of what happened in the CI pipeline.

- 👀 Reports do not run the application  
- 📖 Reports are for humans to see and understand  

### 1️⃣ Unit Test Report

Shows:

- ✅ How many tests passed  
- ❌ How many failed  
- ⏱️ How long tests took  

### 2️⃣ Code Coverage Report

Shows:

- 📊 How much code is covered by tests  

### 3️⃣ Static Code Analysis Report

Shows:

- ⚠️ Code issues  
- 💡 Code smells  
- 🔓 Security hotspots  

### 4️⃣ Security Scan Report

Shows:

- 🕵️ Vulnerabilities in code and libraries  

---

## ⭐ Why Reports Are Important?

- 👀 Helps developers understand problems  
- ✅ Helps team decide whether to move forward  
- 📝 Used for audits and quality checks  

---

## 📦 What is an Artifact?

An artifact is the output file created after building the application.

- 🖥️ Artifacts are used by machines  
- 🚀 Artifacts are deployed  

---

## 📦 Examples of Artifacts (Spring Boot)

1️⃣ JAR / WAR File  
- ⚙️ Final Spring Boot build output  

2️⃣ Docker Image  
- 🐳 Application packed inside a container  

3️⃣ Helm Chart Package  
- ☸️ Kubernetes deployment package  

4️⃣ Configuration Files  
- ⚙️ Deployment-ready files  

---

## 🗄️ Where Are Artifacts Stored?

- 🗄️ Nexus  
- 🗄️ Artifactory  
- 🐳 Docker Hub  
- 🐳 Container Registry  

---

## 🔄 Difference Between Report and Artifact 

| Report | Artifact |
|------|---------|
| 📄 Shows results | ⚙️ Is the final output |
| 👀 For humans | 🚀 For deployment |
| 📖 Read-only | 🖥️ Used in CD |
| 📊 Examples: test report | 📦 Examples: JAR, Docker image |

---

## 🔗 How Reports and Artifacts Fit in CI/CD

CI:

- 📄 Generates reports  
- 📦 Creates artifacts  

CD:

- 🚀 Uses artifacts  
- ❌ Ignores reports (except for approval)  

---

## 🧩 How Junit, Jacoco and sonarQube Work Together

- 📝 You write tests using JUnit  
- ✅ JUnit runs the tests  
- 📊 JaCoCo tracks which lines of code were executed  
- 🔍 SonarQube reads JaCoCo report  

---

## 📋 Simple Table 

| Tool | Purpose |
|----|--------|
| ✅ JUnit | Write & run tests |
| 📊 JaCoCo | Measure code coverage |
| 🔍 SonarQube | Analyze code & show coverage |
