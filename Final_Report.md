# Cybersecurity Incident Response Ontology: A Knowledge Graph Approach for Healthcare Security Operations

**Abdennabi Ahrrabi**

School of Computing, Ulster University
London, United Kingdom
ahrrabi-a@ulster.ac.uk

---

## ABSTRACT

This paper describes a cybersecurity ontology I built for incident response using OWL and Protégé. I modelled a realistic ransomware attack against a healthcare organisation to demonstrate how semantic technologies can support Security Operations Centre work. The implementation has 49 classes organised into 9 hierarchies, 23 object properties with a property chain for automatic attack path inference, 10 datatype properties, and 7 defined classes for automated reasoning. I validated the ontology using HermiT, which confirmed logical consistency across all 54 individuals representing the attack scenario. Key features include automatic classification of vulnerable assets, HIPAA compliance checking, and inference of threat-to-asset targeting relationships. The paper also critically evaluates how ontologies relate to Large Language Models, exploring their synergies, limitations, and integration strategies.

**Keywords:** Ontology, OWL, Cybersecurity, Incident Response, Knowledge Graph, Healthcare Security, HIPAA, Ransomware, Large Language Models

---

## I. INTRODUCTION

During a security incident, understanding how different elements connect to each other is really important. A threat exploits vulnerabilities, those vulnerabilities affect certain assets, security controls protect assets and deal with threats, and incidents need responses. These concepts link together in ways that normal database systems cannot easily handle.

Healthcare organisations have particular difficulties with cybersecurity incidents. When ransomware hits a hospital, the security team needs to quickly work out which systems are compromised, what vulnerabilities were used, what patient data could be exposed, whether they are still HIPAA compliant, and what order to fix things in. HIPAA (the Health Insurance Portability and Accountability Act) sets strict rules for healthcare organisations about protecting patient health information, so quick and accurate incident response is essential.

The issue is that this information usually sits in separate systems—vulnerability scanners, asset inventories, SIEM logs, and compliance checklists. There is no easy way to see the connections between a threat, the vulnerabilities it exploits, and the assets it affects. This separation slows down response times and can cause things to be missed during incident response.

This project creates an ontology—a formal model of these concepts and their relationships—using OWL (Web Ontology Language). The main benefit of using an ontology is that once you define the relationships properly, a reasoner can automatically work out new facts through logical inference. For example, if I define that a threat exploits a vulnerability and that vulnerability affects an asset, the reasoner can figure out that the threat targets that asset without me having to state it explicitly.

### A. Problem Identification and Justification

I chose cybersecurity incident response for this ontology for a few reasons. First, the domain has lots of interconnections between concepts that work well with semantic representation. Threats, vulnerabilities, assets, controls, and incidents form a complicated web of relationships that relational databases struggle to capture properly. Second, healthcare is a high-stakes environment where getting incident response right can actually save lives—if hospital systems go down, critical treatments get delayed and patients could be harmed. Third, regulations like HIPAA require specific compliance measures that can be formally modelled and checked automatically through reasoning.

Before deciding on ontologies, I looked at other approaches. Spreadsheets and databases store data well but cannot reason about relationships on their own. Rule-based systems can automate things but need explicit rules written for every possible situation. Machine learning needs lots of training data and produces "black box" decisions that are hard to explain—not great when you need to demonstrate compliance. Ontologies solve these issues because they enable automatic inference, provide knowledge representation that is explicit and explainable, support consistency checking, and use standard formats like OWL and RDF that work with different tools.

The growing number of ransomware attacks on healthcare motivated this project. Industry reports show that healthcare gets hit by more ransomware than any other sector, and the average breach costs over $10 million. An ontology-based approach can help security teams respond better by giving them a unified view of attack paths, affected assets, and appropriate responses.

### B. Objectives

I set the following goals for this project:

1. Model the main concepts in cybersecurity incident response—assets, threats, vulnerabilities, controls, incidents, and responses
2. Create meaningful relationships between these concepts, including a property chain that automatically infers attack paths
3. Use defined classes so the reasoner can classify individuals automatically
4. Build a realistic healthcare attack scenario with enough detail to properly test everything
5. Make sure the ontology is logically consistent by validating it with a reasoner
6. Critically evaluate how ontology-based approaches relate to Large Language Models

