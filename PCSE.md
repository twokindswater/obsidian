---
cssclasses:
  - my_style_width_100
---

Problems

Google

- need centralized management and access data store → set up Cloud Identity and use those accounts for google cloud work
- customer want to use non-google cloud SaaS and want to use SSO. → third-party application to federate auth/authz to google cloud IdP(identity provider)
- Team need to use service accounts. provide service account to team. what is recommended practices? → Implement daily key rotation process and provide with cloud storage bucket from which they can download the new key every day.
- customer need to maintain there auth solution. it is familiar interface. → configure cloud identity as a SAML 2.0 service provider
- team create firewall rule to allow ssh access. but that also cannot access unauthorized user. → **create firewall rule with target of service account.**
- protect default VPC from all inbound and outbound internet traffic → **inbound is already blocked default**. so create deny all outbound firewall rule.
- **Cloud IAP**(identity-Aware Proxy) to manage authentication and different authorization levels for employee access.
- Create a regular expression (regex) custom infoType detector to match on pattern.
- Cloud storage default encryption → **AES-256**
- uploaded files cannot be deleted within first 5 years. it should not be possible to lower the retention period after it has been set → Apply a retention period and **lock the bucket.**
- Container images contain the latest security patch → **google-managed based images**
- deployment polices → deployment policies define in **Binary Authorization** ensure that only trusted images can be deployed in GKE.
- Vulnerability scanning can be performed by **container analysis** to discover package vulnerability information in container base image.
- Personally identifiable information (PII)
- **Cloud Data Loss Prevention(DLP)** can be used to inspect data(discover important data), protect data(masking)
- Customer-managed encryption keys(CMEK), Customer-supplied Encryption keys(CSEK)
- PCI DSS(Payment Card Industry Data Security Standard)
- Active Directory: microsoft auth program
- **Cloud interconnect** : 지연 시간이 짧고 가용성이 높은 연결을 제공, 내부 IP 주소 통신

| 기능  | Dedicated Interconnect | Partner Interconnect |
| --- | ---------------------- | -------------------- |
| 속도  | ~200Gbps               | 50Mbps~50Gbps        |
- 인증 

| 기능  | Identity-Aware Proxy (IAP)                     | Context-Aware Access                                |
| --- | ---------------------------------------------- | --------------------------------------------------- |
| 목적  | IAP는 웹 애플리케이션 및 VM 인스턴스에 대한 액세스를 보호            | 접근 제어를 더 세밀하게 설정                                    |
| 인증  | google 계정을 사용하여 인증하고, IAM 정책을 통해 접근 권한을 제어합니다. | 사용자 인증 외에도, 위치, 기기 보안 상태, IP 주소, 시간대 등의 컨텍스트 정보를 기반 |

---

Udemy

- GCP has 2 different network service.
    - Standard Tier network : use public network, cost efficiency, normal latency, backend랑 동일한 region에서만 가능
    - Premium Tier network : use backbone network, high cost, low latency, fast
- It is recommended to isolate VMs using service accounts whenever possible → **vm마다 service account를 mapping 할 수 있음**
- **Web security scanner** can help you find security problems. automatically scan and detect common security vulnerabilities.
- **firewall 설정할때 특정 service account 를 allow/deny 할 수 있음.**
- Cloud Armor에는 정책을 update 하기 전에 impact을 미리 볼 수 있는 preview-mode 를 지원함.

| 기능     | VPC Flow Logs                   | Packet Mirroring       | Cloud Audit Logs          |
| ------ | ------------------------------- | ---------------------- | ------------------------- |
| 캡처 데이터 | VPC 내부 네트워크 트래픽 메타데이터           | 네트워크 패킷 데이터            | API 호출 및 리소스 변경           |
| 사용 사례  | 성능 모니터링(기본적인 분석), 보안 분석, 비용 최적화 | 심층 보안 분석, 성능 모니터링      | 컴플라이언스, 보안 분석, 변경 관리      |
| 특징     | 실시간 로그 수집, 로그 분석 도구 통합          | 실시간 패킷 캡처, 외부 분석 도구 통합 | 모든 API 호출 추적, 로그 분석 도구 통합 |

- **Access transparency log** 는 google의 운영자가 고객의 콘텐츠에 접근할 때마다 그 활동을 기록하는 로그입니다.
- **Deterministic encryption**은 동일한 입력 값에 대해 항상 동일한 암호 텍스트를 생성하는 암호화 방법입니다.
- Control rotation schedules for encryption keys → customer-managed encryption key, google managed encryption key는 rotation을 내가 설정할 수 없음.

| 특징/장점/단점  | Google-managed encryption keys | Customer-managed encryption keys (CMEK) |
| --------- | ------------------------------ | --------------------------------------- |
| 키 회전 및 폐기 | 자동                             | 사용자 설정                                  |


- To avoid individual management of access for each object →Uniform bucket-level access

|특징/장점/단점|Uniform bucket-level access|Individual management using ACLs|
|---|---|---|
|object access control|일관된 보안 정책|객체마다 다른 권한 설정 가능|

