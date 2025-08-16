---
layout: page
title: NLP to SQL Queries
description: Plain english to SQL queries to interact with database deployed on AWS using EKS.
img: assets/img/1.png
importance: 1
---
**GitHub Repository:** [View on GitHub](https://github.com/itsAshna/nlp-to-sql-queries)

---

#### Introduction
This project demonstrates how to build and deploy a FastAPI application that translates natural language questions into SQL queries and runs them against a dataset hosted in Amazon Athena. The entire pipeline is containerized, stored in Amazon ECR, and deployed on an AWS EKS cluster, accessible via a public endpoint.

---

#### Problem
Data analysts and non-technical stakeholders often struggle to query data if they don’t know SQL. A natural language interface can bridge this gap, allowing anyone to get insights from data using plain English.
 In this service, users can type a question in plain English (e.g., “Show me all products ordered in July”), and the system generates the corresponding SQL query, executes it against the database, and returns the results in a CSV file - all without touching SQL.

---

#### Approach
1. **Application Development**
   - Built with **FastAPI** to handle HTTP requests.
   - Integrated **OpenAI API** to translate natural language into SQL queries.
   - Connected to **Amazon Athena** to execute SQL queries on S3-hosted data.

2. **Containerization**
   - Created a multi-architecture Docker image supporting **amd64** and **arm64**.
   - Stored images in **Amazon ECR**.

3. **Continuous Integration & Deployment**
   - Used **GitHub Actions** to automate:
     - Building the Docker image.
     - Pushing it to ECR.
     - Deploying updates to EKS.

4. **Infrastructure**
   - Deployed on an **AWS EKS** cluster.
   - Exposed via a LoadBalancer service to get a public URL.

---

#### Results
- Successfully deployed a public API where users can send natural language questions and receive SQL results.
- Achieved end-to-end automation from code commit to deployment.
- Validated scalability on AWS infrastructure.

---

#### Challenges
- **GitHub Actions not triggering** due to missing workflow events.
- **Docker architecture mismatch** (built on ARM Mac, deployed on AMD AWS nodes).
- **OpenAI API quota issues** causing runtime errors.
- **Kubernetes CrashLoopBackOff** errors due to missing environment variables.
- **Cost management** — keeping EKS running racks up charges quickly.

---

#### How I Solved
- Added `on: push` triggers in GitHub Actions to automate builds.
- Used `--platform linux/amd64` in Docker builds to match AWS node architecture.
- Stored sensitive credentials (OpenAI API key, AWS creds) in GitHub Secrets and Kubernetes secrets.
- Implemented cleanup scripts to delete EKS clusters, ECR repos, and S3 data to avoid extra costs.

---

#### Conclusion
This project demonstrates the full lifecycle of deploying an NLP-to-SQL application in the cloud, from local development to production deployment on AWS. It also highlights the importance of CI/CD, cross-platform containerization, and cost management.

---

#### Future Improvements
- Implement caching to reduce repeated OpenAI calls and save on API costs.
- Add authentication and rate-limiting for the public API.
- Expand support for multiple databases beyond Athena.
- Enhance natural language processing for more complex queries.
- Add monitoring and logging dashboards using AWS CloudWatch and Grafana.