### C. Scope

The ontology I built has 49 classes in total—42 primitive and 7 defined. There are 23 object properties for relationships between concepts, 10 datatype properties for attributes like CVSS scores and timestamps, and 54 individuals that make up the attack scenario. I also added 6 disjoint declarations to prevent logical conflicts and 1 property chain for automatic attack path inference. The focus is specifically on ransomware incident response in healthcare, but the framework could be adapted for other attack types or sectors.

---

## II. RELATED WORK

Researchers have been applying ontologies to cybersecurity for about twenty years now. Undercoffer et al. [1] created an ontology for intrusion detection systems that gave a formal vocabulary for describing network attacks. Their work showed that semantic technologies could help security tools work together better, though they focused mainly on detection rather than response.

Gao et al. [2] built an ontology-based model of network attacks that captured how attack methods, targets, and effects relate to each other. Their approach influenced later work in this area, but it came before OWL 2 [5] features like property chains that allow for more advanced automated reasoning. The MITRE ATT&CK framework [6] has become the standard for describing attacker tactics and techniques, and various researchers have turned it into formal ontologies.

Gruber's well-known definition of ontology as "an explicit specification of a conceptualisation" [9] is still the foundation of the field. In my work, I focused on the relationships between security concepts rather than trying to list every possible security phenomenon. Oltramari et al. [10] built a comprehensive cybersecurity ontology, but their work was done before the recent rise in ransomware and does not cover healthcare-specific compliance like HIPAA.

My approach differs from previous work in a few ways. First, I focus specifically on incident response workflows, not just attack detection or classification. Second, I include healthcare compliance requirements like HIPAA as proper ontological concepts. Third, I use modern OWL 2 DL features—property chains and defined classes—to get more sophisticated automated reasoning than older ontology languages allowed.

---

## III. KNOWLEDGE AND DATA FOR ONTOLOGY DESIGN

I used several knowledge sources to make sure the ontology properly covers the incident response domain. The main sources were the MITRE ATT&CK framework [6], which gave me a structured taxonomy of attacker tactics and techniques, the NIST Cybersecurity Framework [7] for organising security controls and response activities, and the Common Vulnerability Scoring System (CVSS) [8] for assessing vulnerability severity.

I incorporated real-world vulnerability data using CVE identifiers. For instance, CVE-2024-21413 is a critical remote code execution vulnerability in Microsoft Outlook with a CVSS score of 9.8, which I used to model the initial compromise in the scenario. Using actual CVE identifiers makes the ontology reflect realistic attack patterns and allows integration with vulnerability management systems.

For healthcare-specific knowledge, I drew from HIPAA regulations [11] and industry guidance on healthcare security. This covered things like classifying sensitive data types (Protected Health Information), security control requirements, and breach notification procedures. I also incorporated knowledge from security operations to model realistic incident response workflows—containment, eradication, and recovery phases.

I used competency questions to guide the ontology scope: "Which assets are vulnerable to the current threat?", "What security controls are HIPAA-compliant?", "What is the attack path from initial compromise to target asset?", and "What response actions are appropriate for this incident type?". The ontology was designed to answer these questions through reasoning over asserted facts.

---

## IV. METHODOLOGY FOR ONTOLOGY CONSTRUCTION

### A. Development Process

I followed the methodology from Noy and McGuinness [3], adapting it for the cybersecurity domain:

**Step 1 - Specification and Domain Scoping:** Identification of key concepts in ransomware incident response, including assets, threats, vulnerabilities, security controls, incidents, responses, and compliance frameworks. The scope was deliberately constrained to healthcare ransomware incidents to maintain tractability while ensuring sufficient depth for meaningful reasoning.

**Step 2 - Conceptualisation and Domain Research:** Analysis of real ransomware attack case studies, particularly LockBit attacks on healthcare organisations. Real CVE identifiers were researched and incorporated to ground the ontology in actual security knowledge.

