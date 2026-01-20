# Spécifications techniques - ANS IG Example v0.1.0

* [**Table of Contents**](toc.md)
* **Spécifications techniques**

## Spécifications techniques

# Spécifications de l'API Mesures de santé de Mon Espace Santé

**Version 1.5.2** **Date : 21/07/2023**

## Documents référencés

| | |
| :--- | :--- |
| Volet mesures de santé v1.2 | Spécifications techniques d'alimentation et de consultation des mesures de santé |
| Spécifications d'interopérabilité au format Guide d'implémentation v3.0 | Spécifications techniques publiées sous forme d'Implementation Guide |

## Introduction à la documentation technique d'interopérabilité avec Mon espace santé

La documentation technique de Mon espace santé ne s'applique qu'aux services ayant ou visant à avoir des échanges de données avec MES.

Avant la lecture du présent document, il est conseillé de se référer au **Document chapeau des APIs Mon espace santé**, qui fonctionne comme un guide d'introduction à l'interopérabilité Mon espace santé et la documentation correspondante.

Ce document comprend :

* La liste des spécifications détaillant les échanges avec Mon espace santé ;
* Une présentation des tests d'interopérabilité requis pour compléter le référencement avec échange de données ;
* Un glossaire des spécifications techniques ;
* Une présentation du format des profils FHIR Mon espace santé et les liens pour les trouver ;
* Un ensemble de bonnes pratiques pour préparer son interopérabilité à Mon espace santé.

Le Document chapeau des APIs Mon espace santé peut être trouvé sur le portail de référencement à l'adresse [Référencement éditeurs (monespacesante.fr)](https://monespacesante.fr).

## 1. Objectif du document

Les interactions entre les partenaires et Mon Espace Santé (MES) s'organisent en trois phases préliminaires aux échanges :

* Une phase administrative de référencement et de contractualisation, couverte par le guide de référencement et le contrat de référencement ;
* Une phase de setup technique (connectivité, partage de secrets, certificats, etc.) couverte par la spécification sur la configuration technique des échanges ;
* L'appariement initial, pour un patient donné, entre le partenaire et Mon espace santé, avec son consentement à l'échange de données avec le partenaire, décrit dans la spécification 'API appariement' à venir mais non publiée dans cette concertation.

Cette documentation de référence définit comment interagir avec l'API Mesures de santé pour les partenaires.

## 2. Description des flux mesures

L'objectif de cette API mesures est de permettre aux systèmes partenaires interfacés avec MES de consulter les mesures d'un utilisateur ou d'en écrire afin de proposer à l'utilisateur une vue à jour de ses mesures de santé.

Toutes les requêtes doivent répondre aux exigences d'**authentification** et d'**identification** décrites dans la spécification d'appariement.

Ainsi, les flux décrits ci-dessous permettent :

