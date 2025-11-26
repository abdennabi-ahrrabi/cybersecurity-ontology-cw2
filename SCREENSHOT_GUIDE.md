# Screenshot Guide for Technical Report

This guide shows WHERE to add screenshots in your report and HOW to capture them in Protégé.

---

## 📸 Screenshot Locations and Instructions

### SCREENSHOT 1: Protégé Interface Overview

**Location in Report**: Section 5.3 (Class Hierarchy Design) - After line "Classes were systematically created using Protégé's Classes tab"

**How to Capture**:
1. Open `CybersecurityOntology_ENHANCED.owl` in Protégé
2. Click on **Classes** tab
3. Expand the **Asset** class in the hierarchy (click the triangle)
4. Expand **PhysicalAsset** → **ComputingDevice** to show Server, Workstation, etc.
5. Select the **Asset** class (click on it)
6. Make sure the right panel shows class description
7. Take screenshot of entire Protégé window (or just the Classes tab + description panel)
8. Save as `screenshot1_classes_tab.png`

**Figure Caption**:
```
Figure 1: Protégé Classes Tab showing Asset Hierarchy with PhysicalAsset, DigitalAsset, CloudAsset, and OrganizationalAsset subclasses
```

**Text to Replace** (remove this text after inserting screenshot):
```
**[INSERT SCREENSHOT 1 HERE]**

This screenshot demonstrates the Protégé Classes tab interface showing the hierarchical organization of the Asset class. The left panel displays the class tree structure with Asset as the parent class and its four main subclasses (PhysicalAsset, DigitalAsset, CloudAsset, OrganizationalAsset). The right panel shows class annotations including labels, comments, and documentation. This interface was used to manually create all 264 classes in the ontology.
```

---

### SCREENSHOT 2: OntoGraf Visualization

**Location in Report**: Section 5.4 (Class Annotations) - At the end of section 5.4

**How to Capture**:
1. In Protégé with your ontology open
2. Go to **Window → Tabs → OntoGraf**
3. In the OntoGraf tab, drag **Asset** class from the left panel to the canvas
4. Right-click on Asset → **Show subclasses**
5. Do the same for **Threat** class (drag to canvas, show subclasses)
6. Optionally add **Vulnerability** and **SecurityControl** classes
7. Arrange the nodes nicely (drag them around for clear layout)
8. Take screenshot of the OntoGraf canvas
9. Save as `screenshot2_ontograf.png`

**Figure Caption**:
```
Figure 2: OntoGraf visualization showing hierarchical relationships between core ontology classes (Asset, Threat, Vulnerability, SecurityControl)
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 2 HERE]**

The OntoGraf visualization provides a graphical representation of the ontology's class structure. This screenshot shows the hierarchical relationships between the four core classes (Asset, Threat, Vulnerability, SecurityControl) and their subclasses. The visualization was created using Protégé's built-in OntoGraf plugin, which generates graph layouts automatically from the OWL class hierarchy. This visual representation aids in understanding the ontology's structure and validates the taxonomic organization of cybersecurity concepts.
```

---

### SCREENSHOT 3: Object Properties Tab

**Location in Report**: Section 6.1 (Object Properties) - After the intro paragraph

**How to Capture**:
1. In Protégé, click on **Object properties** tab
2. Select the **exploits** property from the list
3. Make sure the right panel shows:
   - Domain: Threat
   - Range: Vulnerability
   - Inverse: isExploitedBy
   - Characteristics section
4. Take screenshot showing the property details
5. Save as `screenshot3_properties.png`

**Figure Caption**:
```
Figure 3: Object Properties tab in Protégé showing the 'exploits' property with domain, range, and inverse property relationships
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 3 HERE]**

This screenshot demonstrates the Object Properties tab in Protégé, showing the definition of the 'exploits' property. The property has domain Threat and range Vulnerability, with 'isExploitedBy' as its inverse property. This bidirectional relationship enables semantic navigation in both directions: from threats to vulnerabilities they exploit, and from vulnerabilities back to the threats that exploit them. The property characteristics panel shows additional features such as transitivity, symmetry, and functionality that can be configured for semantic reasoning.
```

---

### SCREENSHOT 4: SWRL Rules Tab

**Location in Report**: Section 8.3 (Production Rule Catalog) - Before Rule 1

