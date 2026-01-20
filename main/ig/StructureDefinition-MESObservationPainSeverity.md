# MESObservationPainSeverity - ANS IG Example v0.1.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **MESObservationPainSeverity**

## Resource Profile: MESObservationPainSeverity 

| | |
| :--- | :--- |
| *Official URL*:https://interop.esante.gouv.fr/ig/fhir/mesmesures/StructureDefinition/MESObservationPainSeverity | *Version*:0.1.0 |
| Draft as of 2026-01-20 | *Computable Name*:MESObservationPainSeverity |

**Utilisations:**

* Ce Profil nest utilisé par aucun profil dans ce guide dimplémentation

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/ans.fhir.fr.mesmesures|current/StructureDefinition/MESObservationPainSeverity)

### Formal Views of Profile Content

 [Description of Profiles, Differentials, Snapshots and how the different presentations work](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

 

Other representations of profile: [CSV](StructureDefinition-MESObservationPainSeverity.csv), [Excel](StructureDefinition-MESObservationPainSeverity.xlsx), [Schematron](StructureDefinition-MESObservationPainSeverity.sch) 



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "MESObservationPainSeverity",
  "url" : "https://interop.esante.gouv.fr/ig/fhir/mesmesures/StructureDefinition/MESObservationPainSeverity",
  "version" : "0.1.0",
  "name" : "MESObservationPainSeverity",
  "status" : "draft",
  "date" : "2026-01-20T13:17:20+00:00",
  "publisher" : "Agence du Numérique en Santé (ANS) - 2-10 Rue d'Oradour-sur-Glane, 75015 Paris",
  "contact" : [
    {
      "name" : "Agence du Numérique en Santé (ANS) - 2-10 Rue d'Oradour-sur-Glane, 75015 Paris",
      "telecom" : [
        {
          "system" : "url",
          "value" : "https://esante.gouv.fr"
        }
      ]
    }
  ],
  "jurisdiction" : [
    {
      "coding" : [
        {
          "system" : "urn:iso:std:iso:3166",
          "code" : "FR",
          "display" : "FRANCE"
        }
      ]
    }
  ],
  "fhirVersion" : "4.0.1",
  "mapping" : [
    {
      "identity" : "workflow",
      "uri" : "http://hl7.org/fhir/workflow",
      "name" : "Workflow Pattern"
    },
    {
      "identity" : "sct-concept",
      "uri" : "http://snomed.info/conceptdomain",
      "name" : "SNOMED CT Concept Domain Binding"
    },
    {
      "identity" : "v2",
      "uri" : "http://hl7.org/v2",
      "name" : "HL7 v2 Mapping"
    },
    {
      "identity" : "rim",
      "uri" : "http://hl7.org/v3",
      "name" : "RIM Mapping"
    },
    {
      "identity" : "w5",
      "uri" : "http://hl7.org/fhir/fivews",
      "name" : "FiveWs Pattern Mapping"
    },
    {
      "identity" : "sct-attr",
      "uri" : "http://snomed.org/attributebinding",
      "name" : "SNOMED CT Attribute Binding"
    }
  ],
  "kind" : "resource",
  "abstract" : false,
  "type" : "Observation",
  "baseDefinition" : "https://interop.esante.gouv.fr/ig/fhir/mesures/StructureDefinition/mesures-observation-pain-severity|3.0.1",
  "derivation" : "constraint",
  "differential" : {
    "element" : [
      {
        "id" : "Observation",
        "path" : "Observation"
      },
      {
        "id" : "Observation.meta.profile",
        "path" : "Observation.meta.profile",
        "fixedCanonical" : "https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-painseverity"
      }
    ]
  }
}

```
