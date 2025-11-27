# Competency Questions for Cybersecurity Incident Response Ontology

## Overview
This document lists the competency questions (CQs) that the ontology is designed to answer. These questions were used to guide the ontology design and can be used to validate that the ontology meets its intended purpose.

---

## CQ1: Asset Identification and Classification

**CQ1.1:** What are all the mission-critical assets in the organization?
```sparql
SELECT ?asset ?name WHERE {
  ?asset rdf:type/rdfs:subClassOf* :Asset .
  ?asset :hasCriticality "Mission-Critical" .
  ?asset :hasName ?name .
}
```
**Expected Result:** PatientRecordServer, DomainController, CoreFirewall, CoreSwitch, PatientDatabase, PatientPHI, EHRApplication

---

**CQ1.2:** Which assets contain sensitive patient data (PHI)?
```sparql
SELECT ?asset ?name WHERE {
  ?asset :hasPart* :PatientPHI .
  ?asset :hasName ?name .
}
```
**Expected Result:** PatientDatabase, PatientRecordServer (via transitive partOf)

---

**CQ1.3:** What is the IP address of each network asset?
```sparql
SELECT ?asset ?name ?ip WHERE {
  ?asset rdf:type/rdfs:subClassOf* :NetworkAsset .
  ?asset :hasName ?name .
  ?asset :hasIPAddress ?ip .
}
```

---

## CQ2: Vulnerability Assessment

**CQ2.1:** What are all critical vulnerabilities (CVSS >= 9.0)?
```sparql
SELECT ?vuln ?name ?cvss WHERE {
  ?vuln rdf:type :Vulnerability .
  ?vuln :hasName ?name .
  ?vuln :hasCVSSScore ?cvss .
  FILTER (?cvss >= 9.0)
}
```
**Expected Result:** CVE_2024_21413 (9.8), CVE_2024_3400 (10.0)

---

**CQ2.2:** Which vulnerabilities are currently unpatched?
```sparql
SELECT ?vuln ?name ?cvss WHERE {
  ?vuln rdf:type/rdfs:subClassOf* :Vulnerability .
  ?vuln :hasName ?name .
  ?vuln :hasCVSSScore ?cvss .
  ?vuln :isPatched false .
}
```
**Expected Result:** CVE_2024_21413, WeakPasswordPolicy, SMBv1Enabled, UnpatchedSQLServer

---

**CQ2.3:** Which assets are affected by unpatched critical vulnerabilities?
```sparql
SELECT DISTINCT ?asset ?assetName ?vuln ?vulnName ?cvss WHERE {
  ?vuln rdf:type/rdfs:subClassOf* :Vulnerability .
  ?vuln :hasCVSSScore ?cvss .
  ?vuln :isPatched false .
  ?vuln :affects ?asset .
  ?vuln :hasName ?vulnName .
  ?asset :hasName ?assetName .
  FILTER (?cvss >= 9.0)
}
```
**Expected Result:** ReceptionWorkstation, NurseStation01, AdminWorkstation affected by CVE_2024_21413

---

## CQ3: Threat Analysis

**CQ3.1:** What threats are currently targeting our assets?
```sparql
SELECT ?threat ?name ?asset ?assetName WHERE {
  ?threat rdf:type/rdfs:subClassOf* :Threat .
  ?threat :hasName ?name .
  ?threat :targets ?asset .
  ?asset :hasName ?assetName .
}
```

---

**CQ3.2:** Which vulnerabilities does each threat exploit?
```sparql
SELECT ?threat ?threatName ?vuln ?vulnName WHERE {
  ?threat rdf:type/rdfs:subClassOf* :Threat .
  ?threat :hasName ?threatName .
  ?threat :exploits ?vuln .
  ?vuln :hasName ?vulnName .
}
```

---

**CQ3.3:** What is the complete attack chain for the ransomware incident?
```sparql
SELECT ?threat ?type ?exploits ?targets WHERE {
  ?threat rdf:type ?type .
  ?type rdfs:subClassOf* :Threat .
  OPTIONAL { ?threat :exploits ?exploits }
  OPTIONAL { ?threat :targets ?targets }
  FILTER (?threat IN (:InitialPhishing, :CobaltStrikeTrojan, :LateralMovement, :LockBitRansomware))
}
```

---

## CQ4: Security Controls Assessment

**CQ4.1:** What security controls protect each mission-critical asset?
```sparql
SELECT ?asset ?assetName ?control ?controlName WHERE {
  ?asset :hasCriticality "Mission-Critical" .
  ?asset :hasName ?assetName .
  ?asset :isProtectedBy ?control .
  ?control :hasName ?controlName .
}
```

---

**CQ4.2:** Which security controls comply with HIPAA?
```sparql
SELECT ?control ?name WHERE {
  ?control rdf:type/rdfs:subClassOf* :SecurityControl .
  ?control :hasName ?name .
  ?control :compliesWith :HIPAA .
}
```
**Expected Result:** PaloAltoFirewall, SplunkSIEM, CrowdStrikeEDR, VeeamBackup, BitLockerEncryption, TDEEncryption, DuoMFA, SecurityAwarenessTraining

---