**Step 3 - Formalisation and Class Hierarchy Construction:** Creation of main class hierarchies in Protégé with logical organisation. For example, Ransomware was defined as a subclass of Malware, which is a subclass of Threat. This hierarchical structure enables inheritance of properties and supports taxonomic reasoning.

**Step 4 - Property Definition:** Creation of object properties for relationships (exploits, affects, targets, protects) with inverse properties and property chain configuration. Datatype properties were defined for attributes such as CVSS scores, IP addresses, and timestamps.

**Step 5 - Constraint and Axiom Addition:** Disjoint class axioms were added to prevent impossible combinations (e.g., an individual cannot be both an Asset and a Threat). Defined classes using equivalent class expressions were created to enable automatic classification by the reasoner.

**Step 6 - Implementation and Scenario Creation:** Development of the MedCare Hospital scenario with servers, workstations, IP addresses, CVE identifiers, and incident response actions with timestamps. This populated the ABox with realistic individuals for testing.

**Step 7 - Validation:** HermiT reasoner [4] execution for consistency checking and inference verification. All inferences were manually validated against expected results.

### B. Tools and Technologies

I used Protégé 5.6 for development, the de facto standard tool for OWL ontology development. Protégé provides a graphical interface for class hierarchy construction, property definition, and individual creation, while also supporting direct editing of OWL axioms for complex expressions. Key features used included the Classes tab for building hierarchies, Object Properties and Data Properties tabs, Individuals tab for scenario creation, and OntoGraf for visualisation.

The HermiT reasoner [4] was used for consistency checking and inference computation. HermiT implements a hypertableau calculus that is complete for OWL 2 DL, ensuring that all logically valid inferences are computed. The reasoner was invoked regularly during development to identify inconsistencies early and verify that defined classes were correctly classifying individuals.

The ontology was developed using OWL 2 DL [5], the description logic fragment of OWL 2 that guarantees decidability of reasoning while providing expressive constructs including property chains, qualified cardinality restrictions, and complex class expressions. The ontology IRI is http://www.semanticweb.org/ulster/ontologies/2025/cybersecurity.

### C. Challenges and Trade-offs

I encountered several challenges during development. The first challenge involved balancing expressiveness with complexity. More expressive ontologies can capture finer distinctions but become harder to maintain and reason over. The decision was made to focus on a core set of concepts with well-defined semantics rather than attempting to model every possible security concept.

The open world assumption inherent in OWL reasoning required careful consideration. Unlike closed-world databases where absence of a fact implies its negation, OWL assumes that missing information is simply unknown. This necessitated explicit negative assertions in some cases, such as marking vulnerabilities as unpatched (isPatched value false) rather than relying on the absence of a patched assertion.

Temporal reasoning presented another challenge. OWL does not natively support temporal relationships, making it difficult to represent the sequence of events in an attack timeline. While timestamps were captured as datatype properties, the ontology cannot reason about temporal ordering without extensions such as OWL-Time or custom SWRL rules. Defined classes were chosen over SWRL rules for their simpler syntax, better tool support, and easier debugging.

---

## V. ONTOLOGY DESIGN

### A. Core Concepts

I identified nine top-level concepts as fundamental to incident response and declared them mutually disjoint to prevent logical inconsistencies:

**Asset:** I split this into PhysicalAsset (NetworkAsset containing Server, Workstation, NetworkDevice) and DigitalAsset (Database, Application, SensitiveData). This captures both physical infrastructure and the data on it.

**Threat:** This covers harmful entities—Malware (with Ransomware and Trojan as subclasses), NetworkAttack, PhishingAttack, and InsiderThreat. The taxonomy aligns with common security frameworks.

**Vulnerability:** Exploitable weaknesses including SoftwareVulnerability (with ZeroDayVulnerability) and ConfigurationVulnerability. These serve as the bridge between threats and assets.

**SecurityControl:** I split protective measures into PreventiveControl (Firewall, Encryption), DetectiveControl (IDS, SIEM), and CorrectiveControl (BackupSystem). Antivirus is modelled as a subclass of both PreventiveControl and DetectiveControl—this is why those two classes are not disjoint with each other, only with CorrectiveControl.

