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
- Container images contain the latest security patch → **google-manged based images**
- deployment polices → deployment policies define in **Binary Authorization** ensure that only trusted images can be deployed in GKE.
- Vulnerability scanning can be performed by **container analysis** to discover package vulnerability information in container base image.
- Personally identifiable information (PII)
- **Cloud Data Loss Prevention(DLP)** can be used to inspect data(discover important data), protect data(masking)
- Customer-managed encryption keys(CMEK), Customer-supplied Encryption keys(CSEK)
- PCI DSS(Payment Card Industry Data Security Standard)
- Active Directory: microsoft auth program
- **Cloud interconnect** : 지연 시간이 짧고 가용성이 높은 연결을 제공, 내부 IP 주소 통신

|기능|Dedicated Interconnect|Partner Interconnect|
|---|---|---|
|속도|~200Gbps|50Mbps~50Gbps|

---

Udemy

- GCP has 2 different network service.
    - Standard Tier network : use public network, cost efficiency, normal latency
    - Premium Tier network : use backbone network, high cost, low latency → backend랑 동일한 region에서만 가능
- It is recommended to isolate VMs using service accounts whenever possible → **vm마다 service account를 mapping 할 수 있음**
- **Web security scanner** can help you find security problems. automatically scan and detect common security vulnerabilities.
- **firewall 설정할때 특정 service account 를 allow/deny 할 수 있음.**
- Cloud Armor에는 정책을 update 하기 전에 impact을 미리 볼 수 있는 preview-mode 를 지원함.

|기능|VPC Flow Logs|Packet Mirroring|Cloud Audit Logs|
|---|---|---|---|
|캡처 데이터|VPC 내부 네트워크 트래픽 메타데이터|네트워크 패킷 데이터|API 호출 및 리소스 변경|
|사용 사례|성능 모니터링(기본적인 분석), 보안 분석, 비용 최적화|심층 보안 분석, 성능 모니터링|컴플라이언스, 보안 분석, 변경 관리|
|특징|실시간 로그 수집, 로그 분석 도구 통합|실시간 패킷 캡처, 외부 분석 도구 통합|모든 API 호출 추적, 로그 분석 도구 통합|

- **Access transparency log** 는 google의 운영자가 고객의 콘텐츠에 접근할 때마다 그 활동을 기록하는 로그입니다.
- **Deterministic encryption**은 동일한 입력 값에 대해 항상 동일한 암호 텍스트를 생성하는 암호화 방법입니다.
- Control rotation schedules for encryption keys → customer-managed encryption key, google managed encryption key는 rotation을 내가 설정할 수 없음.

|특징/장점/단점|Google-managed encryption keys|Customer-managed encryption keys (CMEK)|
|---|---|---|
|키 회전 및 폐기|자동|사용자 설정|

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
- **Secret Manage**r is a secure and convenient storage system designed for API keys, passwords, certificates, and other sensitive data. It serves as a centralized platform and single source of truth for efficiently managing, accessing, and auditing secrets throughout Google Cloud.
- DNSSEC(Domain Name System Security Extensions)는 **IP(Internet Protocol) 네트워크를 통해 전송되는 데이터의 보안을 위해 DNS 레코드에 추가되는 암호화 서명**
- service account가 실수로 지워지면 undeleted command로 살릴 수 있음
- PCI (personal credit information) PCI DSS(Payment Card Industry Data Security Standard)
- PII (Personal Identifiable _Information)_
- _**SIEM**_(Security Information and Event Management)

|기능/특징|Cloud VPN|Shared VPC|VPC Peering|
|---|---|---|---|
|설명|온프레미스 네트워크 또는 다른 클라우드 제공자의 네트워크를 GCP의 VPC 네트워크에 안전하게 연결할 수 있는 서비스|GCP 프로젝트 간에 VPC 네트워크를 공유할 수 있는 기능|두개의 GCP VPC 네트워크를 상호 연결하여 서로의 리소스에 접근|
|주요 용도|온프레미스 네트워크 연결|여러 프로젝트 간 네트워크 공유|VPC 네트워크 간 상호 연결|

|기능/특징|network security|cloud armor|
|---|---|---|
|목적|네트워크 레벨 보안 및 관리|웹 애플리케이션 방어 및 DDoS 방어|
|구성 요소 및 서비스|VPC 방화벽, Cloud VPN, IAM, IAP 등|WAF 규칙, DDoS 방어, 맞춤형 보안 정책|

comprise ~으로 구성되다

consolidate 통합하다

versatile 다재다능한

directive 지시, 명령

leverage 영향력

eligible 자격이있는

mandate 위임장

anonymize 익명으로 하다.

