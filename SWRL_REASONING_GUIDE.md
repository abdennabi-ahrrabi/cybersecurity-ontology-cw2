# SWRL Production Rules & Automated Reasoning Guide

## Overview
This cybersecurity ontology now includes **SWRL (Semantic Web Rule Language)** production rules for automated reasoning, SAT-based inference, and intelligent threat detection.

## Files
- **CybersecurityOntology_ENHANCED.owl** - Main ontology with classes, properties, and individuals
- **CybersecurityOntology_SWRL_Rules.swrl** - Production rules for automated reasoning

---

## Automated Reasoning Capabilities

### **1. Description Logic (DL) Reasoning**
The ontology uses **OWL 2 DL** (SROIQ Description Logic), a decidable fragment of First-Order Logic.

**Features:**
- ✅ Class subsumption inference
- ✅ Property chain reasoning
- ✅ Transitive closure (e.g., `dependsOn`, `contains`)
- ✅ Inverse property navigation
- ✅ Disjoint class consistency checking
- ✅ Cardinality constraint validation

### **2. SWRL Production Rules**
**10 production rules** for cybersecurity event detection and response.

---

## Production Rules Catalog

### **Rule 1: High-Risk Asset Detection**
```
IF Asset(?a) ∧ hasVulnerability(?a, ?v) ∧ hasCVSS(?v, ?score) ∧ ?score > 7.0
THEN HighRiskAsset(?a)
```
**Purpose**: Automatically flags assets with CVSS scores above 7.0 as high-risk

---

### **Rule 2: Critical Asset Protection**
```
IF Asset(?a) ∧ hasAssetValue(?a, "Critical")
THEN RequiresImmediateProtection(?a)
```
**Purpose**: Identifies critical assets requiring immediate protection measures

---

### **Rule 3: Malware Incident Response**
```
IF SecurityEvent(?e) ∧ hasSeverity(?e, "Critical") ∧
   causedBy(?e, ?t) ∧ Malware(?t)
THEN IncidentResponseRequired(?e)
```
**Purpose**: Triggers incident response for critical malware events

---

### **Rule 4: Coordinated Attack Detection**
```
IF Threat(?t1) ∧ Threat(?t2) ∧
   initiatedBy(?t1, ?actor) ∧ initiatedBy(?t2, ?actor) ∧
   targets(?t1, ?a1) ∧ targets(?t2, ?a2) ∧
   communicatesWith(?a1, ?a2)
THEN CoordinatedAttack(?t1), CoordinatedAttack(?t2)
```
**Purpose**: Detects coordinated attacks from the same threat actor

---

### **Rule 5: Exploit Available Alert**
```
IF Vulnerability(?v) ∧ hasExploitAvailable(?v, true) ∧
   affects(?v, ?a) ∧ hasAssetValue(?a, "Critical")
THEN UrgentSecurityAlert(?v)
```
**Purpose**: Generates urgent alerts for exploitable vulnerabilities on critical assets

---

### **Rule 6: Zero-Day Threat Classification**
```
IF ZeroDayVulnerability(?v) ∧ Threat(?t) ∧ exploits(?t, ?v)
THEN ZeroDayThreat(?t)
```
**Purpose**: Classifies threats exploiting zero-day vulnerabilities

---

### **Rule 7: Ransomware Data Target Detection**
```
IF Ransomware(?r) ∧ targets(?r, ?a) ∧
   contains(?a, ?d) ∧ PersonalData(?d)
THEN DataBreachRisk(?a)
```
**Purpose**: Identifies data breach risks from ransomware

---

### **Rule 8: Unpatched Critical Vulnerability Alert**
```
IF Vulnerability(?v) ∧ hasSeverity(?v, "Critical") ∧
   affects(?v, ?a) ∧ locatedIn(?a, ?env) ∧
   ProductionEnvironment(?env)
THEN RequiresUrgentPatching(?v)
```
**Purpose**: Flags critical unpatched vulnerabilities in production

---