**SecurityIncident:** Actual security events like DataBreach and RansomwareIncident. Incidents get triggered by threats and handled by responses.

**IncidentResponse:** Response actions following the standard phases—Containment, Eradication, Recovery—aligning with the NIST incident response lifecycle.

**Organization, ComplianceFramework, ThreatActor:** Supporting concepts for ownership (with SecurityTeam as subclass), regulatory standards (HIPAA, NIST_CSF, ISO27001), and attack perpetrators.

[INSERT Fig. 1. Class hierarchy in Protégé showing the nine top-level concepts with expanded subclass structures for Asset, Threat, Vulnerability, and SecurityControl.]

[INSERT Fig. 2. OntoGraf visualisation showing the nine top-level concepts and their object property relationships.]

### B. Object Properties and Property Chain

I defined 23 object properties in total, with 10 inverse pairs for bidirectional navigation. The core attack chain uses three properties: exploits (Threat → Vulnerability), affects (Vulnerability → Asset), and targets (Threat → Asset).

The property chain is the most useful feature I implemented. I configured targets as a subproperty of exploits ∘ affects, written in Description Logic as targets ⊑ exploits ∘ affects. This means if LockBitRansomware exploits SMBv1Enabled, and SMBv1Enabled affects PatientRecordServer, the reasoner automatically infers that LockBitRansomware targets PatientRecordServer without me having to state it explicitly.

The remaining properties cover other relationships: protects/isProtectedBy links controls to assets, mitigates/isMitigatedBy connects controls to threats or vulnerabilities, triggeredBy/triggers and detectedBy/detects handle incident detection, handledBy/handles and performedBy/performs manage response workflow, compliesWith links controls to compliance frameworks, and partOf/hasPart provides transitive containment.

[INSERT Fig. 3. Object Properties tab showing the 'exploits' property with domain (Threat), range (Vulnerability), and inverse property (isExploitedBy).]

### C. Datatype Properties

I created ten datatype properties to capture attributes: hasName (string), hasDescription (string), hasCVSSScore (decimal, 0.0-10.0), hasCVEIdentifier (string), hasSeverityLevel (Critical/High/Medium/Low), hasTimestamp (dateTime), hasIPAddress (string, functional), hasStatus (Active/Resolved/Contained), hasCriticality (Mission-Critical/High/Medium/Low), and isPatched (boolean). I made hasIPAddress a functional property so each NetworkAsset can only have one IP address—if conflicting values were asserted, the reasoner would flag an inconsistency.

### D. Defined Classes for Automated Reasoning

I created seven defined classes to enable automatic classification using equivalent class expressions. I chose these over SWRL rules because of their simpler syntax, better tool support, and easier debugging:

**VulnerableAsset:** Asset AND (isAffectedBy SOME (Vulnerability AND (isPatched VALUE false))). This automatically identifies assets with unpatched vulnerabilities—in the scenario, PatientRecordServer, BillingServer, ReceptionWorkstation, and others get classified.

**ActivelyExploitedVulnerability:** Vulnerability AND (isExploitedBy SOME Threat). This identifies vulnerabilities currently being exploited—CVE_2024_21413, SMBv1Enabled, and WeakPasswordPolicy all match.

**HighSeverityVulnerability:** Vulnerability AND ((hasSeverityLevel VALUE "Critical") OR (hasSeverityLevel VALUE "High")). Four vulnerabilities match this, including CVE_2024_21413 with its CVSS 9.8.

**HIPAACompliantControl:** SecurityControl AND (compliesWith VALUE HIPAA). Nine controls get automatically identified as HIPAA-compliant, which is useful for compliance reporting.

I also created ProtectedAsset (assets with security controls), DetectedIncident (incidents detected by controls), and MitigatedThreat (threats with mitigation controls in place).

[INSERT Fig. 4. Defined class expression for VulnerableAsset showing the equivalent class axiom in Protégé.]

---