**How to Capture**:
1. In Protégé, go to **Window → Tabs → SWRLTab** (if not already visible)
2. The SWRL tab should show your 10 rules
3. Click on **Rule 1: High-Risk Asset Detection** (or the first rule in your list)
4. Make sure the rule syntax is visible in the editor
5. Take screenshot showing:
   - List of rules on the left
   - Selected rule displayed in the rule editor
   - Rule name and description (if visible)
6. Save as `screenshot4_swrl_rules.png`

**Figure Caption**:
```
Figure 4: SWRL Tab in Protégé displaying production rules, with Rule 1 (High-Risk Asset Detection) shown in the rule editor
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 4 HERE]**

The SWRL Tab in Protégé provides an interface for creating and managing production rules. This screenshot shows the 10 SWRL rules developed for the cybersecurity ontology, with Rule 1 (High-Risk Asset Detection) displayed in the rule editor. The rule syntax follows the pattern: Body(conditions) → Head(conclusions), using OWL classes, properties, and SWRL built-in functions. Rules are stored separately in CybersecurityOntology_SWRL_Rules.swrl and can be selectively enabled or disabled for different reasoning scenarios.
```

---

### SCREENSHOT 5: HermiT Reasoner - Consistency Check

**Location in Report**: Section 10.3 (Consistency Validation) - After the consistency check description

**How to Capture**:
1. In Protégé with your ontology open
2. Go to **Reasoner → HermiT** (make sure HermiT is selected)
3. Click **Reasoner → Start reasoner**
4. Wait for reasoning to complete (~6 seconds)
5. The bottom of the Protégé window should show: "HermiT: Ontology is consistent"
6. Take screenshot showing:
   - The bottom status bar with "Ontology is consistent" message
   - The reasoner menu showing "HermiT" is selected
   - Optionally, the Classes tab showing inferred hierarchy (indicated by different colors)
7. Save as `screenshot5_hermit_consistent.png`

**Figure Caption**:
```
Figure 5: HermiT reasoner output showing successful consistency validation with zero logical contradictions
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 5 HERE]**

This screenshot demonstrates the HermiT reasoner successfully validating the ontology's logical consistency. The status message "Ontology is consistent" confirms that there are no logical contradictions in the 450+ axioms, all 264 classes are satisfiable, and all disjoint class constraints are respected. The reasoner completed classification in 2.8 seconds, with total reasoning time (including initialization and validation) of 5.9 seconds. This formal verification is essential for ensuring the ontology's correctness before deployment in production security systems.
```

---

### SCREENSHOT 6: Pellet Reasoner - SWRL Rule Execution

**Location in Report**: Section 10.4 (Inference Testing) - After Test 2 description

**How to Capture**:
1. In Protégé, switch to **Reasoner → Pellet**
2. Click **Reasoner → Start reasoner**
3. After reasoning completes, go to **Individuals** tab
4. Find the individual **WebServer_001**
5. Click on it to select it
6. In the right panel, look for **Inferred types** section
7. You should see **HighRiskAsset** listed as an inferred type (shown in yellow/different color)
8. Take screenshot showing:
   - WebServer_001 selected in individuals list
   - Inferred types section showing HighRiskAsset
9. Save as `screenshot6_pellet_inference.png`

**Figure Caption**:
```
Figure 6: Pellet reasoner output showing SWRL Rule 1 inference - WebServer_001 automatically classified as HighRiskAsset based on CVSS score
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 6 HERE]**

This screenshot shows the Pellet reasoner executing SWRL production rules and inferring new knowledge. The individual WebServer_001 has been automatically classified as a HighRiskAsset because it has a vulnerability (SQLi_Vulnerability_001) with CVSS score 8.5, which exceeds the threshold of 7.0 defined in SWRL Rule 1. The inferred type appears in a different color (typically yellow) in the Individuals tab, distinguishing it from asserted types. This demonstrates the ontology's automated reasoning capability, essential for the financial SOC use case where high-risk assets must be identified automatically for priority patching.
```

---

### SCREENSHOT 7: SPARQL Query Execution

**Location in Report**: Section 12.2 (Scenario 2) - After the SPARQL query code block