### **Rule 9: Advanced Persistent Threat (APT) Detection**
```
IF ThreatActor(?actor) ∧ Threat(?t1) ∧ Threat(?t2) ∧
   initiatedBy(?t1, ?actor) ∧ initiatedBy(?t2, ?actor) ∧
   hasThreatLevel(?t1, "High")
THEN AdvancedPersistentThreat(?actor)
```
**Purpose**: Detects APTs based on repeated high-level attacks

---

### **Rule 10: Insider Threat Risk Assessment**
```
IF User(?u) ∧ hasAccess(?u, ?a) ∧ hasAssetValue(?a, "Critical") ∧
   SecurityEvent(?e) ∧ performs(?u, ?e) ∧ hasSeverity(?e, "High")
THEN InsiderThreatRisk(?u)
```
**Purpose**: Assesses insider threat risk

---

## How to Use with Reasoners

### **Option 1: Protégé (Desktop)**

1. **Load Ontology:**
   - Open Protégé 5.6+
   - File → Open → Select `CybersecurityOntology_ENHANCED.owl`

2. **Import SWRL Rules:**
   - Go to **Rules** tab
   - Import → Select `CybersecurityOntology_SWRL_Rules.swrl`
   - Or use: File → Import → SWRL Rules

3. **Select Reasoner:**
   - Reasoner → Select **Pellet**, **HermiT**, or **Rac erPro**
   - Click **Start Reasoner**

4. **View Inferences:**
   - Go to **Individuals** tab
   - Select "Inferred" view
   - See new classifications (e.g., `HighRiskAsset`, `IncidentResponseRequired`)

---

### **Option 2: OWL API (Java)**

```java
import org.semanticweb.owlapi.apibinding.OWLManager;
import org.semanticweb.owlapi.model.*;
import org.semanticweb.owlapi.reasoner.*;
import org.semanticweb.HermiT.ReasonerFactory;

// Load ontology
OWLOntologyManager manager = OWLManager.createOWLOntologyManager();
OWLOntology ontology = manager.loadOntologyFromOntologyDocument(
    new File("CybersecurityOntology_ENHANCED.owl")
);

// Create reasoner
OWLReasonerFactory reasonerFactory = new ReasonerFactory();
OWLReasoner reasoner = reasonerFactory.createReasoner(ontology);

// Check consistency
boolean consistent = reasoner.isConsistent();
System.out.println("Ontology consistent: " + consistent);

// Get inferred instances
OWLClass highRiskAsset = dataFactory.getOWLClass(IRI.create(
    "http://www.semanticweb.org/ontologies/cybersecurity#HighRiskAsset"
));
NodeSet<OWLNamedIndividual> instances = reasoner.getInstances(highRiskAsset, false);
```

---

### **Option 3: Apache Jena (Java)**

```java
import org.apache.jena.rdf.model.*;
import org.apache.jena.reasoner.*;
import org.apache.jena.reasoner.rulesys.GenericRuleReasoner;

// Load model
Model model = ModelFactory.createDefaultModel();
model.read("CybersecurityOntology_ENHANCED.owl");

// Load SWRL rules
Model rules = ModelFactory.createDefaultModel();
rules.read("CybersecurityOntology_SWRL_Rules.swrl");

// Create reasoner
Reasoner reasoner = ReasonerRegistry.getOWLReasoner();
reasoner = reasoner.bindSchema(rules);

// Create inference model
InfModel infModel = ModelFactory.createInfModel(reasoner, model);

// Query inferences
String queryString =
    "PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#> " +
    "SELECT ?asset WHERE { ?asset a :HighRiskAsset }";
```

---

### **Option 4: Python with Owlready2**

```python
from owlready2 import *

# Load ontology
onto = get_ontology("file://CybersecurityOntology_ENHANCED.owl").load()

# Run reasoner
with onto:
    sync_reasoner_pellet(infer_property_values=True,
                        infer_data_property_values=True)

# Query inferred instances
high_risk_assets = onto.HighRiskAsset.instances()
for asset in high_risk_assets:
    print(f"High-risk asset: {asset.name}")

# Check SWRL rules fired
incident_responses = onto.IncidentResponseRequired.instances()
for event in incident_responses:
    print(f"Incident response required for: {event.name}")
```