- GKE에서 돌아가는 container image는 immutable하기 때문에 security update or patch가 필요하면 apply patch하고 build new image and redeploy가 필요함.
- Front end instance 에만 public ip를 허용하고 싶을때 → Create **Organization policy** → Apply policy to front-end instances → restrict back-end access
- with **Firewall Insights** we can identify firewall rules overlapping with attributes from other rules having equal or higher priority.
- **ISO 27017** is an international standard that provides guidelines for information security controls applicable to the provision and use of cloud services
- Policy Analyzer 정책 분석 도구를 사용하면 IAM 허용 정책에 따라 어떤 주 구성원(예: 사용자, 서비스 계정, 그룹, 도메인)이 어떤 Google Cloud 리소스에 대해 어떤 액세스 권한을 갖는지에 관한 정보를 확인할 수 있습니다.
- scan 비용을 줄이기위해 → CloudStorageRegexFileSet 와 같은 정규식 표현으로 scan data를 줄인다.
- authentication with third-party SSO SAML identity provider can be accomplished if the third-party **IdP** supports **SAML** and **OIDC protocols.**
- The concept of encrypting all cache storage and VM-to-VM communication using the **BoringCrypto** module involves implementing a secure, cryptographic library to ensure that all data stored in cache and all data transmitted between virtual machines (VMs) is encrypted.
- In the Infrastructure as a Service (IaaS) model on Google Cloud Platform (GCP),

|특징/장점/단점|GCP|Customer|
|---|---|---|
|responsibilities|Infrastructure, physical, compute, storage, networking|Access policy, network security, data security, IAM|

- Use the **Transfer Tool for Unmanaged Users (TTUU)** to find users with conflicting accounts and ask them to transfer their personal Google accounts.
- Use **Google Cloud Directory Sync** to synchronize your local identity management system to Cloud Identity.
- Defending against XSS and SQLi attacks is the correct answer because in **Platform-as-a-Service model** (PaaS), the customer assumes responsibility for web app security, deployment, usage, access policy, and content.
- **Secret Manager** is a secure and convenient storage system designed for API keys, passwords, certificates, and other sensitive data. It serves as a centralized platform and single source of truth for efficiently managing, accessing, and auditing secrets throughout Google Cloud.
- DNSSEC(Domain Name System Security Extensions)는 **IP(Internet Protocol) 네트워크를 통해 전송되는 데이터의 보안을 위해 DNS 레코드에 추가되는 암호화 서명**
- service account가 실수로 지워지면 undeleted command로 살릴 수 있음
- PCI (personal credit information) PCI DSS(Payment Card Industry Data Security Standard)
- PII (Personal Identifiable Information)
- _**SIEM**_(Security Information and Event Management)

| 기능/특징 | Cloud VPN                                                         | Shared VPC                        | VPC Peering                           |
| ----- | ----------------------------------------------------------------- | --------------------------------- | ------------------------------------- |
| 설명    | 온프레미스 네트워크 또는 다른 클라우드 제공자의 네트워크를 GCP의 VPC 네트워크에 안전하게 연결할 수 있는 서비스 | GCP 프로젝트 간에 VPC 네트워크를 공유할 수 있는 기능 | 두개의 GCP VPC 네트워크를 상호 연결하여 서로의 리소스에 접근 |
| 주요 용도 | 온프레미스 네트워크 연결                                                     | 여러 프로젝트 간 네트워크 공유                 | VPC 네트워크 간 상호 연결                      |

| 기능/특징       | network security               | cloud armor                |
| ----------- | ------------------------------ | -------------------------- |
| 목적          | 네트워크 레벨 보안 및 관리                | 웹 애플리케이션 방어 및 DDoS 방어      |
| 구성 요소 및 서비스 | VPC 방화벽, Cloud VPN, IAM, IAP 등 | WAF 규칙, DDoS 방어, 맞춤형 보안 정책 |