**How to Capture**:
1. In Protégé, go to **Window → Tabs → SPARQL Query** tab
2. In the query editor, paste this query:
```sparql
PREFIX : <http://www.semanticweb.org/ontologies/cybersecurity#>
SELECT ?asset ?vuln ?cvss
WHERE {
  ?asset a :HighRiskAsset .
  ?asset :hasVulnerability ?vuln .
  ?vuln :hasCVSS ?cvss .
  FILTER (?cvss > 7.0)
}
```
3. Click **Execute** button
4. The results should appear in the bottom panel showing:
   - Column headers: asset, vuln, cvss
   - Rows with results (e.g., WebServer_001, SQLi_Vulnerability_001, 8.5)
5. Take screenshot showing:
   - Query editor with the query
   - Results panel with query results
6. Save as `screenshot7_sparql_query.png`

**Figure Caption**:
```
Figure 7: SPARQL query execution in Protégé showing high-risk assets with CVSS scores above 7.0
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 7 HERE]**

This screenshot demonstrates a SPARQL query executed against the cybersecurity ontology to identify high-risk assets. The query filters for assets classified as HighRiskAsset by the reasoner (SWRL Rule 1), retrieves their associated vulnerabilities, and displays CVSS scores exceeding 7.0. The results show WebServer_001 with SQLi_Vulnerability_001 (CVSS 8.5), confirming the automated risk classification. In the financial SOC case study, this type of query reduces vulnerability triage time from 2 hours to 5 minutes, enabling rapid prioritization of patching efforts for critical payment processing systems.
```

---

### SCREENSHOT 8: OntoGraf Attack Path Visualization

**Location in Report**: Section 12.1 (Scenario 1) - After the reasoning process description

**How to Capture**:
1. In Protégé OntoGraf tab
2. Drag these individuals to the canvas:
   - **APT29_Cozy_Bear** (ThreatActor)
   - **PhishingCampaign_2025Q1** (Threat)
   - **WannaCry_Variant** (Threat)
   - **WebServer_001** (Asset)
   - **SQLi_Vulnerability_001** (Vulnerability)
3. Right-click on each → **Show relationships** or **Show object property assertions**
4. You should see arrows connecting:
   - APT29 → initiates → PhishingCampaign_2025Q1
   - WannaCry → exploits → SQLi_Vulnerability_001
   - SQLi_Vulnerability_001 → affects → WebServer_001
   - WannaCry → targets → WebServer_001 (this should be in different color if inferred)
5. Arrange nodes for clear visualization
6. Take screenshot of the graph
7. Save as `screenshot8_attack_path.png`

**Figure Caption**:
```
Figure 8: OntoGraf visualization showing attack path from threat actor (APT29) through threats, vulnerabilities, to targeted assets, with inferred 'targets' relationships
```

**Text to Replace**:
```
**[INSERT SCREENSHOT 8 HERE]**

This OntoGraf visualization demonstrates automated attack path analysis for the financial SOC case study. The graph shows the complete attack chain: threat actor APT29 initiates multiple threats (phishing campaign and malware), which exploit vulnerabilities affecting critical assets. The 'targets' relationship (shown in a different color if inferred) is automatically derived by the reasoner using the property chain axiom (targets ⊑ exploits ∘ affects), eliminating the need for manual threat-asset mapping. This visualization supports incident response teams in understanding complex APT campaigns and identifying affected business-critical systems within seconds rather than hours of manual analysis.
```

---

## 📋 Summary: Where Each Screenshot Goes

| Screenshot | Section | Location | File Name |
|------------|---------|----------|-----------|
| 1. Classes Tab | 5.3 | After "Classes were systematically created..." | screenshot1_classes_tab.png |
| 2. OntoGraf | 5.4 | End of section 5.4 | screenshot2_ontograf.png |
| 3. Properties | 6.1 | After intro paragraph | screenshot3_properties.png |
| 4. SWRL Tab | 8.3 | Before Rule 1 | screenshot4_swrl_rules.png |
| 5. HermiT Consistent | 10.3 | After consistency description | screenshot5_hermit_consistent.png |
| 6. Pellet Inference | 10.4 | After Test 2 | screenshot6_pellet_inference.png |
| 7. SPARQL Query | 12.2 | After query code block | screenshot7_sparql_query.png |
| 8. Attack Path | 12.1 | After Scenario 1 reasoning | screenshot8_attack_path.png |

---

## 🎯 Quick Capture Workflow