**CQ4.3:** Are there any critical assets without protective controls?
```sparql
SELECT ?asset ?name WHERE {
  ?asset :hasCriticality "Mission-Critical" .
  ?asset :hasName ?name .
  FILTER NOT EXISTS { ?asset :isProtectedBy ?control }
}
```

---

**CQ4.4:** Which controls can mitigate the LockBit ransomware threat?
```sparql
SELECT ?control ?name WHERE {
  ?control :mitigates :LockBitRansomware .
  ?control :hasName ?name .
}
```
**Expected Result:** CrowdStrikeEDR, VeeamBackup

---

## CQ5: Incident Response

**CQ5.1:** What incidents are currently active (not resolved)?
```sparql
SELECT ?incident ?name ?severity ?status WHERE {
  ?incident rdf:type/rdfs:subClassOf* :SecurityIncident .
  ?incident :hasName ?name .
  ?incident :hasSeverityLevel ?severity .
  ?incident :hasStatus ?status .
  FILTER (?status != "Resolved")
}
```

---

**CQ5.2:** What assets were impacted by the ransomware incident?
```sparql
SELECT ?asset ?name ?criticality WHERE {
  :MedCareRansomwareIncident :impactsAsset ?asset .
  ?asset :hasName ?name .
  OPTIONAL { ?asset :hasCriticality ?criticality }
}
```
**Expected Result:** PatientRecordServer, BillingServer, PatientDatabase, PatientPHI, ReceptionWorkstation

---

**CQ5.3:** What response actions were taken and by whom?
```sparql
SELECT ?response ?name ?status ?team ?teamName ?timestamp WHERE {
  ?response rdf:type/rdfs:subClassOf* :IncidentResponse .
  ?response :hasName ?name .
  ?response :hasStatus ?status .
  ?response :performedBy ?team .
  ?team :hasName ?teamName .
  OPTIONAL { ?response :hasTimestamp ?timestamp }
}
ORDER BY ?timestamp
```

---

**CQ5.4:** Which controls detected the incident?
```sparql
SELECT ?control ?name WHERE {
  :MedCareRansomwareIncident :detectedBy ?control .
  ?control :hasName ?name .
}
```
**Expected Result:** SplunkSIEM, CrowdStrikeEDR

---

## CQ6: Risk Assessment

**CQ6.1:** What is the risk profile of assets with unpatched vulnerabilities?
```sparql
SELECT ?asset ?assetName ?criticality ?vuln ?cvss WHERE {
  ?vuln :affects ?asset .
  ?vuln :isPatched false .
  ?vuln :hasCVSSScore ?cvss .
  ?asset :hasName ?assetName .
  ?asset :hasCriticality ?criticality .
}
ORDER BY DESC(?cvss)
```

---

**CQ6.2:** Which threats pose the highest risk (exploit critical vulns targeting critical assets)?
```sparql
SELECT ?threat ?threatName ?vuln ?vulnCVSS ?asset ?assetCrit WHERE {
  ?threat :exploits ?vuln .
  ?threat :targets ?asset .
  ?threat :hasName ?threatName .
  ?vuln :hasCVSSScore ?vulnCVSS .
  ?asset :hasCriticality ?assetCrit .
  FILTER (?vulnCVSS >= 9.0 && ?assetCrit = "Mission-Critical")
}
```

---

## CQ7: Compliance

**CQ7.1:** What percentage of controls comply with each framework?
```sparql
SELECT ?framework (COUNT(?control) AS ?count) WHERE {
  ?control :compliesWith ?framework .
}
GROUP BY ?framework
```

---

**CQ7.2:** Are all assets containing PHI protected by HIPAA-compliant controls?
```sparql
SELECT ?asset ?assetName WHERE {
  ?asset :hasPart* ?data .
  ?data rdf:type :SensitiveData .
  ?asset :hasName ?assetName .
  FILTER NOT EXISTS {
    ?asset :isProtectedBy ?control .
    ?control :compliesWith :HIPAA .
  }
}
```

---

## CQ8: Reasoner-Inferred Knowledge

**CQ8.1:** Which vulnerabilities are classified as CriticalVulnerability by the reasoner?
```sparql
SELECT ?vuln ?name ?cvss WHERE {
  ?vuln rdf:type :CriticalVulnerability .
  ?vuln :hasName ?name .
  ?vuln :hasCVSSScore ?cvss .
}
```
**Expected (after reasoning):** CVE_2024_21413 (9.8), CVE_2024_3400 (10.0)

---

**CQ8.2:** Which incidents are classified as CriticalIncident by the reasoner?
```sparql
SELECT ?incident ?name WHERE {
  ?incident rdf:type :CriticalIncident .
  ?incident :hasName ?name .
}
```
**Expected (after reasoning):** MedCareRansomwareIncident, PHIDataBreach

---

## Validation Notes

These competency questions should be tested in Protege using:
1. **DL Query Tab** - For simple class expressions
2. **SPARQL Query Tab** - For the queries above
3. **Reasoner** - Run HermiT or Pellet before querying to see inferred facts

### Expected Behavior:
- All queries should return results
- Defined classes (CriticalVulnerability, CriticalIncident) should have inferred members
- Transitive property (partOf/hasPart) should propagate correctly
- Inverse properties should work bidirectionally
