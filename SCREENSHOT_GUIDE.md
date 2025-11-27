# Screenshot Guide for Cybersecurity Incident Response Ontology

This guide shows WHERE to take screenshots in Protégé and the DL queries to demonstrate for your coursework report.

**Ontology File:** `CybersecurityOntology_Focused.owl`

---

## 📸 Screenshot 1: Class Hierarchy

**What to Capture:** Classes tab showing the ontology structure

**Steps:**
1. Open `CybersecurityOntology_Focused.owl` in Protégé
2. Click on **Classes** tab
3. Expand **Asset** → **PhysicalAsset** → **NetworkAsset** → Show Server, Workstation, NetworkDevice
4. Also expand **Threat** → **Malware** → Show Ransomware, Trojan
5. Take screenshot showing the class hierarchy

**Figure Caption:**
```
Figure 1: Protégé Classes tab showing the Asset and Threat class hierarchies with subclasses
```

---

## 📸 Screenshot 2: Object Properties

**What to Capture:** Object Properties tab with property details

**Steps:**
1. Click on **Object properties** tab
2. Select the **exploits** property
3. Right panel should show:
   - Domain: Threat
   - Range: Vulnerability
   - Inverse: isExploitedBy
4. Take screenshot

**Figure Caption:**
```
Figure 2: Object Properties showing 'exploits' property with domain Threat, range Vulnerability, and inverse property
```

---

## 📸 Screenshot 3: Data Properties

**What to Capture:** Data Properties tab

**Steps:**
1. Click on **Data properties** tab
2. Select **hasCVSSScore**
3. Show Domain: Vulnerability, Range: xsd:decimal
4. Take screenshot

**Figure Caption:**
```
Figure 3: Data Properties showing hasCVSSScore with domain Vulnerability and range decimal
```

---

## 📸 Screenshot 4: Individuals (Instances)

**What to Capture:** Individuals tab showing the scenario instances

**Steps:**
1. Click on **Individuals** tab
2. Select **PatientRecordServer**
3. Right panel shows:
   - Types: Server
   - Object property assertions: hasOwner MedCareHospital
   - Data property assertions: hasName "PROD-EHR-01", hasIPAddress "10.1.10.50", hasCriticality "Mission-Critical"
4. Take screenshot

**Figure Caption:**
```
Figure 4: Individual PatientRecordServer showing type assertions and property values
```

---

## 📸 Screenshot 5: OntoGraf Visualization

**What to Capture:** Visual graph of ontology relationships

**Steps:**
1. Go to **Window → Tabs → OntoGraf**
2. Drag these classes to canvas: Asset, Threat, Vulnerability, SecurityControl
3. Right-click each → **Show subclasses**
4. Arrange for clear layout
5. Take screenshot

**Figure Caption:**
```
Figure 5: OntoGraf visualization showing core ontology classes and their hierarchical relationships
```

---

## 📸 Screenshot 6: HermiT Reasoner - Consistency

**What to Capture:** Reasoner confirming ontology is consistent

**Steps:**
1. Go to **Reasoner → HermiT**
2. Click **Reasoner → Start reasoner**
3. Wait for completion
4. Bottom status bar shows: "Ontology is consistent"
5. Take screenshot showing the status

**Figure Caption:**
```
Figure 6: HermiT reasoner confirming ontology consistency with no logical contradictions
```

---

## 📸 Screenshot 7: DL Query - Asset Query

**What to Capture:** DL Query results for Asset class

**Steps:**
1. Go to **Window → Tabs → DL Query**
2. Type: `Asset`
3. Check: ☑ Instances
4. Click **Execute**
5. Take screenshot showing query and results

**Figure Caption:**
```
Figure 7: DL Query returning all Asset instances including servers, workstations, and databases
```

---

## 📸 Screenshot 8: DL Query - Defined Class Inference

**What to Capture:** Reasoner inferring ActivelyExploitedVulnerability

**Steps:**
1. In DL Query tab
2. Type: `ActivelyExploitedVulnerability`
3. Check: ☑ Instances
4. Click **Execute**
5. Results should show: CVE_2024_21413, SMBv1Enabled, WeakPasswordPolicy
6. Take screenshot

**Figure Caption:**
```
Figure 8: Reasoner automatically classifying vulnerabilities as ActivelyExploitedVulnerability based on defined class axiom
```

---

## 📸 Screenshot 9: Attack Scenario Visualization

**What to Capture:** OntoGraf showing attack chain

**Steps:**
1. In OntoGraf tab
2. Drag these individuals to canvas:
   - LockBitRansomware
   - CVE_2024_21413
   - PatientRecordServer
   - MedCareRansomwareIncident
3. Right-click each → **Show relationships**
4. Arrange to show attack flow
5. Take screenshot