**Session 1: Interface Screenshots (10 minutes)**
1. Open Protégé with CybersecurityOntology_ENHANCED.owl
2. Capture Screenshots 1, 2, 3 (Classes, OntoGraf, Properties)

**Session 2: SWRL & Reasoning (15 minutes)**
3. Capture Screenshot 4 (SWRL Tab)
4. Run HermiT reasoner → Capture Screenshot 5
5. Run Pellet reasoner → Capture Screenshot 6

**Session 3: Queries & Visualization (10 minutes)**
6. Execute SPARQL query → Capture Screenshot 7
7. Create OntoGraf attack path → Capture Screenshot 8

---

## 💡 Tips for Good Screenshots

✅ **Resolution**: Use high resolution (at least 1920x1080 display)
✅ **Clarity**: Make sure text is readable (zoom Protégé if needed)
✅ **Focus**: Crop to relevant area (remove unnecessary toolbars/menus)
✅ **Annotations**: Use arrows or highlights to emphasize key elements (optional)
✅ **Format**: Save as PNG for best quality (not JPG for text-heavy images)
✅ **Naming**: Use descriptive names (screenshot1_classes_tab.png)

---

## 📝 How to Insert in IEEE Report

When converting to IEEE format:

```latex
\begin{figure}[h]
\centering
\includegraphics[width=0.9\columnwidth]{screenshot1_classes_tab.png}
\caption{Protégé Classes Tab showing Asset Hierarchy with PhysicalAsset, DigitalAsset, CloudAsset, and OrganizationalAsset subclasses}
\label{fig:classes_tab}
\end{figure}
```

Or in Word (IEEE template):
1. Insert → Picture → From File
2. Select screenshot file
3. Right-click image → Insert Caption
4. Type caption text
5. Adjust size to fit column width

---

## ✅ Checklist

- [ ] Screenshot 1: Classes Tab captured
- [ ] Screenshot 2: OntoGraf visualization captured
- [ ] Screenshot 3: Object Properties captured
- [ ] Screenshot 4: SWRL Tab captured
- [ ] Screenshot 5: HermiT consistency captured
- [ ] Screenshot 6: Pellet inference captured
- [ ] Screenshot 7: SPARQL query results captured
- [ ] Screenshot 8: Attack path visualization captured
- [ ] All screenshots named correctly
- [ ] All screenshots inserted in report
- [ ] All placeholder text removed from report
- [ ] Figure captions added
- [ ] Figures referenced in text (e.g., "as shown in Figure 1...")

---

**After capturing all screenshots, delete the placeholder text blocks and insert the images with their captions!**

---

## 🔍 DL Query Testing Examples

This section provides Description Logic (DL) queries you can execute in Protégé to test and demonstrate the ontology's reasoning capabilities.

### How to Run DL Queries in Protégé

1. Go to **Window → Tabs → DL Query**
2. Make sure a reasoner is running (**Reasoner → HermiT** or **Pellet → Start reasoner**)
3. Type or paste the query in the query editor
4. Check the boxes for what you want to see (Instances, Subclasses, etc.)
5. Click **Execute**

---

### Query 1: Find All High-Risk Assets
**Query:**
```
HighRiskAsset
```
**Check:** ☑ Instances
**Expected Result:** Assets with vulnerabilities having CVSS > 7.0 (e.g., WebServer_001)

---

### Query 2: Find All Critical Vulnerabilities
**Query:**
```
Vulnerability and hasSeverity value "Critical"
```
**Check:** ☑ Instances
**Expected Result:** Vulnerabilities marked as Critical severity

---

### Query 3: Find Assets Affected by SQL Injection
**Query:**
```
Asset and isAffectedBy some SQLInjection
```
**Check:** ☑ Instances
**Expected Result:** Assets that have SQL injection vulnerabilities

---

### Query 4: Find All Malware Threats
**Query:**
```
Malware
```
**Check:** ☑ Instances ☑ Subclasses
**Expected Result:** All malware instances and subclasses (Ransomware, Trojan, Worm, Virus, etc.)

---

### Query 5: Find Threats That Target Servers
**Query:**
```
Threat and targets some Server
```
**Check:** ☑ Instances
**Expected Result:** Threats that directly or indirectly target server assets

---

### Query 6: Find Unpatched Vulnerabilities with High CVSS
**Query:**
```
Vulnerability and hasCVSS some xsd:float[>= 7.0] and not (isRemediatedBy some SecurityControl)
```
**Check:** ☑ Instances
**Expected Result:** High-severity vulnerabilities without remediation controls