* L'alimentation de mesures prises via des services tiers
* La consultation des mesures MES (créés par des services tiers ou saisis manuellement via l'IHM de MES)

### Dépendances

Ces profils ont comme dépendance les packages suivants :

| | | |
| :--- | :--- | :--- |
| ans.cisis.fhir.r4 | 2.0.0 | https://simplifier.net/packages/ans.cisis.fhir.r4/2.0.0 |
| HL7.fhir.uv.phd | 1.0.0 | https://simplifier.net/packages/hl7.fhir.uv.phd/1.0.0/files/596424 |

### 2.1. Ressources exploitées

#### 2.1.1. Observation

Les profils MES des objets "Observation" détaillés dans le volet des constantes de santé ont les champs **requis** suivants par défaut :

* `meta` 
* `profile`
 
* `status`
* `category` 
* `coding` 
* `system`
* `code`
 
 
* `code` 
* `coding` 
* `system`
* `code`
 
 
* `subject`
* `effectiveDateTime`

La ressource Observation permet d'indiquer les résultats de deux manières :

* via le champ `value[x]` s'il n'y a qu'un résultat
* via le champ `component` si l'observation est composée de plusieurs résultats (ex : pression artérielle)

Les profils FHIR des mesures de santé gérées par MES, sont définis avec l'ANS à travers le volet mesures de santé du CI-SIS.

##### Profils FHIR des mesures de santé

| | | |
| :--- | :--- | :--- |
| Poids | MESObservationBodyWeight | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-bodyweight |
| Taille | MESObservationBodyHeight | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-bodyheight |
| IMC | MESObservationBMI | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-bmi |
| Pression artérielle | MESObservationBP | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-bp |
| Température | MESObservationBodyTemperature | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-bodytemperature |
| Glucose | MESObservationGlucose | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-glucose |
| Niveau de douleur | MESObservationPainSeverity | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-painseverity |
| Nombre de pas | MESObservationStepsByDay | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-stepsbyday |
| Tour de taille | MESObservationWaistCircumference | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-waistcircumference |
| Tour de tête | MESObservationHeadCircumference | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-headcircumference |
| Fréquence cardiaque | MESObservationHeartrate | https://fhir.monespacesante.fr/ref/mesure/StructureDefinition/mes-observation-heartrate |

##### Extensions

Les extensions sont publiées sur l'Implementation Guide ANS : https://interop.esante.gouv.fr/ig/fhir/mesures/ImplementationGuide/ans.fhir.fr.mesures

| | | |
| :--- | :--- | :--- |
| MESReasonForMeasurement | https://interop.esante.gouv.fr/ig/fhir/mesures/StructureDefinition/mesures-reason-for-measurement | Motif de la mesure. Exprimé en texte libre. |
| MESMomentOfMeasurement | https://interop.esante.gouv.fr/ig/fhir/mesures/StructureDefinition/mesures-moment-of-measurement | Moment de la mesure. Exprimé par un texte libre ou un code. |
| MESNumberOfDays | https://interop.esante.gouv.fr/ig/fhir/mesures/StructureDefinition/mesures-number-of-days | Nombre de jours. Utilisé pour les mesures du taux de glucose interstitiel et l'index de gestion de glycémie. |
| MESDiabetisType | https://interop.esante.gouv.fr/ig/fhir/mesures/StructureDefinition/mesures-diabetis-type | Type de diabète. Utilisé pour déterminer le type de diabète de l'usager. |

#### 2.1.2. Device (profil PhdDevice)

Le profil "PhdDevice" s'utilise lorsque la mesure est faite par un objet connecté conforme aux normes "ISO / IEEE 11073-20601" pour les dispositifs de santé personnels (PHD – Personal Health) tels que les balances, les tensiomètres, les lecteurs de glycémie, etc.

Le profil "PhdDevice" est spécifié par IHE (package hl7.fhir.uv.phd, version 1.0.0) dans le document dont l'url correspond à : https://hl7.org/fhir/uv/phd/PhdDeviceProfile.html

Les détails des champs du profil sont disponibles en suivant l'adresse suivante : https://simplifier.net/packages/hl7.fhir.uv.phd/1.0.0/files/596424

##### Structure JSON d'un Device PHD (champs requis en gras)

```
{
  "resourceType": "Device",
  "meta": {
    "profile": [
      "http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice"
    ]
  },
  "id": "3bc44de3-069d-442d-829b-f3ef68cae372",
  "identifier": [
    {
      "type": {
        "coding": [
          {
            "system": "http://hl7.org/fhir/uv/phd/CodeSystem/ContinuaDeviceIdentifiers",
            "code": "SYSID"
          }
        ]
      },
      "system": "urn:oid:1.2.840.10004.1.1.1.0.0.1.0.0.1.2680",
      "value": "71-10-00-FE-FF-5F-49-B0"
    }
  ],
  "manufacturer": "ProDoc",
  "serialNumber": "SuperTM",
  "deviceName": [
    {
      "name": "SuperTM",
      "type": "manufacturer-name"
    }
  ],
  "modelNumber": "STM-1000A",
  "type": {
    "coding": [
      {
        "system": "urn:iso:std:iso:11073:10101",
        "code": "65573"
      }
    ]
  },
  "specialization": [
    {
      "systemType": {
        "coding": [
          {
            "system": "urn:iso:std:iso:11073:10101",
            "code": "528457"
          }
        ]
      },
      "version": "2.3"
    }
  ]
}

```

##### Codes Device

À noter les deux codes indiqués ci-dessus :

* Le code du champ "type" indique que le "Device" est un "Personal Health Device" ou "PHD". Il est donc toujours le même pour tous les PHD : **65573**.
* Le code du champs "specialization" indique ce que peut faire le PHD (balance, tensiomètre, fréquence cardiaque…). S'agissant d'une liste, le champ "specialization" peut donc contenir plusieurs codes. Par exemple, une montre connectée est généralement capable de mesurer une fréquence cardiaque et le nombre de pas quotidien, sa liste pourra donc contenir 2 codes.

Ci-dessous, une liste d'exemples de codes de specialization obtenus par la formule suivante :

```
(Code_de_Partition) x 2^16 + (Term_Code)

```

Le code de partition "8" correspondant à "INFRA".

Par exemple pour une balance "Weight Scale" : `8 x 2^16 + 4111 = 528399`

##### Codes MDC des spécialisations

| | | |
| :--- | :--- | :--- |
| Generic 20601 Device | 8::4169 | 528457 |
| Pulse Oximeter | 8::4100 | 528388 |
| Electro cardiograph | 8::4102 | 528390 |
| Blood Pressure Cuff | 8::4103 | 528391 |
| Thermometer | 8::4104 | 528392 |
| Respiration rate | 8::4109 | 528397 |
| Weight Scale | 8::4111 | 528399 |
| Glucose Monitor | 8::4113 | 528401 |
| Coagulation meter | 8::4114 | 528402 |
| Insulin Pump | 8::4115 | 528403 |
| Body Composition Analyzer | 8::4116 | 528404 |
| Peak Flow meter | 8::4117 | 528405 |
| Sleep Apnea Breathing Equipment | 8::4120 | 528408 |
| Continuous Glucose Monitor | 8::4121 | 528409 |
| Cardiovascular Device | 8::4137 | 528425 |
| Strength Equipment | 8::4138 | 528426 |
| Independent Activity/Living Hub | 8::4167 | 528455 |
| Medication Monitor | 8::4168 | 528456 |

Cette liste d'exemples est non-exhaustive et provient des spécifications FHIR. Obtenir d'autres codes MDC et donc d'autres codes de champs nécessite l'acquisition de la norme ISO/IEEE 11073-10101:2020.

### 2.2. Le flux d'alimentation de l'API mesures

Le flux d'alimentation unitaire d'une constante reprend la logique de la transaction "PCH 01" (Communicate FHIR PHD data) du profil "IHE POU" (Personal Health Device Observation Upload). Ce profil et cette transaction sont détaillés dans la documentation IHE.

Ce profil se base sur l'interaction "transaction" de l'API REST de FHIR. Il s'agit d'une requête http POST dont le corps est une ressource "Bundle" de type "transaction".

#### 2.2.1. Contenu de la requête d'alimentation

Le corps de cette requête contient un "Bundle" qui peut contenir jusqu'à deux ressources :

* Une ressource "Observation" issue du package ans.cisis.fhir.r4
* Une ressource optionnelle "Device" issue du package HL7.fhir.uv.phd, représentant le dispositif ayant effectué la mesure. Elle est référencée depuis l'attribut "device" de la ressource "Observation" : "Observation.device"

La ressource Device est optionnelle pour permettre l'alimentation d'une observation non issue d'un appareil de prise de mesure. Si un device est à l'origine de l'observation alors il doit être présent dans le bundle d'alimentation. La suite de cette documentation prend en compte l'hypothèse d'une alimentation d'observation avec Device.

#### 2.2.2. Structure de la requête d'alimentation

Les deux ressources Observation et Device sont incorporées dans la liste ("array") de Bundle.entry. Chaque élément de cette liste est un objet contenant 2 sous-objets : une ressource et la requête http associée.

Ci-dessous, la structure d'un "bundle" au format JSON contenant des ressources "Observation" et "Device" dans l'attribut Bundle.entry.

```
{
  "resourceType": "Bundle",
  "type": "transaction",
  "entry": [
    {
      "fullUrl": "11234563-069d-112d-829b-f01234567892",
      "resource": {
        "resourceType": "Observation",
        "meta": {
          "source": "<OID de la solution éditeur>",
          "profile": [
            "http://esante.gouv.fr/ci-sis/fhir/StructureDefinition/ENS_FrObservationBp"
          ]
        },
        ...
        "device": {
          "reference": "Device/3bc44de3-069d-442d-829b-f3ef68cae372"
        }
      },
      "request": {
        "method": "POST",
        "url": "Observation"
      }
    },
    {
      "resource": {
        "resourceType": "Device",
        "meta": {
          "profile": [
            "http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice"
          ]
        },
        "id": "3bc44de3-069d-442d-829b-f3ef68cae372",
        ...
      },
      "request": {
        "method": "POST",
        "url": "Device",
        "ifNoneExist": "identifier=urn:oid:<OID du PHD|Identifier PHD>"
      }
    }
  ]
}

```

Le champ "type" du "bundle" doit être fixé à "transaction", l'attribut "request" doit être présent avec la method POST et l'url avec le resourceType.

À noter que la validation FHIR requiert l'incorporation d'un champ "fullUrl" pour l'observation.

##### 2.2.2.1. L'attribut « ifNoneExist »

L'attribut ifNoneExist contenant l'oid du device (« sous oid » de la solution éditeur) et son identifier est obligatoire pour la ressource Device. Cet attribut permet d'exécuter la transaction « conditional create » pour les Devices :

* Si le device existe déjà dans l'entrepôt de l'ENS identifié par le couple oid/identifier, il n'est pas recréé (code 200 Success retourné).
* S'il n'existe pas, il sera créé (code 201 Created retourné) avec comme identifiant unique le couple oid + identifier.

#### 2.2.3. Référence de la ressource Observation vers la ressource Device (Observation.device)

La ressource Device doit être référencée dans l'attribut Observation.device.reference. Ainsi, il doit contenir le préfixe « Device/ » et le Device.id doit contenir uniquement l'uuid.

#### 2.2.4. L'attribut « Observation.meta.source »

Le système source de la donnée est indiqué dans le champ meta de l'observation. Le champ source contient l'oid de la solution à l'origine de l'alimentation de l'observation.

Ce champ est facultatif :

* S'il est envoyé par la solution lors de la demande d'alimentation, il est validé par MES : il doit commencer par l'oid de la solution authentifiée sur l'API. Ceci permet d'indiquer des sous-oid de la solution principale.
* S'il n'est pas fourni, l'oid de la solution authentifiée sur l'API est positionné par MES.

#### 2.2.5. L'attribut « meta.profile »

L'Observation et le Device doivent renseigner l'url canonique du profil dans le champs meta.profile. Cette information est nécessaire, elle permet de valider la conformance des ressources Device avec le profil PhdDevice ainsi que celle des ressources Observation avec l'un des 11 profils des mesures de santé.

#### 2.2.6. Cas particulier de la glycémie

Le profil ENS_ObservationGlucose permet de gérer 4 types d'indicateurs de glycémie :

* Le taux de glucose sanguin, mesuré en mg/dl
* Le taux de glucose interstitiel, mesuré en mg/dl
* L'hémoglobine glyquée (Hb1Ac) mesurée en %
* L'index de gestion de glycémie (IGG) qui procure une estimation de l'HbA1c également mesuré en %

En fonction du type de glycémie, des contrôles métiers sur les extensions ENS_NumberOfDays (Nombre de jours) et ENS_MomentOfMeasurement (Contexte de la mesure) sont effectués par l'ENS :

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| **Unité** | mg/dl | % | mg/dl | % |
| **Contexte de la mesure**(Liste : à jeun, après un repas, après l'effort, lors d'un malaise et autre) | ✅ | ❌ | ❌ | ❌ |
| **Nombre de jours**(Liste : 7j, 14 j, 30 j, 90 j et autre) | ❌ | ❌ | ✅ | ✅ |
| **Commentaire** | ✅ | ✅ | ✅ | ✅ |

* ❌ Si une extension non autorisée est présente, l'observation sera considérée comme étant invalide.
* ✅ Si une extension obligatoire est absente, l'observation sera considérée comme étant invalide. Le commentaire reste facultatif dans tous les cas.

#### 2.2.7. Exemple d'appel

Ci-dessous, un exemple de "Bundle" complet qui doit être envoyé dans le corps de la requête d'alimentation. Ce Bundle contient 2 ressources dans l'attribut "entry" :

* Une ressource Observation ENS_FrObservationBodyWeight
* Une ressource Device responsable de la mesure avec : 
* comme identifiant unique au sein de l'ENS : `urn:oid:1.2.840.10004.1.1.1.0.0.1.0.0.1.2680|FE-ED-AB-AA-DE-AD-77-C5`
* la spécialisation Generic 20601 Device (code 528457)
 

```
{
  "resourceType": "Bundle",
  "type": "transaction",
  "entry": [
    {
      "resource": {
        "resourceType": "Device",
        "id": "3bc44de3-069d-442d-829b-f3ef68cae371",
        "meta": {
          "profile": [
            "http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice"
          ]
        },
        "identifier": [
          {
            "type": {
              "coding": [
                {
                  "system": "http://hl7.org/fhir/uv/phd/CodeSystem/ContinuaDeviceIdentifiers",
                  "code": "SYSID"
                }
              ]
            },
            "system": "urn:oid:1.2.840.10004.1.1.1.0.0.1.0.0.1.2680",
            "value": "FE-ED-AB-AA-DE-AD-77-C5"
          }
        ],
        "manufacturer": "OMRONHEALTHCARE",
        "modelNumber": "HEM-9200T",
        "deviceName": [
          {
            "name": "Ma balance",
            "type": "patient-reported-name"
          }
        ],
        "type": {
          "coding": [
            {
              "system": "urn:iso:std:iso:11073:10101",
              "code": "65573"
            }
          ]
        },
        "specialization": [
          {
            "systemType": {
              "coding": [
                {
                  "system": "urn:iso:std:iso:11073:10101",
                  "code": "528457"
                }
              ]
            },
            "version": "2.3"
          }
        ]
      },
      "request": {
        "method": "POST",
        "url": "Device",
        "ifNoneExist": "identifier=urn:oid:1.2.840.10004.1.1.1.0.0.1.0.0.1.2680|FE-ED-AB-AA-DE-AD-77-C5"
      }
    },
    {
      "fullUrl": "3bc44de3-069d-442d-829b-f3ef68cae372",
      "resource": {
        "resourceType": "Observation",
        "meta": {
          "profile": [
            "http://esante.gouv.fr/ci-sis/fhir/StructureDefinition/ENS_FrObservationBodyWeight"
          ]
        },
        "status": "final",
        "category": [
          {
            "coding": [
              {
                "system": "http://terminology.hl7.org/CodeSystem/observation-category",
                "code": "vital-signs",
                "display": "Signes vitaux"
              }
            ]
          }
        ],
        "code": {
          "coding": [
            {
              "system": "http://loinc.org",
              "code": "29463-7",
              "display": "Poids corporel"
            }
          ]
        },
        "subject": {
          "identifier": {
            "system": "urn:oid:1.2.840.10004.1.1.1.0.0.1.0.0.1.2560",
            "value": ""
          }
        },
        "device": {
          "reference": "Device/3bc44de3-069d-442d-829b-f3ef68cae371"
        },
        "effectiveDateTime": "2022-08-22T01:56:16+01:00",
        "valueQuantity": {
          "value": 71,
          "unit": "kg",
          "system": "http://unitsofmeasure.org",
          "code": "kg"
        },
        "extension": [
          {
            "url": "http://esante.gouv.fr/ci-sis/fhir/StructureDefinition/ENS_ReasonForMeasurement",
            "valueString": "Mon nouveau poids !"
          }
        ]
      },
      "request": {
        "method": "POST",
        "url": "Observation"
      }
    }
  ]
}

```

##### 2.2.7.1. Cas particulier de la pression artérielle

Dans le cas de la pression artérielle, il y a deux résultats : la pression artérielle systolique et diastolique.

Ainsi, dans le cas du profil MESFrObservationBp, l'usage de value[x] est interdit, il faut utiliser le champs component. Voici un exemple de pression artérielle à intégrer dans un bundle :

```
{
  "resourceType": "Observation",
  "meta": {
    "profile": [
      "http://esante.gouv.fr/ci-sis/fhir/StructureDefinition/ENS_FrObservationBp"
    ]
  },
  "component": [
    {
      "code": {
        "coding": [
          {
            "system": "http://loinc.org",
            "code": "8480-6"
          }
        ]
      },
      "valueQuantity": {
        "value": 120,
        "unit": "mm[Hg]",
        "system": "http://unitsofmeasure.org",
        "code": "mm[Hg]"
      }
    },
    {
      "code": {
        "coding": [
          {
            "system": "http://loinc.org",
            "code": "8462-4"
          }
        ]
      },
      "valueQuantity": {
        "value": 60,
        "unit": "mm[Hg]",
        "system": "http://unitsofmeasure.org",
        "code": "mm[Hg]"
      }
    }
  ]
}

```

#### 2.2.8. Réponse à la requête d'alimentation

En cas de succès, le code http **200 OK** est retourné.

Le corps de la réponse contient une ressource Bundle de type « transaction-response » avec la liste des réponses pour chaque ressource envoyée. Chacune de ces réponses contient :

* Un http Status code : 
* Le status « 201 Created » pour les ressources créées sur MES. Pour rappel, si le Device identifié via l'attribut ifNoneExist du bundle n'existe pas dans l'entrepôt FHIR, il est créé et le statut « 201 Created » est renvoyé pour la ressource Device.
* Le statut « 200 Success » est renvoyé si le Device est déjà existant
 
* Un attribut location contenant la localisation de la ressource

Voici un exemple de retour à la suite de la création d'une Observation et d'un nouveau Device :

```
{
  "resourceType": "Bundle",
  "type": "transaction-response",
  "entry": [
    {
      "response": {
        "status": "201 Created",
        "location": "Observation/29680733-6158-4e22-ab7e-eb6825dcdb13"
      }
    },
    {
      "response": {
        "status": "201 Created",
        "location": "Device/3bc44de3-069d-442d-829b-f3ef68cae371"
      }
    }
  ]
}

```

##### Codes d'erreur

Dans le cas d'une erreur rencontrée, un code erreur HTTP est retourné :

| | | | |
| :--- | :--- | :--- | :--- |
| 400 | Bad Request | HTTP code 400 : Bad request -> The ID_TOKEN value is not valid (invalid JWT) |   |
| 401 | Unauthorized |   | L'access_token est invalide |
| 403 | Forbidden | idPe requested do not match authorized idPe. | idPe dans la request ne correspond pas à l'idPe de l'id_token |
| 403 | Forbidden | Consent not given, access refused. | L'usager n'a pas donné son consentement pour l'opération d'écriture demandée. |
| 400 | Bad Request | No bundle provided. |   |
| 409 | Conflict | HTTP code 409 :OID conflict between the one from id_token and the one in the system -> OID different between id_token and ecosystem |   |

##### OperationOutcome

Le corps de la réponse contient une ressource Bundle de type « transaction-response ». Cette ressource contient le détail des erreurs et avertissements résultants du traitement de la requête transmise à MES.

En cas d'erreur, une ressource OperationOutcome est renvoyée avec le code HTTP « 422 Unprocessable Entity » :

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| 0 | OperationOutcome | 0..1 |   |   |
| 1 | Issue | 1..* | BackboneElement |   |
| 2 | Severity | 1..1 | Code | Criticité de l'erreur (http://hl7.org/fhir/ValueSet/issue-severity) |
| 2 | Code | 1..1 | Code | Type d'erreur (http://www.hl7.org/fhir/valueset-issue-type.html) |
| 2 | Diagnostics | 0..1 | String | Informations complémentaires sur l'erreur |

##### Liste des erreurs de validation

| | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 422 | Bundle not valid. | NOTSUPPORTED | Resource of type <> is not acceptable with method <>. | L'API ne prend en charge que les ressources Observation ou Device en POST. |   |
| 422 | Bundle not valid. | INVALID | Device request must have a valid IfNoneExist attribute : identifier=urn:oid:<OID> | <DEVICE ID> | Si un device est présent, l'identifier du device présent dans l'attribut « ifNoneExist » doit respecter la regex |
| 422 | Bundle not valid. | INVALID | Bundle must contains one observation creation (POST) |   |   |
| 422 | Observation and Device link not valid. | INVALID | Observation.device.reference is mandatory. |   |   |
| 422 | Observation and Device link not valid. | INVALID | Observation and device not linked by id (Observation.device.reference <-> Device.id) |   |   |
| 422 | Observation resource not valid. | INVALID | Observation must provide meta.profile value. |   |   |
| 422 | Observation resource not valid. | VALUE | Solution oid contains in Observation.meta.source don't belong to root editor oid (<OID>). | Si cet attribut est fourni, il est validé. |   |
| 422 | Observation resource not valid. | VALUE | Observation value quantity not provided. | Dans l'ENS, des observations sans valeur sont refusées |   |
| 422 | Observation resource not valid. | NOTSUPPORTED | Bmi observation cannot be created. | Les observations IMC sont calculées à la volée |   |
| 422 | Observation resource not valid. | INVALID | Observation.subject.identifier is mandatory. | Ce champ doit contenir le couple oid/IDPE |   |
| 422 | Observation resource not valid. | INCOMPLETE | Observation.extension.moment is mandatory. | Se référer au cas particulier de la glycémie |   |
| 422 | Observation resource not valid. | INVALID | Observation.extension.numberOfDays cannot be added. | Se référer au cas particulier de la glycémie |   |
| 422 | Observation resource not valid. | INVALID | Observation.extension.moment cannot be added. | Se référer au cas particulier de la glycémie |   |
| 422 | Observation resource not valid. | INCOMPLETE | Observation.extension.numberOfDays is mandatory. | Se référer au cas particulier de la glycémie |   |
| 422 | Device resource not valid. | INVALID | Device must provide meta.profile value. |   |   |

### 2.3. Le flux de recherche de l'API mesures

L'API de lecture des observations consiste en une requête de type Search qui suit la spécification FHIR.

#### 2.3.1. Modes de recherche

Deux modes de recherche sont mis à disposition. Pour faciliter la suite de la documentation, nous les appellerons « all » et « last ».

La recherche **« all »** recherche toutes les observations pour un code mesures (Observation.code) donné sur une période. Toutes les observations dont l'Observation.effectiveDateTime est comprise dans la période seront retournées.

La recherche **« last »** permet de récupérer la dernière observation pour un code mesures (Observation.code) donné.

##### 2.3.1.1. Paramètres d'appel de l'opération Search

| | | | |
| :--- | :--- | :--- | :--- |
| code | Obligatoire | Code correspondant à l'observation recherchée | Code LOINC du type d'observation recherché :• 29463-7 : Body weight• 8302-2 : Body height• 8280-0 : Waist circumference• 8310-5 : Body temperature• 2345-7 : Glucose• MED-969 : Interstitial Glucose• 4548-4 : Glycated hemoglobin• MED-972 : Hemoglobin glycation index• 85354-9 : Blood pressure• 39156-5 : Body Mass Index• 72514-3 : Pain severity• 8867-4 : Heart rate• 41950-7 : Steps By Day• 8287-5 : Head circumference |
| subject.identifier | Obligatoire | « Dérivé de l'OID identifiant le patient lors de l'appariement (AssignAuth) » + « | » + « Identifiant du patient (idpe) » | Un contrôle est effectué pour s'assurer que ce patient est cohérent avec les informations d'identification |
| date | Obligatoire pour la recherche « all » | Période sur laquelle s'applique la rechercheEx : date=ge2021-02-16&date=le2021-02-26 | https://hapifhir.io/hapi-fhir/docs/server_plain/rest_operations_search.html#DATE_RANGEShttp://hl7.org/fhir/search.html#dateSi une borne est définie, les deux sont obligatoires. Lorsque les deux champs dates sont fournis, toutes les mesures dont l'Observation.effectiveDateTime se situe entre les deux dates sont retournées |
| _include | Facultatif | Observation:device | Si le paramètre _include est présent et s'il contient « Observation:device », alors les ressources Device sont incluses dans le bundle de retour sans doublonhttp://hl7.org/fhir/r4/search.html#include |
| _offset | Facultatif | Numéro de page | La première page à l'index 0. Valeur par défaut : 0 |
| _count | Facultatif pour « all »Obligatoire pour « last » | Nombre d'observations par page | Maximum : 100. Valeur par défaut : 50L'inclusion ou non des devices n'a pas d'impact sur ce compteur. |
| _sort | Obligatoire pour « last » | Doit toujours être égal à « -date » |   |

#### 2.3.2. Exemples d'appel

##### Recherche « all » :

```
https://<baseUrl>/fhir/Observation?subject.identifier=&code=29463-7&date=gt2022-09-04&date=lt2022-09-23&_offset=0&_count=2&_include=Observation.device

```

| | |
| :--- | :--- |
| **Attention**: Si vous effectuez vos tests via Postman vous devez remplacer le « | » séparant l'AssignAuth et l'idpe par « %7C ». |

Cette requête permet de récupérer, pour l'usager ayant l'identifiant Patient Externe « idPe », avec une pagination de deux ressources Observation par page :

* Les observations Poids ayant une effectiveDate entre le 04/09/2022 et le 23/09/2022
* Les devices liés aux observations remontées (si un même device est rattaché à plusieurs observations, il ne sera présent qu'une fois dans la réponse)

##### Requête « last » :

```
https://<baseUrl>/fhir/Observation?subject.identifier=&code=29463-7&_sort=-date&_count=1&_include=Observation.device

```

Elle permet de récupérer, pour l'usager ayant l'identifiant Patient Externe « idPe » :

* La dernière observation Poids
* Le device associé à l'observation remontée

#### 2.3.3. Réponse à la requête de recherche

Quel que soit le mode de recherche, le corps de la réponse contient un bundle de type searchset avec pagination (présence des liens previous/self/next pour naviguer dans la pagination).

Exemple de retour de la première page de 2 observations d'une recherche contenant 4 observations au total. Le device remonté étant commun aux 2 observations, il n'est présent qu'une fois :

```
{
  "resourceType": "Bundle",
  "id": "0479299d-e813-480b-a00d-4e96b50299e3",
  "meta": {
    "lastUpdated": "2022-09-22T04:23:24.163+02:00"
  },
  "type": "searchset",
  "total": 4,
  "link": [
    {
      "relation": "next",
      "url": "http://<BaseURL>/fhir/Observation?subject.identifier=patient-externe-id-2&code=29463-7&date=2022-09-04&_offset=1&_count=2&_include=Observation.device"
    },
    {
      "relation": "self",
      "url": "http://<BaseURL>/fhir/Observation?subject.identifier=patient-externe-id-2&code=29463-7&date=2022-09-04&_offset=0&_count=2&_include=Observation.device"
    }
  ],
  "entry": [
    {
      "resource": {
        "resourceType": "Observation",
        "id": "3bc44de3-069d-442d-829b-f3ef68cae372",
        "meta": {
          "source": "urn:oid:1.2.250.1.215.400",
          "profile": [
            "http://esante.gouv.fr/ci-sis/fhir/StructureDefinition/ENS_FrObservationBodyWeight"
          ]
        },
        "extension": [
          {
            "url": "http://esante.gouv.fr/ci-sis/fhir/StructureDefinition/ENS_ReasonForMeasurement",
            "valueString": "Mon nouveau poids !"
          }
        ],
        "status": "final",
        "category": [
          {
            "coding": [
              {
                "system": "http://terminology.hl7.org/CodeSystem/observation-category",
                "code": "vital-signs",
                "display": "Signes vitaux"
              }
            ]
          }
        ],
        "code": {
          "coding": [
            {
              "system": "http://loinc.org",
              "code": "29463-7",
              "display": "Poids corporel"
            }
          ]
        },
        "subject": {
          "identifier": {
            "system": "urn:oid:1.2.250.1.215.400",
            "value": "patient-externe-id-2"
          }
        },
        "effectiveDateTime": "2022-09-22T01:56:16+01:00",
        "valueQuantity": {
          "value": 71,
          "unit": "kg",
          "system": "http://unitsofmeasure.org",
          "code": "kg"
        },
        "device": {
          "reference": "Device/75d4e824-7ea3-4719-90f4-c9d9ce871239"
        }
      }
    },
    {
      "resource": {
        "resourceType": "Device",
        "id": "75d4e824-7ea3-4719-90f4-c9d9ce871239",
        "meta": {
          "profile": [
            "http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice"
          ]
        },
        "identifier": [
          {
            "type": {
              "coding": [
                {
                  "system": "http://hl7.org/fhir/uv/phd/CodeSystem/ContinuaDeviceIdentifiers",
                  "code": "SYSID"
                }
              ]
            },
            "system": "urn:oid:1.2.840.10004.1.1.1.0.0.1.0.0.1.2680",
            "value": "FE-ED-AB-AA-DE-AD-77-C5"
          }
        ],
        "manufacturer": "OMRONHEALTHCARE",
        "serialNumber": "20150200002A",
        "deviceName": [
          {
            "name": "Ma balance",
            "type": "patient-reported-name"
          }
        ],
        "modelNumber": "HEM-9200T",
        "type": {
          "coding": [
            {
              "system": "urn:iso:std:iso:11073:10101",
              "code": "65573"
            }
          ]
        },
        "specialization": [
          {
            "systemType": {
              "coding": [
                {
                  "system": "urn:iso:std:iso:11073:10101",
                  "code": "528457"
                }
              ]
            },
            "version": "2.3"
          }
        ]
      }
    }
  ]
}

```

##### Codes d'erreur

Dans le cas d'une erreur rencontrée, un code erreur HTTP est retourné :

| | | |
| :--- | :--- | :--- |
| 400 | Bad Request | HTTP code 400 : Bad request -> The ID_TOKEN value is not valid (invalid JWT) |
| 401 | Unauthorized | L'access_token est invalide |
| 403 | Forbidden | idPe requested do not match authorized idPe. (idPe dans la request ne correspond pas à l'idPe de l'id_token) |
| 403 | Forbidden | Consent not given, access refused. (L'usager n'a pas donné son consentement pour l'opération de lecture demandée) |
| 409 | Conflict | HTTP code 409 :OID conflict between the one from id_token and the one in the system -> OID different between id_token and ecosystem |

Dans le cas où la requête ne serait pas valide, un code HTTP « 400 Request not valid » sera renvoyé avec une ressource OperationOutcome dans le corps de la réponse. Cette ressource contient le détail des erreurs et avertissements résultants du traitement de la requête transmise par MES.

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| 400 | Request not valid | INVALID | Maximum page size allowed is <max_page_size>. Actual : <request_pageSize> |   |
| 400 | Request not valid | INVALID | Sort parameter must be equals to -date (date DESC) with _count equals to 1 to retrieve last observation | Dans le cas d'une recherche « last » |
| 400 | Request not valid | INVALID | Paged search and search last cannot be requested concurrently |   |
| 400 | Request not valid | INVALID | No search mode detected |   |

