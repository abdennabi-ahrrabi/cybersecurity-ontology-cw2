# Cybersecurity Ontology

**Author:** Abdennabi Ahrrabi
**Institution:** Ulster University
**Course:** Knowledge Graphs and Semantic Web
**Format:** OWL 2 DL (Web Ontology Language)
**Tool:** Protégé 5.6.0 Desktop Edition
**URI:** http://www.semanticweb.org/ontologies/cybersecurity#

---

## Overview

This is a comprehensive cybersecurity ontology developed using Protégé ontology editor. The ontology models cybersecurity domain knowledge including threats, vulnerabilities, assets, security controls, and their complex relationships. It incorporates advanced OWL 2 DL features and SWRL production rules for automated reasoning and formal verification.

## Ontology Statistics

- **Total Classes:** 264 (9 main hierarchies)
- **Total Object Properties:** 28 (with 25+ inverse pairs)
- **Total Datatype Properties:** 30
- **Total Individuals:** 28 (realistic security scenarios)
- **SWRL Production Rules:** 10
- **File Size:** 112 KB (RDF/XML format)

---

## Main Class Hierarchies

### 1. Asset (74 classes)
Protected resources organized into:
- **PhysicalAsset** (19): Servers, workstations, network devices, storage
- **DigitalAsset** (22): Applications, data, operating systems, credentials
- **CloudAsset** (20): Compute resources, cloud storage, cloud services
- **OrganizationalAsset** (8): Human resources, intellectual property

### 2. Threat (44 classes)
Security threats categorized by type:
- **Malware** (9): Virus, worm, trojan, ransomware, spyware, rootkit
- **NetworkThreat** (7): DDoS, man-in-the-middle, port scanning
- **SocialEngineering** (8): Phishing, spear phishing, whaling
- **WebThreat** (6): SQL injection, XSS, CSRF, RCE
- **PhysicalThreat** (4): Theft, sabotage, unauthorized access
- **InsiderThreat** (3): Malicious, negligent, compromised

### 3. Vulnerability (36 classes)
Security weaknesses by component:
- **SoftwareVulnerability** (9): Buffer overflow, privilege escalation, zero-day
- **HardwareVulnerability** (3): Firmware flaws, side-channel attacks
- **ConfigurationVulnerability** (6): Default credentials, open ports
- **HumanVulnerability** (5): Lack of awareness, password reuse
- **NetworkVulnerability** (3): Unsecured WiFi, weak segmentation
- **CryptographicVulnerability** (3): Weak ciphers, poor key management

### 4. SecurityControl (62 classes)
Security measures organized by type:
- **TechnicalControl** (38): Firewalls, IDS/IPS, encryption, MFA, SIEM
- **AdministrativeControl** (15): Policies, training, incident response
- **PhysicalControl** (9): Perimeter security, surveillance, access control

### 5. Other Core Classes
- **ThreatActor** (8 types): Nation-states, cybercriminals, hacktivists, APTs
- **SecurityEvent** (12 types): Data breaches, incidents, alerts
- **User** (6 types): Administrators, regular users, privileged accounts
- **Environment** (8 types): Production, development, staging, cloud
- **ComplianceFramework** (8): GDPR, HIPAA, PCI-DSS, ISO 27001, NIST

---

## Key Features

### Advanced OWL 2 DL Features

**Inverse Properties (25+ pairs)**
- All major relationships have inverse properties enabling bidirectional navigation
- Examples: exploits ⟷ isExploitedBy, targets ⟷ isTargetedBy, protects ⟷ isProtectedBy

**Transitive Properties**
- `dependsOn`: Asset dependency chain inference
- `contains/isContainedIn`: Nested asset structure support

**Symmetric Properties**
- `communicatesWith`: Bidirectional communication relationships

**Property Chain Axioms**
- `targets ⊑ exploits ∘ affects`: Infers threat targets from vulnerability exploitation

**Disjoint Class Axioms**
- Asset types mutually exclusive (Physical ⊥ Digital ⊥ Cloud ⊥ Organizational)
- Threat categories disjoint (Malware ⊥ PhysicalThreat ⊥ SocialEngineering)
- Prevents logical inconsistencies