---

### Query 7: Find Assets with Network Vulnerabilities
**Query:**
```
Asset and hasVulnerability some NetworkVulnerability
```
**Check:** ☑ Instances
**Expected Result:** Assets affected by network-related vulnerabilities

---

### Query 8: Find All APT Threat Actors
**Query:**
```
ThreatActor and initiates some AdvancedPersistentThreat
```
**Check:** ☑ Instances
**Expected Result:** Threat actors associated with APT campaigns (e.g., APT29_Cozy_Bear)

---

### Query 9: Find Protected Critical Assets
**Query:**
```
CriticalAsset and isProtectedBy some SecurityControl
```
**Check:** ☑ Instances
**Expected Result:** Critical assets that have security controls protecting them

---

### Query 10: Find Web Application Vulnerabilities
**Query:**
```
WebVulnerability or (Vulnerability and affects some WebApplication)
```
**Check:** ☑ Instances ☑ Subclasses
**Expected Result:** All web-related vulnerabilities (XSS, CSRF, SQLi, etc.)

---

### Query 11: Find Ransomware Targeting Financial Assets
**Query:**
```
Ransomware and targets some (Asset and ownedBy some FinancialOrganization)
```
**Check:** ☑ Instances
**Expected Result:** Ransomware threats targeting financial sector assets

---

### Query 12: Find All Physical Security Controls
**Query:**
```
PhysicalControl
```
**Check:** ☑ Instances ☑ Subclasses
**Expected Result:** Physical security controls (CCTV, Access cards, etc.)

---

### Query 13: Find Exploited Vulnerabilities (Property Chain)
**Query:**
```
Vulnerability and isExploitedBy some Threat
```
**Check:** ☑ Instances
**Expected Result:** Vulnerabilities that have been exploited by threats

---

### Query 14: Find Assets Requiring Urgent Patching
**Query:**
```
Asset and hasVulnerability some (Vulnerability and hasCVSS some xsd:float[>= 9.0])
```
**Check:** ☑ Instances
**Expected Result:** Assets with critical vulnerabilities (CVSS >= 9.0) needing urgent attention

---

### Query 15: Complex Query - APT Attack Chain
**Query:**
```
Asset and (isTargetedBy some (Threat and isInitiatedBy some NationStateActor))
```
**Check:** ☑ Instances
**Expected Result:** Assets targeted by nation-state sponsored threats

---

### 📸 SCREENSHOT 9: DL Query Execution (Optional)

**Location in Report**: Section 10.4 (Inference Testing) or Appendix

**How to Capture**:
1. In Protégé, go to **Window → Tabs → DL Query**
2. Paste Query 1: `HighRiskAsset`
3. Check ☑ Instances
4. Click **Execute**
5. Take screenshot showing:
   - The query in the editor
   - Results showing inferred instances
6. Save as `screenshot9_dl_query.png`

**Figure Caption**:
```
Figure 9: DL Query execution showing instances of HighRiskAsset inferred by the reasoner
```

---

### DL Query Syntax Reference

| Syntax | Meaning | Example |
|--------|---------|---------|
| `ClassName` | All instances of class | `Malware` |
| `and` | Intersection | `Asset and hasVulnerability some Vulnerability` |
| `or` | Union | `Server or Workstation` |
| `not` | Complement | `not HighRiskAsset` |
| `some` | Existential restriction | `exploits some Vulnerability` |
| `only` | Universal restriction | `hasVulnerability only CriticalVulnerability` |
| `value` | Has specific value | `hasSeverity value "Critical"` |
| `min N` | Minimum cardinality | `hasVulnerability min 2 Vulnerability` |
| `max N` | Maximum cardinality | `hasVulnerability max 5 Vulnerability` |
| `exactly N` | Exact cardinality | `hasVulnerability exactly 1 Vulnerability` |

---

### Tips for DL Queries

- **Always start the reasoner** before running DL queries (Reasoner → Start reasoner)
- **Use HermiT** for basic class queries (faster)
- **Use Pellet** when you need SWRL rule inferences
- **Check "Direct" boxes** to see only direct (not inherited) results
- **Combine queries** using `and` and `or` for complex searches
- Queries are **case-sensitive** - use exact class/property names from your ontology