## VI. ONTOLOGY EVALUATION: MEDCARE HOSPITAL CASE STUDY

### A. Scenario Overview

I validated the ontology using a realistic scenario based on a LockBit ransomware attack against MedCare Hospital, a fictional healthcare facility with around 500 employees. I designed the scenario to test all major ontology features—property chains, defined classes, and compliance reasoning.

### B. Attack Timeline

The scenario draws on documented LockBit attack patterns [13].

**Day 1 - Initial Compromise (November 15, 2025, 14:32):** A spear phishing email was sent to reception staff exploiting CVE-2024-21413, a critical Outlook remote code execution vulnerability with CVSS 9.8. ReceptionWorkstation got infected and a Cobalt Strike beacon was deployed for command and control.

**Day 1 - Lateral Movement:** The attacker exploited WeakPasswordPolicy to steal credentials and used the SMBv1Enabled vulnerability to move laterally through the network. PatientRecordServer and BillingServer were compromised, putting 12,000 patient records at risk—a potential HIPAA breach.

**Day 1 - Detection (15:10):** SplunkSIEM detected anomalous network activity and CrowdStrikeEDR identified malicious processes. MedCareSOC was alerted and started incident response procedures.

**Days 1-3 - Response:** The response followed standard phases. Containment: NetworkIsolation at CoreSwitch, EndpointQuarantine via CrowdStrike (15 endpoints). Eradication: MalwareRemoval, CredentialReset for all Active Directory passwords. Recovery: SystemRestore from VeeamBackup, PatchDeployment for CVE-2024-21413 and SMBv1 disabling.

### C. Reasoning Results and Validation

I ran HermiT and the ontology passed consistency checking with no errors—no disjoint violations, all property constraints satisfied, and no logical contradictions.

The property chain worked exactly as intended. Because LockBitRansomware exploits SMBv1Enabled, and SMBv1Enabled affects PatientRecordServer, the reasoner inferred that LockBitRansomware targets PatientRecordServer without me stating it directly.

Nine assets were automatically classified as VulnerableAsset: ReceptionWorkstation, NurseStation01, AdminWorkstation, PatientRecordServer, BillingServer, DomainController, EmployeeCredentials, OutlookClient, and PatientDatabase. The transitive partOf property also worked correctly—PatientPHI partOf PatientRecordServer was inferred through the intermediate PatientDatabase.

For compliance, nine security controls were automatically tagged as HIPAACompliantControl including PaloAltoFirewall, SplunkSIEM, CrowdStrikeEDR, and VeeamBackup. This kind of automatic classification would be useful for breach documentation in a real incident.

[INSERT Fig. 5. HermiT reasoner results showing ontology consistency and automatic classification of individuals as VulnerableAsset.]

[INSERT Fig. 6. LockBitRansomware individual showing asserted 'exploits' relationships and inferred 'targets' relationships derived from the property chain.]

---

## VII. ONTOLOGY AND LARGE LANGUAGE MODELS

### A. Complementary Strengths

The relationship between ontologies and Large Language Models is one of the most interesting areas in AI right now. These technologies come from different traditions—ontologies from symbolic AI and knowledge representation, LLMs from statistical machine learning—but they have complementary strengths that make integration worth exploring.

Ontologies give you formal, explicit specifications of domain knowledge with precise semantics. They enable deductive reasoning that guarantees logical consistency and completeness—every inference from an OWL reasoner is provably correct given the axioms. There are no hallucinations or made-up facts. This makes ontologies well-suited for domains needing high assurance, like healthcare, aerospace, and financial regulation.

LLMs, on the other hand, are good at natural language understanding, generation, and flexible reasoning over unstructured text. They can handle ambiguous, incomplete, or contextual information that formal systems struggle with. LLMs can do abductive reasoning, generating plausible hypotheses that might not be logically entailed by explicit knowledge, and they make information accessible to non-experts.

### B. Integration Opportunities

Recent research has identified several integration strategies. Ontology-grounded LLMs use ontological knowledge to constrain or guide LLM outputs, which reduces hallucination and improves factual accuracy. For instance, an LLM generating incident response recommendations could be limited to suggesting only controls defined in the ontology and marked appropriate for the threat type.