**Cardinality Constraints**
- SecurityEvent: exactly 1 hasTimestamp, exactly 1 hasSeverity
- Ensures data completeness and integrity

**Enumerated Datatypes**
- hasSeverity restricted to: {Critical, High, Medium, Low}
- Prevents invalid severity values

### SWRL Production Rules (10 rules)

1. **High-Risk Asset Detection**: Assets with CVSS > 7.0 classified as HighRiskAsset
2. **Critical Asset Protection**: Business-critical assets flagged for mandatory protection
3. **Incident Response Trigger**: Critical malware events trigger incident response
4. **Coordinated Attack Detection**: Multi-vector attacks from same actor identified
5. **Exploit Available Alert**: Exploitable vulnerabilities on critical assets flagged
6. **Zero-Day Classification**: Threats exploiting zero-days specially classified
7. **Ransomware Breach Risk**: Ransomware targeting personal data flagged for GDPR
8. **Urgent Patching Alert**: Critical vulnerabilities in production prioritized
9. **APT Detection**: Repeated high-level attacks identify sophisticated actors
10. **Insider Threat Assessment**: Privileged users with suspicious activity flagged

---

## Getting Started with Protégé

### Opening the Ontology

1. **Download and Install Protégé**
   - Download from: https://protege.stanford.edu/
   - Install version 5.6.0 or later

2. **Open the Ontology**
   - Launch Protégé
   - File → Open
   - Select `CybersecurityOntology_ENHANCED.owl`

3. **Explore the Class Hierarchy**
   - Navigate to **Classes** tab
   - Expand class hierarchies (Asset, Threat, Vulnerability, etc.)
   - View class descriptions and annotations

### Using the Ontology in Protégé

#### Exploring Classes

1. Click **Classes** tab
2. Browse hierarchies:
   - Asset → PhysicalAsset → ComputingDevice → Server
   - Threat → Malware → Ransomware
   - Vulnerability → SoftwareVulnerability → ZeroDayVulnerability
3. Select a class to view:
   - Description
   - Annotations (labels, comments)
   - Usage (superclasses, restrictions)

#### Viewing Properties

1. Click **Object Properties** tab
   - View relationships: exploits, targets, protects, mitigates
   - Check inverse properties, domains, ranges

2. Click **Data Properties** tab
   - View attributes: hasSeverity, hasCVSS, hasTimestamp
   - Check constraints and ranges

#### Examining Individuals

1. Click **Individuals** tab
2. Browse instances:
   - WebServer_001, DatabaseServer_Main
   - WannaCry_Variant, APT29_Cozy_Bear
   - SQLi_Vulnerability_001
3. View property assertions and relationships

#### Running the Reasoner

1. **Select Reasoner**
   - Reasoner → HermiT (recommended)
   - Or: Pellet (for SWRL rules)

2. **Start Reasoning**
   - Reasoner → Start reasoner
   - Wait for classification (~6 seconds)

3. **View Results**
   - Check consistency: Should show "Consistent"
   - View inferred class hierarchy
   - See inferred relationships (property chains, SWRL rules)

#### Visualizing with OntoGraf

1. **Open OntoGraf**
   - Window → Tabs → OntoGraf

2. **Visualize Classes**
   - Drag "Asset" class to canvas
   - Right-click → Show subclasses
   - Drag "Threat" class to canvas
   - Right-click → Show subclasses

3. **Visualize Individuals**
   - Drag "WebServer_001" to canvas
   - Right-click → Show relationships
   - Observe connections to vulnerabilities, threats, controls

#### Working with SWRL Rules

1. **View SWRL Rules**
   - Window → Tabs → SWRLTab
   - View 10 production rules

2. **Test Rules with Pellet**
   - Reasoner → Pellet
   - Reasoner → Start reasoner
   - Rules fire automatically
   - View inferred classifications

---

## Object Properties (Relationships)

