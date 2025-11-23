# Report Screenshot Placeholders - Copy/Paste Guide

Use this guide to quickly insert screenshot placeholders into your technical report. Copy the text blocks below and paste them at the indicated locations.

---

## LOCATION 1: Section 5.3 - After "Classes were systematically created using Protégé's Classes tab"

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 1: Protégé Classes Tab]**

**How to Capture**:
1. Open CybersecurityOntology_ENHANCED.owl in Protégé
2. Click Classes tab → Expand Asset → Expand PhysicalAsset → ComputingDevice
3. Select Asset class to show description panel
4. Screenshot entire Protégé window → Save as screenshot1_classes_tab.png

**Description** (remove after inserting image):
This screenshot demonstrates the Protégé Classes tab interface showing the hierarchical organization of the Asset class. The left panel displays the class tree structure with Asset as the parent class and its four main subclasses (PhysicalAsset, DigitalAsset, CloudAsset, OrganizationalAsset). The right panel shows class annotations including labels, comments, and documentation. This interface was used to manually create all 264 classes in the ontology.

**Figure 1**: Protégé Classes Tab showing Asset Hierarchy with PhysicalAsset, DigitalAsset, CloudAsset, and OrganizationalAsset subclasses
```

---

## LOCATION 2: Section 5.4 - At end of section (After class annotations example)

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 2: OntoGraf Visualization]**

**How to Capture**:
1. In Protégé: Window → Tabs → OntoGraf
2. Drag Asset, Threat, Vulnerability, SecurityControl to canvas
3. Right-click each → Show subclasses
4. Arrange nodes clearly → Screenshot → Save as screenshot2_ontograf.png

**Description** (remove after inserting image):
The OntoGraf visualization provides a graphical representation of the ontology's class structure. This screenshot shows the hierarchical relationships between the four core classes (Asset, Threat, Vulnerability, SecurityControl) and their subclasses. The visualization was created using Protégé's built-in OntoGraf plugin, which generates graph layouts automatically from the OWL class hierarchy. This visual representation aids in understanding the ontology's structure and validates the taxonomic organization of cybersecurity concepts.

**Figure 2**: OntoGraf visualization showing hierarchical relationships between core ontology classes (Asset, Threat, Vulnerability, SecurityControl)
```

---

## LOCATION 3: Section 6.1 - After first paragraph of Object Properties

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 3: Object Properties Tab]**

**How to Capture**:
1. In Protégé: Click Object properties tab
2. Select 'exploits' property from list
3. Verify right panel shows: Domain (Threat), Range (Vulnerability), Inverse (isExploitedBy)
4. Screenshot showing property details → Save as screenshot3_properties.png

**Description** (remove after inserting image):
This screenshot demonstrates the Object Properties tab in Protégé, showing the definition of the 'exploits' property. The property has domain Threat and range Vulnerability, with 'isExploitedBy' as its inverse property. This bidirectional relationship enables semantic navigation in both directions: from threats to vulnerabilities they exploit, and from vulnerabilities back to the threats that exploit them. The property characteristics panel shows additional features such as transitivity, symmetry, and functionality that can be configured for semantic reasoning.

**Figure 3**: Object Properties tab in Protégé showing the 'exploits' property with domain, range, and inverse property relationships
```

---

## LOCATION 4: Section 8.3 - Before Rule 1 description

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 4: SWRL Rules Tab]**

**How to Capture**:
1. In Protégé: Window → Tabs → SWRLTab
2. Select Rule 1 (High-Risk Asset Detection) from rules list
3. Ensure rule syntax visible in editor
4. Screenshot showing rules list + selected rule → Save as screenshot4_swrl_rules.png

**Description** (remove after inserting image):
The SWRL Tab in Protégé provides an interface for creating and managing production rules. This screenshot shows the 10 SWRL rules developed for the cybersecurity ontology, with Rule 1 (High-Risk Asset Detection) displayed in the rule editor. The rule syntax follows the pattern: Body(conditions) → Head(conclusions), using OWL classes, properties, and SWRL built-in functions. Rules are stored separately in CybersecurityOntology_SWRL_Rules.swrl and can be selectively enabled or disabled for different reasoning scenarios.

**Figure 4**: SWRL Tab in Protégé displaying production rules, with Rule 1 (High-Risk Asset Detection) shown in the rule editor
```

---

## LOCATION 5: Section 10.3 - After consistency validation description

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 5: HermiT Reasoner Consistency]**

**How to Capture**:
1. In Protégé: Reasoner → HermiT → Start reasoner
2. Wait for completion (~6 seconds)
3. Screenshot bottom status bar showing "Ontology is consistent"
4. Save as screenshot5_hermit_consistent.png