obstruct 막다

retain 유지하다. Preclude 배제하다.

assessment 평가

elastic 탄력이 있는

inherent 고유의

delegate 대리자, 특파하다, 위임하다.

delegation 대표단, 위임

redundant 불필요한, 중복된

Pseudonymization 가명화

pertinent 적절한

imperative 반드시 해야하는

possess 소유하다

reconcile 조정하다

migrates 이동하다

corresponding 상응하는

tailored 맞춤형

permissive 허용적인

suspend 중단하다

recurring 반복되는

encompasses 포함하다

federation 연합

retrieval 회복, 검색

constraint 제약, 통제

immutable 변경할수없는

intention 의사, 의도

revoke 취소, 취소하다

autonomously 자율적으로, 자체적으로

criteria 기준

audit 심사, 감시

constant 끊임없는

publicly 공개적으로

Granular 세분화된

straightforward 똑바로, 간단한, 솔직한

Uphold 받치다, 유지하다

segregation 분리

precise 정밀한

Unless ~하지 않는한

proctor 감독관

onsite 현장의

formulate 공식화하다

compromise 타협, 더럽히다

perimeters 둘레

exfiltration 유출 exfiltrate 유출하다

mitigate 완화시키다

irrespective 관계없이

respective 각각의

upholding 지지하다

referential 참고의

apprehensive 걱정되는, 불안한

extensive 대규모의

pertinent 적절

compliance 규정 준수

mandate 위임장

basis 근거, 이유, 기준

redaction : 편집

segments : 구획, 분활하다.

oversee 감독하다

corporate 기업의, 회사의

adhere 준수하다. 집착하다. 들러붙다

inquiring 미심쩍은, 탐구적인

redact 수정하다

leading 주요한

disruption 분열

swiftly 신속하게

compromising 타협하여 해결짓다.

facilitate 가능하게 하다

Subsequently 그 뒤에, 나중에

objective 목적, 목표

feasible 실현가능한

explicit 분명한

privileges 특권

incorporates 통합하다

adequately 적절하게

malicious 악의적인

arbitrary 임의적인

victim 피해자

contextual 상황에 맞는

vulnerabilities 취약점

seamlessly 원활하게

fortify 확고히 하다

comprehensive 포괄적인