| Property | Domain | Range | Inverse | Description |
|----------|--------|-------|---------|-------------|
| exploits | Threat | Vulnerability | isExploitedBy | Threat exploits vulnerability |
| targets | Threat | Asset | isTargetedBy | Threat targets asset |
| affects | Vulnerability | Asset | isAffectedBy | Vulnerability affects asset |
| hasVulnerability | Asset | Vulnerability | - | Asset has vulnerability |
| protects | SecurityControl | Asset | isProtectedBy | Control protects asset |
| mitigates | SecurityControl | Threat | isMitigatedBy | Control mitigates threat |
| remediates | SecurityControl | Vulnerability | isRemediatedBy | Control remediates vulnerability |
| detects | SecurityControl | Threat | isDetectedBy | Control detects threat |
| causedBy | SecurityEvent | Threat | causes | Event caused by threat |
| initiatedBy | Threat | ThreatActor | initiates | Threat initiated by actor |
| ownedBy | Asset | User | owns | Asset owned by user |
| locatedIn | Asset | Environment | hosts | Asset located in environment |
| dependsOn | Asset | Asset | - | Asset depends on asset (transitive) |
| contains | Asset | Asset | isContainedIn | Asset contains asset (transitive) |
| communicatesWith | Asset | Asset | - | Bidirectional communication (symmetric) |
| hasAccess | User | Asset | isAccessedBy | User has access to asset |
| performs | User | SecurityEvent | isPerformedBy | User performs event |
| compliesWith | SecurityControl | ComplianceFramework | requires | Control complies with framework |
| generates | Asset | SecurityEvent | isGeneratedBy | Asset generates event |
| respondsTo | SecurityControl | SecurityEvent | isRespondedToBy | Control responds to event |

---

## Datatype Properties (Attributes)

### Identification
- hasName (string), hasID (string), hasDescription (string)

### Risk & Severity
- **hasSeverity** (enumerated: Critical, High, Medium, Low)
- hasCVSS (float, 0.0-10.0)
- hasRiskLevel (string)
- hasThreatLevel (string)
- hasPriority (string)

### Temporal
- hasTimestamp (string)
- hasDiscoveryDate (string)
- hasPublicationDate (string)
- hasPatchDate (string)

### Network
- hasIPAddress (string)
- hasMACAddress (string)
- hasHostname (string)
- hasSourceIP (string)
- hasDestinationIP (string)

### Vulnerability
- hasCVE (string, format: CVE-YYYY-NNNN)
- hasCWE (string, format: CWE-NNN)
- hasExploitAvailable (boolean)

### User
- hasUsername (string, functional)
- hasEmail (string)
- hasRole (string)

### Asset
- hasAssetValue (string)
- hasVersion (string)

### Control
- hasImplementationStatus (string)
- hasEffectiveness (string)

### Event
- hasStatus (string)
- hasImpact (string)
- hasConfidence (string)

---

## Sample Individuals

The ontology includes 28 individuals representing realistic security scenarios:

**Assets:**
- WebServer_001: Production web server (IP: 192.168.1.100)
- DatabaseServer_Main: Customer database server
- CustomerDatabase: PII database (GDPR-protected)

**Vulnerabilities:**
- SQLi_Vulnerability_001: CVE-2025-1234, CVSS 8.5, exploit available
- OutdatedApache_001: Apache 2.4.29 vulnerabilities
- DefaultCreds_Router_001: Default credentials on router

**Threats:**
- WannaCry_Variant: Ransomware targeting SMB
- PhishingCampaign_2025Q1: Spear phishing campaign
- DDoS_Attack_001: Distributed denial of service

**Threat Actors:**
- APT29_Cozy_Bear: Russian nation-state actor
- RansomwareGroup_001: Cybercriminal ransomware operator

**Security Controls:**
- CorporateFirewall_Main: Perimeter firewall
- IDS_Network_001: Network intrusion detection
- MFA_System: Multi-factor authentication
- SIEM_Main: Security information and event management

**Security Events:**
- DataBreach_2025_001: Critical breach event (2025-03-15)
- FailedLogin_001: Failed login attempt
- AnomalyEvent_001: Anomaly detection alert