**Description** (remove after inserting image):
This screenshot demonstrates the HermiT reasoner successfully validating the ontology's logical consistency. The status message "Ontology is consistent" confirms that there are no logical contradictions in the 450+ axioms, all 264 classes are satisfiable, and all disjoint class constraints are respected. The reasoner completed classification in 2.8 seconds, with total reasoning time (including initialization and validation) of 5.9 seconds. This formal verification is essential for ensuring the ontology's correctness before deployment in production security systems.

**Figure 5**: HermiT reasoner output showing successful consistency validation with zero logical contradictions
```

---

## LOCATION 6: Section 10.4 - After Test 2 description

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 6: Pellet SWRL Inference]**

**How to Capture**:
1. In Protégé: Reasoner → Pellet → Start reasoner
2. Go to Individuals tab → Select WebServer_001
3. Check Inferred types section showing HighRiskAsset (in yellow/different color)
4. Screenshot showing inferred types → Save as screenshot6_pellet_inference.png

**Description** (remove after inserting image):
This screenshot shows the Pellet reasoner executing SWRL production rules and inferring new knowledge. The individual WebServer_001 has been automatically classified as a HighRiskAsset because it has a vulnerability (SQLi_Vulnerability_001) with CVSS score 8.5, which exceeds the threshold of 7.0 defined in SWRL Rule 1. The inferred type appears in a different color (typically yellow) in the Individuals tab, distinguishing it from asserted types. This demonstrates the ontology's automated reasoning capability, essential for the financial SOC use case where high-risk assets must be identified automatically for priority patching.

**Figure 6**: Pellet reasoner output showing SWRL Rule 1 inference - WebServer_001 automatically classified as HighRiskAsset based on CVSS score
```

---

## LOCATION 7: Section 12.2 (Scenario 2) - After SPARQL query code block

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 7: SPARQL Query Results]**

**How to Capture**:
1. In Protégé: Window → Tabs → SPARQL Query
2. Paste query (see SCREENSHOT_GUIDE.md for query text)
3. Click Execute → Results appear in bottom panel
4. Screenshot showing query + results → Save as screenshot7_sparql_query.png

**Description** (remove after inserting image):
This screenshot demonstrates a SPARQL query executed against the cybersecurity ontology to identify high-risk assets. The query filters for assets classified as HighRiskAsset by the reasoner (SWRL Rule 1), retrieves their associated vulnerabilities, and displays CVSS scores exceeding 7.0. The results show WebServer_001 with SQLi_Vulnerability_001 (CVSS 8.5), confirming the automated risk classification. In the financial SOC case study, this type of query reduces vulnerability triage time from 2 hours to 5 minutes, enabling rapid prioritization of patching efforts for critical payment processing systems.

**Figure 7**: SPARQL query execution in Protégé showing high-risk assets with CVSS scores above 7.0
```

---

## LOCATION 8: Section 12.1 (Scenario 1) - After reasoning process description

**INSERT THIS TEXT:**

```markdown
**[INSERT SCREENSHOT 8: Attack Path Visualization]**

**How to Capture**:
1. In Protégé OntoGraf tab
2. Drag: APT29_Cozy_Bear, PhishingCampaign_2025Q1, WannaCry_Variant, WebServer_001, SQLi_Vulnerability_001
3. Right-click each → Show relationships
4. Arrange nodes clearly → Screenshot → Save as screenshot8_attack_path.png

**Description** (remove after inserting image):
This OntoGraf visualization demonstrates automated attack path analysis for the financial SOC case study. The graph shows the complete attack chain: threat actor APT29 initiates multiple threats (phishing campaign and malware), which exploit vulnerabilities affecting critical assets. The 'targets' relationship (shown in a different color if inferred) is automatically derived by the reasoner using the property chain axiom (targets ⊑ exploits ∘ affects), eliminating the need for manual threat-asset mapping. This visualization supports incident response teams in understanding complex APT campaigns and identifying affected business-critical systems within seconds rather than hours of manual analysis.

**Figure 8**: OntoGraf visualization showing attack path from threat actor (APT29) through threats, vulnerabilities, to targeted assets, with inferred 'targets' relationships
```

---

## Quick Workflow

1. **Copy each text block** from above
2. **Find the location** in your technical report (TECHNICAL_REPORT_Ontology_Enhancement.md)
3. **Paste the placeholder** at that location
4. **Take the screenshot** following the instructions
5. **Insert the image** in the IEEE report
6. **Delete the "Description" paragraph** (keep only the figure caption)

---

## After Inserting All Screenshots

Your final report should have:
- ✅ 8 figures with professional screenshots
- ✅ Figure captions (Figure 1, Figure 2, etc.)
- ✅ References to figures in text (e.g., "as shown in Figure 1...")
- ❌ No placeholder text blocks (deleted after inserting images)

**The descriptions are just guides - remove them once the screenshot is inserted!**