**Figure Caption:**
```
Figure 9: Attack chain visualization showing LockBit ransomware exploiting vulnerability to target patient records server
```

---

## 📸 Screenshot 10: Incident Response Timeline

**What to Capture:** Individuals showing response actions

**Steps:**
1. In Individuals tab
2. Select **NetworkIsolation** (Containment)
3. Show its properties: handles MedCareRansomwareIncident, performedBy MedCareSOC
4. Take screenshot

**Figure Caption:**
```
Figure 10: Incident response action showing containment performed by SOC team
```

---

## 🔍 DL Query Examples for Screenshots

### Basic Class Queries

```
Asset
```
Returns: All 20+ assets (servers, workstations, databases, applications, sensitive data)

```
Server
```
Returns: PatientRecordServer, BillingServer, EmailServer, DomainController, BackupServer, PharmacyServer, LaboratoryServer, RadiologyServer

```
Threat
```
Returns: LockBitRansomware, InitialPhishing, CobaltStrikeTrojan, LateralMovement

```
Vulnerability
```
Returns: CVE_2024_21413, CVE_2024_3400, WeakPasswordPolicy, SMBv1Enabled, UnpatchedSQLServer

```
SecurityControl
```
Returns: All firewalls, SIEM, EDR, IDS, encryption, backup systems

---

### Defined Class Queries (Reasoner Inferred) - 7 Defined Classes!

```
ActivelyExploitedVulnerability
```
**Expected:** CVE_2024_21413, SMBv1Enabled, WeakPasswordPolicy
(Vulnerabilities that have `isExploitedBy some Threat`)

```
DetectedIncident
```
**Expected:** MedCareRansomwareIncident, PHIDataBreach
(Incidents that have `detectedBy some SecurityControl`)

```
HighSeverityVulnerability
```
**Expected:** CVE_2024_21413, CVE_2024_3400, SMBv1Enabled, UnpatchedSQLServer
(Vulnerabilities with severity "Critical" OR "High")

```
ProtectedAsset
```
**Expected:** PatientRecordServer, DomainController, ReceptionWorkstation, NurseStation01, AdminWorkstation, PatientDatabase, BillingDatabase, PatientPHI, EHRApplication, PharmacyServer
(Assets with `isProtectedBy some SecurityControl`)

```
VulnerableAsset
```
**Expected:** OutlookClient, ReceptionWorkstation, NurseStation01, AdminWorkstation, CoreFirewall, DomainController, EmployeeCredentials, PatientRecordServer, BillingServer, PatientDatabase
(Assets affected by unpatched vulnerabilities)

```
MitigatedThreat
```
**Expected:** LockBitRansomware, CobaltStrikeTrojan, LateralMovement, InitialPhishing
(Threats with `isMitigatedBy some SecurityControl`)

```
HIPAACompliantControl
```
**Expected:** PaloAltoFirewall, SplunkSIEM, CrowdStrikeEDR, VeeamBackup, BitLockerEncryption, TDEEncryption, WebApplicationFirewall, DuoMFA, SecurityAwarenessTraining
(Controls that `compliesWith HIPAA`)

---

### Property Value Queries

```
Asset and hasCriticality value "Mission-Critical"
```
Returns: PatientRecordServer, DomainController, CoreFirewall, CoreSwitch, PatientDatabase, PatientPHI, EHRApplication, EmployeeCredentials

```
Asset and hasCriticality value "High"
```
Returns: BillingServer, EmailServer, BackupServer, NurseStation01, AdminWorkstation, BillingDatabase, PharmacyServer, LaboratoryServer, RadiologyServer

```
Vulnerability and isPatched value false
```
Returns: CVE_2024_21413, WeakPasswordPolicy, SMBv1Enabled, UnpatchedSQLServer

```
Vulnerability and hasSeverityLevel value "Critical"
```
Returns: CVE_2024_21413, CVE_2024_3400

```
SecurityControl and compliesWith value HIPAA
```
Returns: PaloAltoFirewall, SplunkSIEM, CrowdStrikeEDR, VeeamBackup, BitLockerEncryption, TDEEncryption, WebApplicationFirewall, DuoMFA, SecurityAwarenessTraining

```
IncidentResponse and hasStatus value "Completed"
```
Returns: NetworkIsolation, EndpointQuarantine, MalwareRemoval, CredentialReset, SystemRestore

---

### Existential Restriction Queries

```
Asset and isAffectedBy some Vulnerability
```
Returns: Assets that have vulnerabilities affecting them

```
Asset and isProtectedBy some SecurityControl
```
Returns: Assets with security controls

```
Threat and exploits some Vulnerability
```
Returns: LockBitRansomware, InitialPhishing, CobaltStrikeTrojan, LateralMovement

