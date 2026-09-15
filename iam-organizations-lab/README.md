# AWS IAM & Organizations Governance Lab

## 📌 Project Overview
This project demonstrates secure identity management, least privilege access control, and multi-account governance using AWS Organizations. It covers IAM Users, Groups, Roles, custom JSON policies, and the IAM Policy Simulator. Based on hands-on labs from Adrian Cantrill's AWS SAA-C03 course.

---

## Phase 1: Identity Foundation & Least Privilege

### 🏗️ Architecture & Design Decisions
In this phase, I designed an identity structure based on **AWS Best Practices**:
*   **No Direct User Policies:** IAM policies are attached exclusively to Groups, not individual Users. This ensures scalability and easier access management.
*   **Least Privilege:** Custom JSON policies were written to grant only the minimum permissions required for a specific job function.
*   **Roles over Users:** An IAM Role was created for EC2 instances to avoid hardcoding long-term access keys on the server.

### 📸 Walkthrough & Screenshots
*(Note: Upload your actual screenshots to this folder and replace these text placeholders)*

**1. IAM Users and Groups Setup**
*   Created 3 users: `Alice-Admin`, `Bob-Dev`, `Charlie-Audit`.
*   Created 3 groups: `Admins`, `Developers`, `Auditors`.
*   *[Insert Screenshot: IAM Console showing Users and Groups]*

**2. Custom Least-Privilege Policies**
*   **Developers Policy:** Created a custom policy allowing `Bob-Dev` to start and stop EC2 instances, but *only* if the instance is tagged with `Environment: Dev`. 
    *   *[Insert Screenshot: JSON Policy Editor showing the Condition block]*
*   **Auditors Policy:** Created a custom policy allowing `Charlie-Audit` read-only access to IAM, CloudTrail, and Organizations to perform security audits.

**3. IAM Role for EC2 (PassRole)**
*   Created a role named `EC2-S3-ReadOnly-Role`.
*   **Trust Policy:** Configured to allow the EC2 service (`ec2.amazonaws.com`) to assume this role.
*   **Permissions:** Attached an S3 ReadOnly policy. 
*   *Why?* This eliminates the need to store AWS credentials on the EC2 instance itself.
    *   *[Insert Screenshot: Trust Relationship JSON for the EC2 Role]*

**4. Testing Least Privilege (IAM Policy Simulator)**
To prove the policies work as intended, I used the IAM Policy Simulator:
*   **Test Case A:** Simulated `ec2:StartInstances` for `Bob-Dev` on an instance tagged `Environment: Dev`. Result: **Allowed**.
*   **Test Case B:** Simulated `ec2:StartInstances` for `Bob-Dev` on an instance tagged `Environment: Prod`. Result: **Denied**.
    *   *[Insert Screenshots: Policy Simulator showing Allowed vs Denied]*

### 🛠️ Skills Demonstrated
*   AWS Identity and Access Management (IAM)
*   JSON Policy Writing (Condition blocks, Resource ARNs)
*   Least Privilege Principles
*   IAM Roles and Trust Policies
*   AWS Policy Simulator
