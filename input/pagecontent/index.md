<div style="width: 65%">
    <blockquote class="dragon">
    <p>Guide d'implémentation de démo, celui-ci n'a pas vocation à être utilisé</p>
    </blockquote>
</div>


<p style="padding: 5px; border-radius: 5px; border: 2px solid maroon; background: #ffffe6; width: 65%">
<b>Guide d'Implémentation FHIR - API Mesures de santé de Mon Espace Santé</b><br>
Ce guide d'implémentation définit les spécifications FHIR pour l'interopérabilité avec l'API Mesures de santé de Mon Espace Santé, permettant aux systèmes partenaires de consulter et d'alimenter les mesures de santé des utilisateurs.
</p>

{% if site.data.info.releaselabel == 'ci-build' %}
<div style="width: 65%">
    <blockquote class="stu-note">
    <p>Cet Implementation Guide n'est pas la version courante, il s'agit de la version en intégration continue soumise à des changements fréquents uniquement destinée à suivre les travaux en cours. La version courante sera accessible via l'URL canonique suite à la première release : https://interop.esante.gouv.fr/ig/fhir/mesmesures</p>
    </blockquote>
</div>
{% endif %}

{% if site.data.info.releaselabel == 'public-comment' %}
<div style="width: 65%">
<blockquote class="stu-note">
<p>
  <b>Attention !</b>
  <br>
 Cet Implementation Guide est actuellement en concertation. La version courante est accessible à l'adresse : https://interop.esante.gouv.fr/ig/fhir/mesmesures
</p>
</blockquote>
</div>
{% endif %}

Ce guide d'implémentation est un test pour mettre MonEspaceSanté au format IG, et également un test pour mettre plusieurs versions du même package en dépendance.

### Introduction

La documentation technique de Mon espace santé s'applique aux services ayant ou visant à avoir des échanges de données avec MES (Mon Espace Santé).

Ce guide d'implémentation présente les spécifications FHIR de l'**API Mesures de santé** qui permet aux systèmes partenaires interfacés avec Mon Espace Santé de :
- Consulter les mesures d'un utilisateur
- Alimenter des mesures prises via des services tiers
- Proposer à l'utilisateur une vue à jour de ses mesures de santé

Les principales sections de l'IG sont :

* **Spécifications techniques** : Description détaillée des flux d'alimentation et de recherche
* **Ressources de conformité** : Profils FHIR des mesures de santé (Observation, Device)
* **Historique des versions** : Suivi des évolutions de l'API

### Périmètre du projet

L'API Mesures de santé permet l'échange de **11 types de mesures de santé** entre les systèmes partenaires et Mon Espace Santé :

- Poids corporel (Body Weight)
- Taille (Body Height)
- Indice de Masse Corporelle - IMC (Body Mass Index)
- Pression artérielle (Blood Pressure)
- Température corporelle (Body Temperature)
- Glycémie (Glucose)
- Niveau de douleur (Pain Severity)
- Nombre de pas quotidien (Steps By Day)
- Tour de taille (Waist Circumference)
- Tour de tête (Head Circumference)
- Fréquence cardiaque (Heart Rate)

Les flux couverts sont :
- **Flux d'alimentation** : Envoi de mesures vers Mon Espace Santé via un Bundle FHIR de type transaction
- **Flux de recherche** : Consultation des mesures stockées dans Mon Espace Santé

Toutes les requêtes doivent répondre aux exigences d'authentification et d'identification décrites dans la spécification d'appariement.

### Interactions préliminaires

Les interactions entre les partenaires et Mon Espace Santé s'organisent en trois phases préliminaires aux échanges :

1. **Phase administrative** : Référencement et contractualisation
2. **Phase de setup technique** : Connectivité, partage de secrets, certificats
3. **Appariement initial** : Consentement de l'utilisateur à l'échange de données avec le partenaire

### Documents référencés

| Nom | Description |
|-----|-------------|
| Volet mesures de santé v1.2 | Spécifications techniques d'alimentation et de consultation des mesures de santé |
| Spécifications d'interopérabilité au format Guide d'implémentation v3.0 | Spécifications techniques publiées sous forme d'Implementation Guide |

Le Document chapeau des APIs Mon espace santé peut être trouvé sur le portail de référencement à l'adresse [Référencement éditeurs (monespacesante.fr)](https://monespacesante.fr).

### Dépendances

{% lang-fragment dependency-table.xhtml %}

### Propriété intellectuelle

{% lang-fragment ip-statements.xhtml %}