```
SecurityControl and mitigates some Threat
```
Returns: PaloAltoFirewall, CrowdStrikeEDR, SnortIDS, VeeamBackup, SecurityAwarenessTraining

```
SecurityIncident and impactsAsset some Asset
```
Returns: MedCareRansomwareIncident, PHIDataBreach

```
IncidentResponse and handles value MedCareRansomwareIncident
```
Returns: All response actions for the ransomware incident

---

### Complex Queries

```
Asset and (isAffectedBy some (Vulnerability and isPatched value false))
```
Assets affected by unpatched vulnerabilities

```
Asset and (hasCriticality value "Mission-Critical") and (isAffectedBy some Vulnerability)
```
Mission-critical assets with vulnerabilities

```
SecurityControl and (protects some (Asset and hasCriticality value "Mission-Critical"))
```
Controls protecting mission-critical assets

```
Threat and (targets some Server)
```
Threats targeting servers

```
Vulnerability and (isExploitedBy some Ransomware)
```
Vulnerabilities exploited by ransomware (CVE_2024_21413, SMBv1Enabled)

---

### Incident Response Queries

```
Containment
```
Returns: NetworkIsolation, EndpointQuarantine

```
Eradication
```
Returns: MalwareRemoval, CredentialReset

```
Recovery
```
Returns: SystemRestore, PatchDeployment

```
IncidentResponse and performedBy value MedCareSOC
```
Returns: NetworkIsolation, EndpointQuarantine

```
IncidentResponse and performedBy value MedCareIRT
```
Returns: MalwareRemoval, CredentialReset, SystemRestore, PatchDeployment

---

### Compliance Queries

```
SecurityControl and compliesWith value NIST_CSF
```
Returns: PaloAltoFirewall, SnortIDS, DuoMFA, VulnerabilityScanner

```
SecurityControl and compliesWith value ISO27001
```
Returns: SplunkSIEM, VeeamBackup

```
SecurityControl and (compliesWith value HIPAA) and (compliesWith value NIST_CSF)
```
Returns: Controls compliant with both frameworks (PaloAltoFirewall, DuoMFA)

---

## 📋 Screenshot Checklist

- [ ] Screenshot 1: Class Hierarchy (Asset, Threat expanded)
- [ ] Screenshot 2: Object Properties (exploits property)
- [ ] Screenshot 3: Data Properties (hasCVSSScore)
- [ ] Screenshot 4: Individual (PatientRecordServer)
- [ ] Screenshot 5: OntoGraf class visualization
- [ ] Screenshot 6: HermiT consistency check
- [ ] Screenshot 7: DL Query - Asset instances
- [ ] Screenshot 8: DL Query - ActivelyExploitedVulnerability (inferred)
- [ ] Screenshot 9: OntoGraf attack chain
- [ ] Screenshot 10: Incident Response individual

---

## 💡 Tips

1. **Start the reasoner** before running DL queries (Reasoner → HermiT → Start reasoner)
2. **Check "Instances"** box in DL Query to see individuals
3. **Use high resolution** display for clear screenshots
4. **Crop screenshots** to show relevant area only
5. **Save as PNG** for best quality

---

## 📊 Ontology Statistics

| Component | Count |
|-----------|-------|
| Classes | 45 |
| Object Properties | 24 (12 pairs with inverses) |
| Data Properties | 10 (1 functional) |
| Individuals | 55+ |
| Disjoint Axioms | 5 groups |
| Defined Classes | 7 (reasoner inferred) |
| Property Chains | 1 (targets ⊑ exploits ∘ affects) |

---

## 🎯 Key Features to Demonstrate

1. **Class Hierarchy**: Asset → PhysicalAsset → NetworkAsset → Server/Workstation/NetworkDevice
2. **Inverse Properties**: exploits ↔ isExploitedBy, targets ↔ isTargetedBy
3. **Transitive Property**: partOf (PatientPHI partOf PatientDatabase partOf PatientRecordServer)
4. **Property Chain**: targets ⊑ exploits ∘ affects (infers threat-asset relationships)
5. **Functional Property**: hasIPAddress (each asset has exactly one IP)
6. **7 Defined Classes**: Reasoner automatically classifies:
   - ActivelyExploitedVulnerability
   - DetectedIncident
   - HighSeverityVulnerability
   - ProtectedAsset
   - VulnerableAsset
   - MitigatedThreat
   - HIPAACompliantControl
7. **Disjoint Classes**: Asset, Threat, Vulnerability, SecurityControl are mutually disjoint
8. **Real Scenario**: Complete ransomware attack with incident response
9. **Compliance Mapping**: Controls mapped to HIPAA, NIST CSF, ISO 27001
