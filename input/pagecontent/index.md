<p style="padding: 5px; border-radius: 5px; border: 2px solid maroon; background: #ffffe6; width: 65%">
<b>Brief description of this Implementation Guide</b><br>
[Add a brief description of this IG in English]
</p>

{% if site.data.info.releaselabel == 'ci-build' %}
<div style="width: 65%">
    <blockquote class="stu-note">
    <p>Cet Implementation Guide n'est pas la version courante, il s'agit de la version en intégration continue soumise à des changements fréquents uniquement destinée à suivre les travaux en cours. La version courante sera accessible via l'URL canonique suite à la première release : http://interop.esante.gouv.fr/ig/fhir/[code - ig]</p>
    </blockquote>
</div>
{% endif %}



{% if site.data.info.releaselabel == 'public-comment' %}
<div style="width: 65%">
<blockquote class="stu-note">
<p>
  <b>Attention !</b>
  <br>
 Cet Implementation Guide est actuellement en concertation. La version courante est accessible à l'adresse : http://interop.esante.gouv.fr/ig/fhir/[code - ig]
</p>
</blockquote>
</div>
{% endif %}

Ce guide d'implémentation est un test pour mettre MonEspaceSanté au format IG, et également un test pour mettre plusieurs versions du même package en dépendance.

### Introduction

Définir ici de quoi parle l'IG (En termes non expert, compréhensible par un patient). Rajouter également les détails techniques sur le contexte et le besoin de cet IG

Les principales sections de l'IG  sont :

* Le contexte de l'IG, quelle problématique il résout
* Ce que les Implémenteurs doivent mettre en place
* Un onglet "Ressources de conformité" pour s'assurer d'un schéma global entre tous les IGs

### Périmètre du projet

Définir en quelques lignes quel est le périmètre du projet

Toujours laisser l'onglet "Ressources de conformité" pour s'assurer d'une cohérence globales entre tous les IGs

### Auteurs et contributeurs (optionnel)

| Role  | Nom | Organisation | Contact |
| --- | --- | --- | --- |
| **Primary Editor** | Prenom Nom | Agence du Numérique en Santé | prenom.nom@address.email |

### Dépendances

{% lang-fragment dependency-table.xhtml %}

### Propriété intellectuelle

{% lang-fragment ip-statements.xhtml %}