---

## SAT-Based Reasoning

### **HermiT Reasoner (SAT-based)**
HermiT uses a **hypertableau calculus** that translates OWL to SAT problems.

```bash
# Command-line usage
java -jar hermit-cli.jar -c CybersecurityOntology_ENHANCED.owl
```

**Reasoning Tasks:**
- ✅ Consistency checking
- ✅ Class satisfiability
- ✅ Instance classification
- ✅ SWRL rule evaluation

---

## Querying with SPARQL

```sparql
PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

# Find all high-risk assets
SELECT ?asset ?vuln ?cvss
WHERE {
  ?asset rdf:type :HighRiskAsset .
  ?asset :hasVulnerability ?vuln .
  ?vuln :hasCVSS ?cvss .
  FILTER (?cvss > 7.0)
}

# Find coordinated attacks
SELECT ?attack1 ?attack2 ?actor
WHERE {
  ?attack1 rdf:type :CoordinatedAttack .
  ?attack2 rdf:type :CoordinatedAttack .
  ?attack1 :initiatedBy ?actor .
  ?attack2 :initiatedBy ?actor .
  FILTER (?attack1 != ?attack2)
}

# Detect insider threats
SELECT ?user ?asset ?event
WHERE {
  ?user rdf:type :InsiderThreatRisk .
  ?user :hasAccess ?asset .
  ?asset :hasAssetValue "Critical" .
  ?user :performs ?event .
  ?event :hasSeverity "High" .
}
```

---

## Performance Optimization

### **1. Reasoner Selection**
| Reasoner | Speed | Completeness | SWRL Support |
|----------|-------|--------------|--------------|
| HermiT   | Medium| Full OWL 2   | Yes          |
| Pellet   | Fast  | OWL 2 DL     | Yes          |
| FaCT++   | Fast  | OWL 2 DL     | Limited      |
| ELK      | Very Fast | OWL EL   | No           |

**Recommendation**: Use **Pellet** for SWRL + performance balance

### **2. Optimization Tips**
- Use **incremental reasoning** for large knowledge bases
- Enable **rule caching** for repeated queries
- Partition ontology by **security domains** (network, application, data)
- Use **materialization** for static inferences

---

## Use Cases

### **1. Threat Intelligence Platform**
- Automatic threat classification
- Attack pattern detection
- Risk scoring

### **2. Security Information & Event Management (SIEM)**
- Event correlation
- Incident prioritization
- Automated response triggers

### **3. Vulnerability Management**
- Critical asset identification
- Patch prioritization
- Exploit risk assessment

### **4. Compliance Monitoring**
- GDPR/HIPAA violation detection
- Policy enforcement
- Audit trail generation

### **5. Insider Threat Detection**
- Behavioral anomaly detection
- Access pattern analysis
- Risk scoring

---

## Example Workflow

```
1. Load ontology → CybersecurityOntology_ENHANCED.owl
2. Import SWRL rules → CybersecurityOntology_SWRL_Rules.swrl
3. Add instances → New threats, vulnerabilities, assets
4. Run reasoner → Pellet/HermiT
5. Query results → SPARQL/OWL API
6. Generate alerts → Based on inferred classes
7. Trigger response → Automated workflows
```

---

## Further Reading

- **OWL 2 Specification**: https://www.w3.org/TR/owl2-overview/
- **SWRL Specification**: https://www.w3.org/Submission/SWRL/
- **Protégé Tutorial**: https://protegewiki.stanford.edu/wiki/SWRL
- **HermiT Reasoner**: http://www.hermit-reasoner.com/
- **Pellet Reasoner**: https://github.com/stardog-union/pellet

---

## Support
For questions or issues with the ontology/rules, check the documentation or consult the OWL/SWRL community forums.