[examtopics](https://www.notion.so/examtopics-d91833db80764dce9a8956d7bfd38914?pvs=21)

---

Q. To establish a Cloud Interconnect connection between your company's on-premises data center and VPC host network, with the aim of restricting on-premises applications to access Google APIs exclusively via Cloud Interconnect and not through the public internet, while ensuring usage of only VPC Service Controls-supported APIs to mitigate exfiltration risk to non-supported APIs, what network configuration should you implement?

A. **Use restricted [googleapis.com](http://googleapis.com) to access Google APIs using a set of IP addresses only routable from within Google Cloud, which are advertised as routes over the Cloud Interconnect connection.**

Q. How should your team structure the network to ensure that only the frontend application can access the backend database, with no access granted to other instances on the network?

A. **Create an ingress firewall rule to allow access only from the application to the database using firewall tags.**

Q. You are tasked with establishing a connection between your organization's on-premises network and an existing Google Cloud environment, featuring a Shared VPC with Production and Non-Production subnets. Your requirements are as follows:

- Utilize a private transport link.
- Set up access to Google Cloud APIs through private API endpoints originating from on-premises environments.
- Ensure that Google Cloud APIs are exclusively accessed via VPC Service Controls. How would you proceed?

A.

**1. Set up a Dedicated Interconnect link between the on-premises environment and Google Cloud.**

**2. Configure private access using the [restricted.googleapis.com](http://restricted.googleapis.com) domains in on-premises DNS configurations.**

Q. Your team is tasked with organizing the Google Cloud Platform (GCP) environment to consolidate control over networking components such as firewall rules, subnets, and routes. Additionally, there is an on-premises infrastructure requiring connectivity to GCP resources through a private VPN connection. The network security team is responsible for overseeing these networking resources. What type of networking design should your team employ to fulfill these requirements?

A. **Shared VPC Network with a host project and service projects**

centralize the control → Shared VPC

Q. To balance the load across multiple instances running the application and ensure a secure TLS connection terminated by the Load Balancer for an application implemented on Compute Engine, accessed by clients on port 587, which type of Load Balancing should be utilized?

A. **SSL Proxy Load Balancing**

Q. As the manager of your organization's Security Operations Center (SOC), you oversee the monitoring and detection of network traffic anomalies in Google Cloud VPCs, primarily based on **packet header information.** However, you aim to enhance your investigative capabilities by exploring network flows and their payloads. Which Google Cloud product would best serve this purpose?

A. **Packet Mirroring**

Q.

You've recently acquired a new workload, and the Web and Application (App) servers are set to operate on Compute Engine within a freshly established custom VPC. Your task is to implement a secure network communication solution that adheres to the following specifications:

- Restrict communication exclusively between the Web and App tiers.
- Ensure uniform network security when autoscaling the Web and App tiers.
- Preclude Compute Engine Instance Admins from modifying network traffic.

What steps should you take to achieve this?

A.

**1. Re-deploy the Web and App servers with instance templates configured with respective service accounts.**

**2. Create an allow VPC firewall rule that specifies the target/source with respective service accounts.**

Q. Which load balancer type should you employ to retain client IP by default while utilizing the standard network tier?

A. **TCP/UDP Network**

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

Q. To comply with PCI DSS requirements, a client seeks to enforce authorization for all outgoing traffic. Which two cloud services fulfill this demand without requiring supplementary compensating measures? (Select two.)

A. Compute Engine

Cloud Function

Q. In handling protected health information (PHI) for an electronic health record system, the privacy officer is apprehensive about sensitive data storage in the analytics system. Your responsibility is to anonymize the sensitive data in a manner that is non-reversible and ensures that the anonymized data does not retain the character set and length. What Google Cloud solution should you employ?

A. **Cloud Data Loss Prevention with cryptographic hashing**

Q. Your organization is implementing a Zero Trust security model and wants to ensure that only authorized users with the right devices can access resources in Google Cloud. Which GCP feature should be used to enforce device-based access controls for users?

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

Q.Your organization is adopting a microservices architecture on GCP, and you want to ensure secure communication between microservices running in different clusters. Which GCP service can you leverage to establish a private and secure connection between these microservices?

A. **Anthos Service Mesh**

Q. How can you ensure that an external user cannot access the application, even in the event of a compromised employee password, when your company is using GSuite and has developed an internal-use application on Google App Engine?

A.**Enforce 2-factor authentication in GSuite for all users.**

Q. What steps should be taken to investigate and confirm the functionality of firewall rules on a Compute Engine-hosted public-facing application when users report an outage, and recent changes to firewall rules are suspected to be the cause?

A. **Enable Firewall Rules Logging on the latest rules that were changed. Use Logs Explorer to analyze whether the rules are working correctly.**

Q. A large e-retailer is moving to Google Cloud Platform with its ecommerce website. The company wants to ensure payment information is encrypted between the customer's browser and GCP when the customers checkout online. What should they do?

A. **Configure an SSL Certificate on an L7 Load Balancer and require encryption.**

Q. In a scenario where an organization is experiencing a rise in phishing emails, what approach should be employed to safeguard employee credentials?

A. **Multifactor Authentication**

Q. As a member of the security team in an organization, tasked with securing a GCP project that includes credit card payment processing systems, web applications, and data processing systems, your goal is to minimize the scope of systems subject to PCI audit standards. What steps should you take to achieve this objective?

A. **Move the cardholder data environment into a separate GCP project.**

Q. When engaging with support center agents through online chat, customers frequently provide images of their documents containing personally identifiable information (PII). The organization operating the support center is apprehensive about PII being stored in their databases within regular chat logs, which are retained for analysis by internal or external analysts to identify customer service trends. To address this concern and uphold data utility, which Google Cloud solution should the organization employ?

A. **Use the image inspection and redaction actions of the DLP API to redact PII from the images before storing them for analysis.**

Q. Your multi-cloud environment involves integrating on-premises systems with GCP resources. To ensure private transport links and control access to GCP APIs through private API endpoints originating from on-premises environments, which hybrid networking solution should you implement?

A. dedicated interconnect

Q.A customer's organization comprises multiple business units, each functioning autonomously with its own engineering group. Our team aims to gain visibility into all company projects and seeks to structure Google Cloud Platform (GCP) projects according to distinct business units. Additionally, each business unit requires its own specific sets of IAM permissions.

A. **Create an organization node, and assign folders for each business unit.**

Q.

You are assigned the responsibility of exporting and auditing security logs for login activity events in the Google Cloud console and API calls that modify configurations to Google Cloud resources. The export must adhere to the following specifications:

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

Q.

To adhere to the directive set by the Chief Information Security Officer (CISO) in your company, which mandates the storage of business data in designated locations to meet regulatory requirements for the organization's global expansion, you have conducted a thorough analysis for implementation. The key findings are as follows:

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

A.

**1. Export logs in each dev project to a Cloud Pub/Sub topic in a dedicated SIEM project.**

**2. Subscribe SIEM to the topic.**