---

## Use Cases

### 1. Security Risk Assessment
**Query:** Find critical assets with high-severity vulnerabilities
**Protégé:** Use DL Query tab or SPARQL

### 2. Attack Path Analysis
**Query:** Trace threat → vulnerability → asset relationships
**Protégé:** OntoGraf visualization with relationships

### 3. Compliance Mapping
**Query:** Map security controls to GDPR/PCI-DSS requirements
**Protégé:** Query compliesWith relationships

### 4. Incident Response
**Query:** Identify events requiring incident response (SWRL Rule 3)
**Protégé:** Run Pellet reasoner, check inferred IncidentResponseRequired class

### 5. Control Coverage Analysis
**Query:** Find unprotected critical assets
**Protégé:** SPARQL or DL Query for assets without protects relationships

### 6. Threat Intelligence
**Query:** Link threat actors to TTPs and targets
**Protégé:** OntoGraf visualization of initiatedBy and targets

### 7. Vulnerability Management
**Query:** Prioritize patching based on CVSS and exploit availability
**Protégé:** Query HighRiskAsset class (inferred by SWRL Rule 1)

### 8. Zero-Day Response
**Query:** Identify threats exploiting zero-day vulnerabilities
**Protégé:** Run reasoner, check ZeroDayThreat class (SWRL Rule 6)

---

## SPARQL Query Examples

### Query 1: Find High-Risk Assets (CVSS > 7.0)
```sparql
PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#>
SELECT ?asset ?vuln ?cvss
WHERE {
  ?asset :hasVulnerability ?vuln .
  ?vuln :hasCVSS ?cvss .
  FILTER (?cvss > 7.0)
}
```

### Query 2: Find Unprotected Critical Assets
```sparql
PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#>
SELECT ?asset
WHERE {
  ?asset a :Asset .
  ?asset :hasAssetValue "Critical" .
  FILTER NOT EXISTS { ?control :protects ?asset }
}
```

### Query 3: Threat Attribution (Nation-State Actors)
```sparql
PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#>
SELECT ?threat ?actor ?asset
WHERE {
  ?threat :initiatedBy ?actor .
  ?threat :targets ?asset .
  ?actor a :NationState .
}
```

### Query 4: Find Exploitable Vulnerabilities
```sparql
PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#>
SELECT ?vuln ?cve ?asset
WHERE {
  ?vuln :hasCVE ?cve .
  ?vuln :hasExploitAvailable true .
  ?vuln :affects ?asset .
}
```

**To run SPARQL in Protégé:**
1. Window → Tabs → SPARQL Query
2. Paste query
3. Click Execute

---

## Reasoning and Validation

### Consistency Checking

The ontology has been validated for logical consistency:

✅ **Consistent**: No logical contradictions
✅ **All classes satisfiable**: No unsatisfiable classes
✅ **Disjoint axioms verified**: No violations
✅ **Cardinality constraints met**: All individuals satisfy constraints
✅ **Property domains/ranges valid**: No type conflicts

**To verify in Protégé:**
1. Reasoner → HermiT → Start reasoner
2. Check for "Consistent" status (no errors)
3. View "Entities" tab for any unsatisfiable classes (should be none)

### Inference Testing

**Property Chain Inference:**
```
Given:
  WannaCry exploits SMBv1_Vulnerability
  SMBv1_Vulnerability affects FileServer_001

Reasoner Infers:
  WannaCry targets FileServer_001
```

**SWRL Rule Inference (Rule 1):**
```
Given:
  WebServer_001 hasVulnerability SQLi_Vulnerability_001
  SQLi_Vulnerability_001 hasCVSS 8.5

Reasoner Infers:
  WebServer_001 is HighRiskAsset (because 8.5 > 7.0)
```

**To test inferences in Protégé:**
1. Reasoner → Pellet → Start reasoner
2. Check inferred class hierarchy
3. View individuals' inferred types

---

## Industry Standards Integration

The ontology aligns with major cybersecurity frameworks:

| Standard | Coverage | Details |
|----------|----------|---------|
| **MITRE ATT&CK** | ✅ Aligned | Threat taxonomy based on ATT&CK |
| **NIST CSF** | ✅ Mapped | Security controls mapped to functions |
| **CIS Controls v8** | ✅ Integrated | Control hierarchy follows CIS |
| **OWASP Top 10** | ✅ Included | Web threats cover OWASP 2021 |
| **CVE** | ✅ Supported | hasCVE property with CVE IDs |
| **CWE** | ✅ Supported | hasCWE property for weakness types |
| **CVSS v3.1** | ✅ Implemented | hasCVSS with 0.0-10.0 scoring |
| **GDPR** | ✅ Compliance | PersonalData class for GDPR scope |
| **PCI-DSS** | ✅ Compliance | FinancialData class for payment data |
| **ISO 27001** | ✅ Compatible | Control categories align with ISO |

---

## Files Included

- **CybersecurityOntology_ENHANCED.owl** (112 KB) - Main ontology file in RDF/XML format
- **CybersecurityOntology_SWRL_Rules.swrl** (25 KB) - SWRL production rules (separate file)
- **TECHNICAL_REPORT_Ontology_Enhancement.md** - Comprehensive technical report
- **README.md** - This documentation
- **INDEX.md** - Project file index and overview

---

## Extending the Ontology

The ontology is designed for easy extension:

### Adding New Classes

1. Open ontology in Protégé
2. Select parent class (e.g., Malware)
3. Click "Add subclass" button
4. Name new class (e.g., Cryptojacker)
5. Add annotations (label, comment)

### Adding New Properties

1. Navigate to Object Properties or Data Properties tab
2. Click "Add property" button
3. Define domain and range
4. Add inverse property if applicable
5. Set characteristics (transitive, symmetric, etc.)

### Adding New Individuals

1. Navigate to Individuals tab
2. Select class (e.g., Server)
3. Click "Add individual" button
4. Name individual (e.g., WebServer_002)
5. Add property assertions (hasIPAddress, locatedIn, etc.)

### Adding New SWRL Rules

1. Window → Tabs → SWRLTab
2. Click "New Rule"
3. Enter SWRL syntax
4. Enable rule
5. Run Pellet reasoner to test

---

## Requirements

- **Protégé**: Version 5.6.0 or later
- **Java**: JRE 8 or later (required by Protégé)
- **Reasoners**: HermiT, Pellet (bundled with Protégé)
- **Optional**: SPARQL Query plugin, OntoGraf plugin

**Download Protégé:** https://protege.stanford.edu/software.php

---

## Academic Context

This ontology was developed for the **Knowledge Graphs and Semantic Web** course at Ulster University, demonstrating:

1. **Production System**: 10 SWRL forward-chaining rules
2. **SAT-based Reasoning**: HermiT reasoner (propositional logic)
3. **First-Order Logic Reasoning**: OWL 2 DL (SROIQ description logic)
4. **Formal Verification**: Consistency, satisfiability, completeness checking

---

## License & Attribution

**Author:** Abdennabi Ahrrabi
**Institution:** Ulster University
**Purpose:** Academic coursework and research
**Date:** November 2025

---

## Additional Resources

### Learning Resources
- **Protégé Tutorial:** https://protegewiki.stanford.edu/wiki/Protege4UserDocs
- **OWL 2 Primer:** https://www.w3.org/TR/owl2-primer/
- **SWRL Guide:** https://github.com/protegeproject/swrlapi/wiki

### Ontology Engineering References
- Noy & McGuinness (2001): "Ontology Development 101"
- Gruber (1993): "A Translation Approach to Portable Ontology Specifications"

### Cybersecurity References
- MITRE ATT&CK: https://attack.mitre.org/
- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
- OWASP Top 10: https://owasp.org/www-project-top-ten/

---

**Happy Exploring!**

For questions or issues, consult the technical report (TECHNICAL_REPORT_Ontology_Enhancement.md) for detailed documentation of design decisions and implementation details.