[examtopics](https://www.notion.so/examtopics-d91833db80764dce9a8956d7bfd38914?pvs=21)

---

Q. To establish a Cloud Interconnect connection between your company's on-premises data center and VPC host network, with the aim of restricting on-premises applications to access Google APIs exclusively via **Cloud Interconnect** and not through the public internet, while ensuring usage of only VPC Service Controls-supported APIs to mitigate exfiltration risk to non-supported APIs, what network configuration should you implement?

A. **Use restricted [googleapis.com](http://googleapis.com) to access Google APIs using a set of IP addresses only routable from within Google Cloud, which are advertised as routes over the Cloud Interconnect connection.**

Q. How should your team structure the network to ensure that only the frontend application can access the backend database, with no access granted to other instances on the network?

A. **Create an ingress firewall rule to allow access only from the application to the database using firewall tags.**

Q. You are tasked with establishing a connection between your organization's on-premises network and an existing Google Cloud environment, featuring a Shared VPC with Production and Non-Production subnets. Your requirements are as follows:

- Utilize a private transport link.
- Set up access to Google Cloud APIs through private API endpoints originating from on-premises environments.
- Ensure that Google Cloud APIs are exclusively accessed via VPC Service Controls. How would you proceed?

A.**1. Set up a Dedicated Interconnect link between the on-premises environment and Google Cloud.**
**2. Configure private access using the [restricted.googleapis.com](http://restricted.googleapis.com) domains in on-premises DNS configurations.**

Q. Your team is tasked with organizing the Google Cloud Platform (GCP) environment to consolidate control over networking components such as firewall rules, subnets, and routes. Additionally, there is an on-premises infrastructure requiring connectivity to GCP resources through a private VPN connection. The network security team is responsible for overseeing these networking resources. What type of networking design should your team employ to fulfill these requirements?

A. **Shared VPC Network with a host project and service projects**
centralize the control → Shared VPC

Q. To balance the load across multiple instances running the application and ensure a secure **TLS connection** terminated by the Load Balancer for an application implemented on Compute Engine, accessed by clients on port 587, which type of Load Balancing should be utilized?

A. **SSL Proxy Load Balancing**

Q. As the manager of your organization's Security Operations Center (SOC), you oversee the monitoring and detection of network traffic anomalies in Google Cloud VPCs, primarily based on **packet header information.** However, you aim to enhance your investigative capabilities by exploring network flows and their payloads. Which Google Cloud product would best serve this purpose?

A. **Packet Mirroring**

Q. You've recently acquired a new workload, and the Web and Application (App) servers are set to operate on Compute Engine within a freshly established custom VPC. Your task is to implement a secure network communication solution that adheres to the following specifications:

- Restrict communication exclusively between the Web and App tiers.
- Ensure uniform network security when autoscaling the Web and App tiers.
- Preclude Compute Engine Instance Admins from modifying network traffic.

What steps should you take to achieve this?

A.
**1. Re-deploy the Web and App servers with instance templates configured with respective service accounts.**
**2. Create an allow VPC firewall rule that specifies the target/source with respective service accounts.**

Q. Which load balancer type should you employ to retain client IP by default while utilizing the standard network tier?

A. **TCP/UDP Network**
ALB는 client ip를 x-forwarded-for header에 포함시키고, 자신의 ip를 overwrite해서 보냄

Q.How should you structure the network to examine all traffic between two network segments, one designated as untrusted and the other as trusted, using a virtual appliance like a next-generation firewall (NGFW)?

A.
**1. Set up two VPC networks: one trusted and the other untrusted.**
**2. Configure a virtual appliance using multiple network interfaces, with each interface connected to one of the VPC networks.**

Q. Your company is using Cloud Storage to store sensitive documents. The compliance team requires that data at rest is encrypted and that access to the data is audited. Which configuration should be applied to meet these requirements?

A. **Use Customer-Managed Encryption Keys (CMEK) for Cloud Storage**

Q. While developing an internal App Engine application that requires access to a user's Google Drive without relying on the user's current credentials, your company aims to follow Google-recommended practices. What approach should you take?

A. **Create a new service account, and grant it G Suite domain-wide delegation. Have the application use it to impersonate the user.**

Q. Which mode of VPC Service Controls should you employ when enabling it and allowing changes to perimeters in existing environments without obstructing access to resources?

A. **Dry Run**

Q. To comply with PCI DSS requirements, a client seeks tol enforce authorization for all outgoing traffic. Which two cloud services fulfill this demand without requiring supplementary compensating measures? (Select two.)

A. Compute Engine
Cloud Function

Q. In handling protected health information (PHI) for an electronic health record system, the privacy officer is apprehensive about sensitive data storage in the analytics system. Your responsibility is to anonymize the sensitive data in a manner that is **non-reversible** and ensures that the anonymized data does not retain the character set and length. What Google Cloud solution should you employ?

A. **Cloud Data Loss Prevention with cryptographic hashing**

Q. Your organization is implementing a Zero Trust security model and wants to ensure that only authorized users with the right **devices** can access resources in Google Cloud. Which GCP feature should be used to enforce device-based access controls for users?

A. **Context-Aware Access**

Q. How can you address the error indicating that log sinks do not support uniform bucket-level access policies when exporting application logs to Cloud Storage?

A. **Change the access control model for the bucket**

Q. As a security administrator within your organization, you have implemented the domain restricted sharing organization policy following Google-recommended best practices to restrict access to only necessary domains. However, the engineering team has encountered an issue where users from an external partner, outside the organization's domain, cannot be granted access to project resources. How can you create an exception for your partner's domain while adhering to the established best practices?

A. **Turn off the domain restricted sharing organization policy. Set the policy value to "Custom." Add each external partner's Cloud Identity or Google Workspace customer ID as an exception under the organization policy, and then turn the policy back on.**

Q. What is the recommended approach for a customer to consistently transfer Stackdriver logs from Google Cloud Platform (GCP) to their on-premises Security Information and Event Management (SIEM) system?

A. **Configure Organizational Log Sinks to export logs to a Cloud Pub/Sub Topic, which will be sent to the SIEM via Dataflow.**

Q.You aim to safeguard against unintentional deletion of a Shared VPC host project. Which organization-level policy constraint should be activated?

A. **compute.restrictXpnProjectLienRemoval**

Q. How can you enhance the security of your CI/CD cluster hosted on Compute Engine to minimize the risk of unauthorized access to its credentials by a third party?

A. **Create a custom service account for the cluster. Enable the constraints/iam.disableServiceAccountKeyCreation organization policy at the project level**

Q.Your organization is adopting a microservices architecture on GCP, and you want to ensure secure communication between microservices running in **different clusters**. Which GCP service can you leverage to establish a private and secure connection between these microservices?

A. **Anthos Service Mesh**

Q. How can you ensure that an external user cannot access the application, even in the event of a compromised employee password, when your company is using GSuite and has developed an internal-use application on Google App Engine?

A.**Enforce 2-factor authentication in GSuite for all users.**

Q. What steps should be taken to investigate and confirm the functionality of firewall rules on a Compute Engine-hosted public-facing application when users report an outage, and recent changes to firewall rules are suspected to be the cause?

A. **Enable Firewall Rules Logging on the latest rules that were changed. Use Logs Explorer to analyze whether the rules are working correctly.**

Q. A large e-retailer is moving to Google Cloud Platform with its ecommerce website. The company wants to ensure payment information is **encrypted between the customer's browser and GCP** when the customers checkout online. What should they do?

A. **Configure an SSL Certificate on an L7 Load Balancer and require encryption.**

Q. In a scenario where an organization is experiencing a rise in phishing emails, what approach should be employed to safeguard employee credentials?

A. **Multifactor Authentication**

Q. As a member of the security team in an organization, tasked with securing a GCP project that includes credit card payment processing systems, web applications, and data processing systems, your goal is to **minimize the scope** of systems subject to PCI audit standards. What steps should you take to achieve this objective?

A. **Move the cardholder data environment into a separate GCP project.**

Q. When engaging with support center agents through online chat, customers frequently provide images of their documents containing personally identifiable information (PII). The organization operating the support center is apprehensive about PII being stored in their databases within regular chat logs, which are retained for analysis by internal or external analysts to identify customer service trends. To address this concern and uphold data utility, which Google Cloud solution should the organization employ?

A. **Use the image inspection and redaction actions of the DLP API to redact PII from the images before storing them for analysis.**

Q. Your multi-cloud environment involves integrating on-premises systems with GCP resources. To ensure private transport links and control access to GCP APIs through private API endpoints originating from on-premises environments, which hybrid networking solution should you implement?

A. dedicated interconnect

Q. A customer's organization comprises multiple business units, each functioning autonomously with its own engineering group. Our team aims to gain visibility into all company projects and seeks to structure Google Cloud Platform (GCP) projects according to distinct business units. Additionally, each business unit requires its own specific sets of IAM permissions.

A. **Create an organization node, and assign folders for each business unit.**

Q. You are assigned the responsibility of exporting and auditing security logs for login activity events in the Google Cloud console and API calls that modify configurations to Google Cloud resources. The export must adhere to the following specifications:

- Export logs for all projects within the Google Cloud organization.
- Export logs in near real-time to an external SIEM.

What actions should you take? (Choose two.)

A. **Create a Log Sink at the organization level with the includeChildren parameter, and set the destination to a Pub/Sub topic.**
**Enable Google Workspace audit logs to be shared with Google Cloud in the Admin Console.**

Q. How can your team centrally manage Google Cloud Platform (GCP) IAM permissions through their on-premises Active Directory Service, specifically focusing on permission management based on Active Directory group membership?

A. **Set up Cloud Directory Sync to sync groups, and set IAM permissions on the groups.**

Q. As a member of the security team, tasked with minimizing the external attack surface of the Linux bastion host by eliminating public IP addresses, you need to provide Site Reliability Engineers (SREs) with access to the bastion host from public locations for off-site access to the internal VPC. What is the recommended approach to enable this access?

A. **Implement Identity-Aware Proxy TCP forwarding for the bastion host.**

Q. Your company is deploying a critical application on Google Kubernetes Engine (GKE), and the security team is concerned about potential runtime vulnerabilities in the container images. What GCP service or tool should be integrated into the CI/CD pipeline to perform automated security scanning of container images during the build process

A. **Container Registry Vulnerability Scanning**

Q. To assess GCP for PCI compliance and identify Google's inherent controls, which document should you consult for the relevant information?

A. **Google Cloud Platform: Customer Responsibility Matrix**

Q. You aim to restrict the selection of images eligible for use as boot disks, and these images will be housed in a dedicated project. What course of action should you take?

A. **Use the Organization Policy Service to create a compute.trustedimageProjects constraint on the organization level. List the trusted project as the whitelist in an allow operation**

Q. When constructing a secure container image, what are the two elements that you should include in the build whenever feasible? (Choose two.)

A. **Remove any unnecessary tools not needed by the app.**
**Package a single app as a container.**

Q. Your organization is hosting a critical healthcare application on Google Cloud. The Security Operations Center (SOC) needs to implement a solution for real-time monitoring and alerting of security incidents. Which GCP service should they leverage, considering the specific requirements and sensitivity of healthcare data?

A. **Cloud Security Command Center**

Q. To adhere to the directive set by the Chief Information Security Officer (CISO) in your company, which mandates the storage of business data in designated locations to meet regulatory requirements for the organization's global expansion, you have conducted a thorough analysis for implementation. The key findings are as follows:

- The relevant services fall within the purview of the Google Cloud Data Residency Terms.
- Business data is confined to specific locations within the same organizational framework.
- The folder structure is versatile enough to accommodate multiple data residency locations.

With the intention of enforcing the Resource Location Restriction organization policy constraint, the question arises: at what level in the resource hierarchy should this constraint be established?

A. Project

Q. You are tasked with migrating a legacy application from your company's datacenters to GCP before the current maintenance contract expires. Unfortunately, there is no documentation available to identify the ports used by the application, and you want to ensure a smooth migration without jeopardizing your environment. What steps should you take?

A. **Migrate the application into an isolated project using a "Lift & Shift" approach. Enable all internal TCP traffic using VPC Firewall rules. Use VPC Flow logs to determine what traffic should be allowed for the application to work properly.**

Q. A company is implementing their application on Google Cloud Platform and adheres to a policy mandating the use of a storage solution capable of automatically replicating long-term data across at least two geographic locations. Which storage solution is compliant with this requirement?

A. **Cloud BigQuery**

Q. To achieve a consolidated log view of all development cloud projects in your SIEM, your team needs to address projects within the NONPROD organization folder, alongside test and pre-production projects. These development projects share the ABC-BILLING billing account with the wider organization. What logging export strategy should be employed to fulfill these requirements?

A. **1. Export logs in each dev project to a Cloud Pub/Sub topic in a dedicated SIEM project.**

**2. Subscribe SIEM to the topic.**

Q. TrendyTech recently experienced a security incident where an unauthorized user accessed internal resources. To prevent similar incidents, you need to implement a more robust access control strategy for Cloud SQL. What is the best approach considering TrendyTech's existing application architecture and user groups?

A. Leverage Cloud Identity & Access Management (IAM) to define separate roles with granular permissions for different user groups like developers, QA testers, and database administrators.

Q.A mobile workforce uses a variety of devices to access cloud applications. The security team wants to grant access based on whether the device is corporate-managed and meets certain security standards. Which Access Context Manager feature should they use?

A. Custom access levels using Common Expression Language.

Q.You want to limit network access to your GKE pods for enhanced security. Which strategies can you use?

A.Utilize pod security policies to restrict privileged containers and host volume mounts.
Implement service accounts with limited permissions for pods to access external resources.
Configure network policies to define inbound and outbound traffic rules for pods.

Q."TrendyTech," the rapidly growing e-commerce platform, needs to manage access to sensitive customer data stored in Cloud Storage buckets. Their development team requires read access for analytics, while customer support needs limited read access for order-related tasks. Choose the best solutions for each scenario:

To ensure auditability and maintain a record of user activity within Cloud Storage buckets, TrendyTech should:

A. Enable Cloud Logging for centralized logging of all bucket access attempts and data modifications.

Q. **Company "FinTech Solutions" exposes financial APIs through Cloud API Gateway and needs to balance security with performance. Choose the best approach for each situation:**

"FinTech Solutions" relies heavily on API keys for user authentication. How can they mitigate the risks associated with API keys?
A. Encrypt API keys in transit using HTTPS but store them unencrypted at rest within the application.
Rotate API keys regularly and implement short-lived access tokens to minimize exposure time.

Q. You need to ensure that incident response activities are logged and audited for compliance purposes. What GCP service provides detailed audit logs for incident response activities?

A. Cloud Security Command Center (Cloud SCC)

Q.A cloud security manager wants to audit who has **permission to delete** virtual machines in a specific Google Cloud project. They need to identify all principals with this capability. Which feature of Policy Analyzer should they utilize to find this information?

A. Run a query specifying the permission for VM deletion and the project scope.

Q.Your company stores sensitive financial data in Cloud Storage buckets. To comply with industry regulations and protect data at rest, what should you implement?

A.Server-side encryption with Cloud Key Management Service (KMS) for centralized key management.

Q. Your company develops and deploys microservices using Google Kubernetes Engine (GKE). To protect container images from unauthorized access and tampering, what security measures should you prioritize?

A. Store container images in Cloud Storage buckets with no public access for easy deployment.
Encrypt container images with Cloud Key Management Service (KMS) before storing them in the Container Registry.
Implement Binary Authorization to enforce image signature verification before deployment.

Q. You need to ensure that an Azure VM using a managed identity can obtain Google Cloud credentials. Which attribute should you primarily use as the subject identifier in Google Cloud for Azure VMs?

A. The managed identity ID.

Q. Your project requires automated tools to use credentials from an AWS EC2 instance to access Google Cloud services. How can these tools automatically obtain the external credentials?

A. Through a credential configuration file that points to the **workload identity pool** and provider.

Q. Your organization is deploying applications on GKE across multiple regions, and you want to ensure low-latency communication between clusters. What GCP service can you use to connect GKE clusters in different regions securely?

A. Anthos Service Mesh

Q. Your company is looking for a cost-effective MFA solution that can integrate with Google Cloud. What is a recommended cost-effective MFA method for GCP?

A. SMS-based codes

Q. An organization needs to understand which users and groups have access to modify a particular BigQuery dataset containing sensitive data. They want to ensure the audit captures all potential access, including indirect permissions through groups. What option should they enable in their Policy Analyzer query?

A. Group expansion to list all individual group members.

Q. Your company has resources spread across multiple cloud projects and wants to ensure that data does not leak outside of these environments. What feature of Access Context Manager would best meet this requirement?

A. Service perimeters defining sandboxes of resources.

Q. Your company plans to use AWS EC2 instance profiles to authenticate to Google Cloud services without managing service account keys. What is the first step to enable this integration?

A. Configure a workload identity pool in Google Cloud.

Q.Your critical API endpoint experiences a sudden surge in traffic. How can you differentiate between a legitimate traffic spike and a DDoS attack?

A. Leverage Cloud Armor's rate limiting and IP blacklisting features to mitigate the traffic surge.
Implement Cloud Monitoring anomaly detection to automatically alert on unusual API activity.
Analyze traffic patterns and identify anomalies in request volume and origin.

Q. Your company's security team suspects a potential malware infection within a Compute Engine VM. To investigate and remediate the threat, what steps should you take?

A. Use Cloud Logging to analyze VM logs for suspicious activity and identify the malware origin.
Immediately shut down the VM to prevent further spread of malware.
Deploy a Cloud Armor security policy to block network traffic from the infected VM.

Q. After setting up a workload identity pool, what is the next step to allow an external workload from AWS to authenticate to Google Cloud using the pool?

A. Create a service account in Google Cloud to represent the workload.

Q. To detect and prevent unauthorized access attempts to GCP resources, what security feature should you enable?

A. Context-aware access (CAA) to evaluate user and device context before granting access.
Security Health Analytics (SHA) for detailed logs of user activities and access events.
Cloud Security Command Center (SCC) for security-related insights and threat detection.

Q. Your company has a large number of employees and contractors with varying levels of access to GCP resources. To simplify access management and reduce security risks, what should you implement?

A. Leverage Google Groups to group users with similar access needs and assign IAM roles to groups instead of individual users.
Integrate with Active Directory using Cloud Identity for seamless user authentication and authorization.

Q. TrendyTech's application relies heavily on real-time analytics for customer behavior insights. The application continuously reads and writes data to Cloud Storage buckets containing sensitive customer purchase records. How can you secure this **data transfer** while maintaining performance and scalability?

A. Encrypt data at rest in Cloud Storage buckets using Cloud Key Management Service (KMS) and implement server-side encryption for data in transit using HTTPS and IAM permissions.
DLP는 데이터 내용만 보호해준다는 한계가 존재. 데이터 전송 및 보안과 관련된 내용은 KMS & HTTPS & IAM

Q. You are setting up an App Engine project and want to ensure that users can sign in using various providers through Identity Platform. What should be your first step after creating a new Google Cloud project?

A. Enable Identity Platform in the Google Cloud Marketplace.



# Pratice Exam 1 

Q. As a security engineer at a financial institution, your organization intends to store data on Google Cloud. However, the leadership team is apprehensive about the security of highly sensitive data, particularly regarding the potential access by **internal Google employees** to your company's data on Google Cloud. What solution would you recommend?

A. Enable Access Transparency logs with Access Approval requests for Google employees.
**Access transparency log** 는 google의 운영자가 고객의 콘텐츠에 접근할 때마다 그 활동을 기록하는 로그입니다.

Q. As the security administrator for your company, you oversee the creation of multiple GCP projects by the development team under the "implementation" folder for various development, staging, and production workloads. To prevent data exfiltration by malicious insiders or compromised code, you aim to establish a security perimeter. However, you want to ensure that communication between the projects is not restricted.

What steps should you take?
A. Use an infrastructure-as-code software tool to set up a **single service perimeter** and to deploy a Cloud Function that monitors the "implementation" folder via Google Cloud Monitoring (formerly Stackdriver) and Cloud Pub/Sub. When the function notices that a new project is added to the folder, it executes Terraform to add the new project to the associated perimeter.
**monitoring을 위한 하나의 service perimeter 설정**

Q. You are tasked with suggesting a solution for storing and retrieving sensitive configuration data from an application **hosted on Compute Engine**. What option would you recommend?
A. Secret Manager 
**compute engine에서 hosting 되고있으면 secret manager를 사용** 

Q. Which two security features are pertinent to the implementation of VPC peering for connecting two VPC networks? (Choose two.)

A. Ability to peer networks that belong to different Google Cloud organizations
Non-transitive peered networks; where only directly peered networks can communicate

Q. The security and risk management teams of an organization are inquiring about their responsibility and Google's responsibility concerning specific production workloads on Google Cloud, mainly leveraging platform-as-a-Service (PaaS) options like App Engine. What should be their primary focus within the technology stack regarding responsibilities when utilizing App Engine?
A. Defending against XSS and SQLi attacks

Q. You are addressing access denied errors between Compute Engine instances linked to a Shared VPC and BigQuery datasets situated in a project safeguarded by a **VPC Service Controls perimeter**. What measures should you undertake to resolve this problem?
A. Add the host project containing the Shared VPC to the service perimeter.

Q. As a member of a security team, your objective is to guarantee that a Cloud Storage bucket in Project A is exclusively readable from Project B. Additionally, you aim to prevent access to the data in the Cloud Storage bucket from being accomplished or replicated to Cloud Storage buckets outside the network, irrespective of the user possessing the correct credentials.

What steps should you take to achieve these security requirements?
A. Enable VPC Service Controls, create a perimeter with Project A and B, and include Cloud Storage service.
**PC 서비스 제어(VPC Service Controls)는 민감한 데이터의 유출을 방지하고 보안을 강화**

Q. Your organization has set up synchronization and SAML federation between Cloud Identity and Microsoft Active Directory. To minimize the risk of Google Cloud user accounts being compromised, what steps should you take?
A. Create an Active Directory domain password policy with strong password settings, and configure post-SSO (single sign-on) 2-Step Verification with **security keys** in the Google Admin console.

Q. As your company expands, you've chosen to integrate Google Cloud Directory Sync (GCDS) with your on-premises LDAP server for user management in Cloud Identity. Your objectives include replicating user and group lifecycle changes from LDAP and disabling manually created users in Cloud Identity. With LDAP search attributes configured, what is the appropriate next step to complete this solution?
A. 1. Configure the option to suspend domain users not found in LDAP.
2.Set up a recurring GCDS task.

Q. In the initial phase of transitioning infrastructure from on-premises to Google Cloud Platform (GCP), an organization prioritizes migrating ongoing data backup and disaster recovery solutions to GCP. The subsequent phase involves migrating the on-premises production environment to GCP, accompanied by the implementation of **stable networking connectivity** between the two environments. In this scenario, which GCP solution would be most suitable?
A. Employ Cloud Storage with a scheduled task and gsutil, leveraging **Cloud Interconnect**.

Q. How can you ensure that data on Compute Engine disks is encrypted at rest with keys managed by Cloud Key Management Service (KMS), and the Cloud Identity and Access Management (IAM) permissions for these keys are managed collectively in a **group-oriented manner**, maintaining **uniform permissions** across all keys?
A. Create a single KeyRing for all persistent disks and all Keys in this KeyRing. Manage the IAM permissions at the **KeyRing** level.

Q. You are formulating a new governance model for your organization's secrets housed in Secret Manager. Presently, secrets for both Production and Non-Production applications are stored and retrieved utilizing service accounts. Your proposed solution must:

- Enable precise access control for secrets
- Grant you authority over the rotation schedules for the encryption keys securing your secrets
- Uphold segregation between different environments
- Facilitate straightforward management

What approach should you adopt to meet these requirements?
A.1. Use separate Google Cloud projects to store Production and Non-Production secrets.
2. Enforce access control to secrets using project-level identity and Access Management (IAM) bindings.
3. Use customer-managed encryption keys to encrypt secrets.

Q. Your Security team suspects that a former employee gained unauthorized access to Google Cloud resources within the past two months using a service account key. To confirm this unauthorized access and assess user activity, what steps should you take?
A. Use the Logs Explorer to search for user activity.

Q. In the development of a 3-tier web application on Google Cloud Platform (GCP), a customer and another company are collaborating to create different segments of the application in **separate GCP Organizations**. The customer is responsible for the application tier in their GCP Organization, while the other company is handling the storage tier. To ensure that communication between application segments avoids the public internet, what type of connectivity should be implemented?
A. VPC peering

Q. The security operations team requires access to **security-related logs** for all projects within their organization. They have specific requirements:

- Adhere to the least privilege model, providing only view access to logs.
- Access Admin Activity logs.
- Access Data Access logs.
- Access Access Transparency logs.    
Which Identity and Access Management (IAM) role should be assigned to the security operations team?

A. roles/logging.privateLogViewer
- 모든 로그 항목에 대한 읽기 권한(공개 및 비공개 로그 포함).
- Admin Activity 로그, Data Access 로그 및 기타 비공개 로그에 대한 접근 권한을 포함합니다.

Q. You are required to establish an encryption-at-rest strategy that **simplifies key management for non-sensitive data**, **safeguards sensitive data**, and allows flexibility in controlling key residency and rotation schedules. The compliance mandate necessitates adhering to FIPS 140-2 Level 1 for all data types. What steps should you take to meet these requirements?
A. Encrypt non-sensitive data with Google default encryption, and encrypt sensitive data with Cloud Key Management Service.

Q. How can the organization fulfill compliance requirements to guarantee that PCI Kubernetes Pods designated as in-scope are situated exclusively on Nodes labeled as "in-scope"? Additionally, these Nodes should only host Pods that fall within the defined in-scope category.
A. Place a **taint** on the Nodes with the label in-scope: true and effect NoSchedule and a toleration to match in the Pod configuration.

Q. As part of a security team investigating a compromised service account key, you need to audit which new resources were created by the service account. What should you do?
A. Query Admin Activity logs -> resource created/deleted log

Q. Your company manages an application instance group currently deployed behind a Google Cloud load balancer in us-central-1, utilizing the **Standard Tier network**. The infrastructure team intends to expand to a second Google Cloud region, us-east-2. To facilitate the distribution of new requests to the instance groups in both regions using a single external IP address, what steps should you take?
A. Change the load balancer frontend configuration to use the Premium Tier network, and add the new instance group.
-> standard tier lb 는 하나의 region 밖에 host 못함. 그래서 premium tier lb로 바꿔야됨 

Q. What steps should be taken to confirm that the data written to BigQuery, from the newly deployed App Engine application last week (with no other workloads in the project), was exclusively carried out using the App Engine Default Service Account?
A. 1. Use Cloud Logging and filter on BigQuery Insert Jobs.
2. Click on the email address in line with the App Engine Default Service Account in the authentication field.
3. **Click Hide Matching Entries.** -> default service account 가 사용한것은 정상적인것
4. Make sure the resulting list is empty.

Q. Your organization has recently implemented a new application on Google Kubernetes Engine, and now there's a need for a protective solution with the following specifications:

- Scans must occur at least once weekly.
- Capability to identify cross-site scripting vulnerabilities is essential.
- Authentication using Google accounts is a requirement.
Which solution is most suitable for these requirements?
A. Web Security Scanner
GKE에서 실행되는 웹 애플리케이션의 보안 취약점을 식별하고 해결하는 데 도움이 되는 관리형 서비스입니다. 

Q. In the event of terminating an engineer, what actions should a customer take to ensure the automatic deprovisioning of the engineer's Google account?
A. Configure Cloud Directory Sync with their directory service to provision and deprovision users from Cloud Identity.

Q. As the Security Admin in your company, you aim to synchronize all security groups with an email address from your LDAP directory in Cloud IAM. What steps should you take?
A. Configure Google Cloud Directory Sync to sync security groups using LDAP search rules that have "user email address" as the attribute to facilitate one-way sync.

Q. You've been assigned the responsibility of fortifying an external web application against common attacks for a public application on Google Cloud. Before enforcing these policy changes, what service should you employ to validate them?
A. Google Cloud Armor's preconfigured rules in **preview mode**

Q. In a scenario where a customer aims to enhance accessibility for their mobile workforce to reach a CRM web interface hosted on **Google Cloud Platform** (GCP), currently limited to access within the corporate network, the customer seeks to extend access over the internet. The team emphasizes the necessity of implementing an authentication layer supporting two-factor authentication for enhanced security.

Which GCP product should the customer implement to fulfill these requirements?
A. Cloud Identity-Aware Proxy

Q. Your company aims to identify suitable products for customers to enhance their credit scores based on age groups. To achieve this, you must integrate user information from the company's banking app with credit score data obtained from a third party. Although utilizing raw data would fulfill the task, it poses a risk by exposing sensitive information that could extend into new systems. To address this risk, you need to implement de-identification and tokenization using Cloud Data Loss Prevention while preserving referential integrity throughout the database. What cryptographic token format should you employ to fulfill these requirements?
A. Deterministic encryption

Q. You are tasked with safeguarding highly sensitive data stored in BigQuery. While your operations teams require access to this data, compliance with privacy regulations mandates that they cannot read specific sensitive fields, such as email addresses and first names. These particular sensitive fields should only be accessible to the Human Resources team on a need-to-know basis.

How can you address this situation and implement the necessary privacy controls?
A. Perform tokenization for Pseudonymization with the Cloud Data Loss Prevention API, and store that data in BigQuery for later use.
tokenization은 원복이 가능, redaction은 복원불가 

Q. As a member of your company's development team, you've identified a potential security concern in the web application hosted on GKE staging. The application dynamically incorporates user data into web pages without adequately validating the input, posing a risk for attackers to execute malicious commands and display arbitrary content in a victim user's browser in a production environment.

How should you address and rectify this vulnerability?

A. Use Web Security Scanner in staging to simulate an XSS injection attack, and then use a templating system that supports contextual auto-escaping.

Q. How can the architecture of your company's messaging app be aligned with FIPS 140-2 compliance on GCP compute and network services? The app utilizes a Managed Instance Group (MIG) to oversee a cluster of Compute Engine instances, which employ Local SSDs for data caching and use UDP for instance-to-instance communications. The app development team is open to making any required changes to ensure compliance. What recommendations should be suggested to fulfill these requirements?
A. Encrypt all cache storage and VM-to-VM communication using the BoringCrypto module.
BoringCrypto는 Google이 관리하는 FIPS 140-2 인증을 받은 암호화 모듈로, BoringSSL의 일부분입니다 