LLM-assisted ontology engineering uses language models to speed up ontology development—things like term extraction, relationship identification, and generating axioms from natural language sources. This tackles a major barrier to ontology adoption: the expertise and effort needed to build them.

Retrieval-augmented generation (RAG) systems can use ontologies as structured knowledge bases, with the LLM pulling relevant ontological facts to inform its responses. The ontology I built could work as a knowledge source for an LLM-based security assistant. Pan et al. [12] provide a roadmap for unifying knowledge graphs and LLMs, covering paradigms like KG-enhanced LLMs, LLM-augmented KGs, and synergised systems.

In cybersecurity specifically, LLMs could parse unstructured threat intelligence reports and extract entities to populate the ontology. The ontology could then constrain LLM outputs to prevent recommendations of deprecated security controls or technically inaccurate assessments. A natural language interface could let analysts query the ontology in plain English—asking something like "What assets are vulnerable to the current attack?" and getting structured, accurate responses.

### C. Limitations and Pitfalls

Despite the potential synergies, integrating ontologies and LLMs has real challenges. Semantic alignment is tricky—ontologies define terms with precise formal semantics, while LLMs represent meaning through statistical distributions over tokens. The same term can mean slightly different things in each system, causing errors when you try to integrate outputs.

Ontologies struggle with temporal reasoning and uncertainty, which is where LLMs are more flexible. In my MedCare scenario, I could not reason about the attack timeline temporally within OWL, so the ontology cannot answer questions about what happened in what order or when to respond.

LLMs have well-known problems: hallucination, inconsistency, and sensitivity to how you phrase prompts. If you use LLM outputs directly as ontology assertions, errors could propagate through reasoning. For security decisions, you need certainty that answers come from actual data, not LLM pattern-matching. Validation and human oversight are essential for any integration approach.

Scalability is also challenging but in different ways. Ontology reasoning gets computationally expensive with large ABoxes, while LLMs need significant resources for inference. Any hybrid system has to balance these costs while keeping response times acceptable.

### D. Future Integration Strategies

Cybersecurity offers good opportunities for ontology-LLM integration. An LLM could act as a natural language interface to the incident response ontology, translating analyst queries into SPARQL or DL queries and explaining the reasoning results in plain language. This would make ontologies more accessible to people who are not experts in semantic technologies.

On the flip side, the ontology could provide a structured backbone for LLM-based security analysis, making sure that generated threat assessments reference valid CVE identifiers, use appropriate CVSS scoring, and recommend controls that are actually defined in the knowledge base. Neurosymbolic architectures that tightly couple neural and symbolic components are the most ambitious integration approach—the goal is to combine learning capabilities with reasoning guarantees.

---

## VIII. DISCUSSION

### A. Strengths and Contributions

The ontology I built demonstrates several useful capabilities. The property chain for attack path inference automates what would otherwise need manual tracing of exploit chains—you just need to know what vulnerabilities a threat exploits and what assets have those vulnerabilities. The VulnerableAsset defined class automatically identifies assets needing remediation, which is valuable for prioritising patching in a real SOC. The HIPAACompliantControl class helps with compliance reporting by automatically pulling together relevant controls.

The ontology gives a unified conceptual model that connects technical security data (CVEs, IP addresses) with compliance requirements (HIPAA) and organisational structure (security teams, response procedures). This integration supports a holistic approach to incident response that considers technical, regulatory, and organisational factors at the same time.

### B. Limitations

The current implementation has several limitations. There is no temporal reasoning, so I cannot analyse attack sequences or optimise response timing—timestamps are captured as data but the reasoner cannot work out whether one event happened before another. Risk scoring is not integrated either; while I capture CVSS scores and asset criticality as datatype properties, the ontology does not combine them into an aggregate risk score without SWRL rules or external computation.

The scale of my scenario (54 individuals) is fairly modest—a real enterprise environment would have thousands of assets, which would need attention to reasoning performance and possibly ontology modularisation. Choosing defined classes over SWRL rules simplified development but limits some computational capabilities.

