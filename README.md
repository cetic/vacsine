# vacsine 

Adaptive continuous security orchestration in polymorphous environments
----------

Vacsine is an open-source security orchestration, automation and response tool that provides adaptive security for distributed systems. It relies on continuous monitoring of Cloud and Edge systems to define, evaluate and apply automated countermeasures such as firewalls, intrusion detection systems, honeypots or quarantining. The automated response is triggered by changes to security requirements, indicators of compromise, incidents and vulnerabilities. The efficiency and speed of countermeasures deployment is evaluated in automatically provisioned sandbox environments that shadow the target Cloud/Edge systems. Those sandboxes provide observability and scalability for the training and maintenance of security response strategies.

Use cases
-------

1. Enforce security policies on cloud/edge infrastructures based on certification criteria
2. Continuous security self-assessment

Requirements
-------

### 1. Orchestration of the adaptive security response

* Input: security policy, target system description
* Output: verified remediation execution

1. create a test sandbox containing a clone of the target system
2. analyse the security policy and deduce a remediation workflow
3. apply remediation to the test sandbox
4. check security requirements against test sandbox
5. apply remediation to the target system
6. check security requirements against target system

### 2. Observability of the security policy orchestration

* Input: remediation workflow, target system description
* Output: remediation logs

1) apply remediation workflow to the system
2) check remediation workflow execution status: execution logs for each remediation step should contain details on the execution for tracability (start time, duration, informative, error messages, ...)

Architecture
-------

Vacsine is composed of several modules that are deployed in Cloud and Edges infrastructures:

### Federated Security Controller

* management of the security remediation on the target system
* consolidated view of the remediations history and states across the various edges and clouds
* registry of the **security policies** of the system

### Remediation registry

* contains templates and workflows of security remediations

### Security monitoring

* remediation execution logs, 
* results of vulnerability scans, 
* threat indicators, etc.

### Security Agent

* deployed on each edge and cloud
* provides security remediations based on the detection of various events and the matching of those events to **remediation workflows**, those are triggered by:
  * changes to security requirements,
  * threat indicators,
  * incidents,
  * vulnerabilities
* _can_ operate in autonomous mode to provide quicker response time to events happening in the edge they are deployed on, and continued operation in case the edge-cloud connexion is degraded. The **edge datastore** contains a local version of the security policies, remediations catalog and security monitoring information.

### Security Services

* Vulnerability remediation in the form of **security services**:
  * firewalls, 
  * penetration tests, 
  * intrusion detection systems, 
  * honeypots, etc. 

### Remediation sandboxes

* test remediation workflows in a dedicated environment before applying them
* training of new remediation strategies