### C. Future Work

There are several directions I could take this work in the future. Adding more defined classes could support risk prioritisation—automatically classifying assets as high-risk based on combinations of vulnerability severity and asset criticality. Integrating with a SPARQL endpoint would allow more flexible querying and connection with security information systems. Adding temporal reasoning through OWL-Time or similar extensions would let me analyse attack sequences properly. Testing with larger scenarios would help identify performance issues and optimisation needs. Finally, integrating with LLM-based security tools could provide natural language interfaces while keeping the formal semantic grounding.

---

## IX. CONCLUSION

This paper described how I developed and evaluated a cybersecurity ontology for incident response in healthcare settings. The ontology has 49 classes organised into 9 hierarchies, 23 object properties including a property chain for attack path inference, 10 datatype properties, 7 defined classes for automatic reasoning, and 54 individuals modelling a realistic LockBit ransomware attack at MedCare Hospital.

The property chain for automatic attack path inference and the defined classes for automatic classification turned out to be the most useful features, showing practical applications of semantic technologies in security operations. The VulnerableAsset and HIPAACompliantControl classes were particularly helpful for operational security and compliance reporting.

Looking at how ontologies and LLMs relate, I found they have complementary strengths: ontologies provide formal semantics and guaranteed reasoning while LLMs offer natural language processing and flexible interpretation. Integration strategies like ontology-grounded generation, LLM-assisted ontology engineering, and retrieval-augmented generation look promising, though challenges around semantic alignment and hallucination prevention still need to be solved.

Ontologies remain valuable in domains that need formal semantics, guaranteed reasoning, and explicit knowledge representation. Healthcare cybersecurity is a good example of this—regulatory compliance, patient safety, and the need for auditable decisions all favour explicit, verifiable knowledge structures. Future work should look at tighter integration between ontological reasoning and LLM-based natural language interfaces, letting security analysts query formal knowledge using conversational language while keeping the guarantees that formal methods provide.

---

## REFERENCES

[1] J. Undercoffer, A. Joshi, and J. Pinkston, "Modeling Computer Attacks: An Ontology for Intrusion Detection," in RAID Workshop, 2003.

[2] J. B. Gao et al., "Ontology-Based Model of Network Attacks," Journal of Shanghai Jiaotong University, vol. 18, pp. 554-562, 2013.

[3] N. F. Noy and D. L. McGuinness, "Ontology Development 101: A Guide to Creating Your First Ontology," Stanford Knowledge Systems Laboratory, 2001.

[4] B. Glimm, I. Horrocks, B. Motik, G. Stoilos, and Z. Wang, "HermiT: An OWL 2 Reasoner," Journal of Automated Reasoning, vol. 53, no. 3, pp. 245-269, 2014.

[5] W3C, "OWL 2 Web Ontology Language Document Overview," 2012. [Online]. Available: https://www.w3.org/TR/owl2-overview/

[6] MITRE, "ATT&CK Framework." [Online]. Available: https://attack.mitre.org/

[7] NIST, "Framework for Improving Critical Infrastructure Cybersecurity, Version 1.1," 2018.

[8] FIRST, "Common Vulnerability Scoring System v3.1," 2019. [Online]. Available: https://www.first.org/cvss/

[9] T. R. Gruber, "A Translation Approach to Portable Ontology Specifications," Knowledge Acquisition, vol. 5, no. 2, pp. 199-220, 1993.

[10] A. Oltramari et al., "Building an Ontology of Cyber Security," in STIDS, 2014.

[11] U.S. Department of Health and Human Services, "HIPAA Security Rule." [Online]. Available: https://www.hhs.gov/hipaa/

[12] S. Pan et al., "Unifying Large Language Models and Knowledge Graphs: A Roadmap," IEEE Trans. Knowledge and Data Engineering, 2024.

[13] CISA, "LockBit 3.0 Ransomware Affiliates Exploit CVE 2023-4966 Citrix Bleed Vulnerability," Cybersecurity Advisory, 2023.
