# Utiliser les pages Wazuh

Ce guide explique **où cliquer, quoi regarder et quoi faire ensuite**. Les boutons gardent leur nom anglais pour pouvoir les retrouver à l'écran.

## Avant de commencer

| Bouton | En français | À quoi il sert |
| --- | --- | --- |
| Dashboard | Vue d'ensemble | Voir les indicateurs et graphiques |
| Events | Événements | Lire les lignes et les détails des alertes |
| Inventory | Inventaire | Voir les logiciels et vulnérabilités concernés |
| Last 24 hours | Dernières 24 heures | Choisir la période pour les pages d'événements |
| Add filter | Ajouter un filtre | Afficher seulement une machine, un niveau ou une règle |
| Refresh | Actualiser | Appliquer la recherche et recharger les résultats |

**Pour afficher une seule machine :** cliquez sur **Add filter**. Dans **Field**, choisissez `agent.name` ; dans **Operator**, choisissez **is** ; dans **Value**, choisissez le nom de la machine. Cliquez sur **Save**, puis sur **Refresh** si nécessaire. Cette procédure a été vérifiée dans la page Events de Threat Hunting.

**Pour lire une alerte :** dans **Events**, cliquez sur le petit bouton à gauche de la ligne, nommé **Inspect document details**. Le lien portant le nom de la machine ouvre sa fiche ; il n'ouvre pas le détail de l'alerte.

| Colonne | Ce qu'elle veut dire |
| --- | --- |
| `timestamp` | Date et heure de l'événement |
| `agent.name` | Machine concernée |
| `rule.description` | Message qui explique pourquoi l'alerte existe |
| `rule.level` | Niveau utilisé pour trier les alertes |
| `rule.id` | Numéro de la règle qui a produit l'alerte |

**Si vous ne savez pas quoi décider :** notez la machine, l'heure, le message et le numéro de règle, puis transmettez ces éléments à l'équipe informatique ou sécurité par le canal interne habituel. Le graphique seul ne suffit pas pour décider de bloquer ou supprimer quelque chose.

## 1. Threat Hunting — rechercher des activités suspectes

**Objectif :** explorer les alertes collectées pour comprendre ce qui s'est passé. Le Dashboard affiche des indicateurs et graphiques ; Events permet de consulter les événements.

1. Ouvrir Threat Hunting depuis l'accueil.
2. Choisir une période correspondant au moment recherché. Last 24 hours est un point de départ.
3. Cliquer sur Events, puis utiliser Add filter pour garder la machine recherchée. La procédure est expliquée plus haut.
4. Ouvrir une ligne avec Inspect document details, le petit bouton à gauche.
5. Lire l'heure, la machine et le message. Repérer le niveau et le numéro de règle si une vérification est nécessaire.
6. Regarder les événements juste avant et après. Demander si l'opération était prévue : une connexion ou une commande peut être normale.

**Comment lire la capture :** les cartes comptent les alertes et les connexions réussies ou échouées. Le graphique de gauche montre à quels moments les alertes augmentent. Celui de droite les répartit par techniques associées. Un pic aide à choisir une heure à examiner dans Events.

**Quoi faire ensuite :** si l'activité est prévue, documenter la vérification selon la procédure de l'équipe. Si elle est inhabituelle, conserver les détails et faire examiner la machine par la personne responsable.

**Exemple fictif :** plusieurs connexions échouent sur POSTE-DEMO. Rechercher les échecs, examiner leur fréquence et vérifier si une connexion réussie suit. Une erreur de mot de passe répétée peut aussi provenir d'un service mal configuré.

Exemples DQL à adapter aux champs présents, en laissant la langue sur DQL :

```text
agent.name: "POSTE-DEMO"
rule.level >= 12
rule.groups: "authentication_failed"
agent.name: "POSTE-DEMO" and rule.level >= 12
```

Le niveau d'une règle aide au tri ; il ne remplace pas l'analyse. Si aucun résultat n'apparaît, vérifier période, filtres, état de l'agent et collecte.

## 2. Vulnerability Detection — repérer les failles connues

**Objectif :** comparer l'inventaire logiciel collecté avec les informations de vulnérabilités. Dashboard donne la répartition ; Inventory présente les résultats détaillés ; Events permet de suivre les événements de détection.

1. Ouvrir Vulnerability Detection, puis Inventory.
2. Avec Add filter, garder une machine ou une gravité. Pour la gravité, rechercher le champ `vulnerability.severity` et choisir Critical ou High dans les valeurs disponibles.
3. Lire le nom de la machine (`agent.name`), le logiciel (`package.name`), sa version (`package.version`) et le numéro de faille (`vulnerability.id`, appelé CVE).
4. Cliquer sur Inspect vulnerability details à gauche de la ligne. Lire la description et la référence de la faille.
5. Consulter l'avis de l'éditeur : vérifier quelle version corrige la faille et si le résultat s'applique vraiment au logiciel installé.
6. Faire appliquer la mise à jour selon les habitudes de l'équipe. Commencer par les cas les plus urgents : logiciel exposé, machine importante, faille exploitée ou gravité élevée.
7. Après la mise à jour, laisser l'inventaire s'actualiser puis revenir dans Inventory pour vérifier le résultat. Si la ligne reste présente, vérifier la version détectée et la date de collecte.

**Comment lire la capture :** Critical signifie critique, High élevée, Medium moyenne et Low faible. Les graphiques montrent la répartition des résultats. Ils ne donnent pas la marche à suivre pour chaque logiciel : il faut ouvrir Inventory.

**Quoi faire ensuite :** préparer une petite liste « machine / logiciel / version / CVE / correctif à vérifier » et la faire traiter par la personne responsable des mises à jour.

**Exemple fictif :** une version vulnérable d'un navigateur est détectée sur POSTE-DEMO. Vérifier la version, appliquer le correctif approuvé, puis contrôler que le résultat est actualisé.

Un total peut compter plusieurs associations entre machines, paquets et CVE. Il ne correspond pas forcément au nombre de failles uniques. Une détection basée sur l'inventaire ne constitue pas un test d'exploitation.

## 3. Malware Detection — enquêter sur les indicateurs

**Objectif :** examiner les signaux associés à des fichiers malveillants, anomalies ou outils de détection intégrés. La page observée comporte Dashboard et Events ; des filtres de groupes de règles peuvent déjà être appliqués.

1. Ouvrir Malware Detection et choisir la période.
2. Lire les filtres actifs avant d'interpréter les graphiques.
3. Cliquer sur Events, filtrer la machine concernée, puis ouvrir une ligne avec Inspect document details.
4. Lire le message et sa source. Rootcheck signale des anomalies ; YARA et VirusTotal peuvent apporter d'autres détections si ces intégrations sont configurées.
5. Noter le fichier ou l'activité concernée. Le chemin indique où se trouve le fichier ; le hash est son empreinte, lorsqu'il est disponible.
6. Faire vérifier le signal avec les outils de sécurité de l'organisation. Si une menace est confirmée, suivre sa procédure de réponse.

**Comment lire la capture :** le panneau de gauche montre quand les machines produisent des signaux ; celui de droite répartit les événements selon les groupes de règles. Ils servent à repérer un moment à examiner dans Events.

**Quoi faire ensuite :** prévenir l'équipe responsable avec les détails du signal. Ne pas lancer le fichier suspect ni le supprimer uniquement parce qu'une courbe monte.

**Exemple fictif :** un fichier déclenche une règle YARA dans un laboratoire où cette intégration est configurée. Examiner la règle correspondante et les événements liés avant de qualifier l'incident.

Rootcheck recherche des anomalies et signatures ; certains signaux peuvent être des faux positifs. FIM seul détecte des changements, pas la nature malveillante d'un fichier. YARA et VirusTotal nécessitent une intégration. Wazuh peut également analyser les journaux de Microsoft Defender ou ClamAV. L'absence de résultats dans un panneau ne prouve pas l'absence de malware ni la désactivation d'un module. [Mécanismes documentés](https://documentation.wazuh.com/current/user-manual/capabilities/malware-detection/index.html).

## 4. MITRE ATT&CK — donner du contexte à une alerte

**Objectif :** rapprocher les alertes des comportements documentés des attaquants. Le référentiel classe les tactiques (objectifs) et techniques (moyens).

1. Ouvrir MITRE ATT&CK.
2. Cliquer sur Framework pour découvrir les techniques : une tactique est l'objectif, une technique est la façon de le poursuivre.
3. Regarder Dashboard pour voir les catégories auxquelles les alertes sont associées pendant la période choisie.
4. Cliquer sur Events. Pour une technique précise, ajouter un filtre sur `rule.mitre.id` et choisir son identifiant parmi les valeurs présentes.
5. Ouvrir une alerte, lire le message et vérifier ce qui s'est vraiment passé sur la machine.

**Exemple simple :** un attaquant veut rester présent sur une machine (objectif : persistance). Il peut créer une tâche planifiée qui relance son programme (méthode). Un administrateur peut aussi créer une tâche planifiée légitime : le contexte permet de faire la différence.

**Quoi faire ensuite :** utiliser la technique pour expliquer et regrouper les faits. Vérifier les alertes et les activités liées avant de parler d'attaque.

Une commande PowerShell peut être associée à une technique sans être malveillante. Le rattachement repose sur les règles ; il ne démontre ni une compromission ni une couverture complète du référentiel.

## 5. File Integrity Monitoring — suivre les changements

La surveillance d'intégrité compare l'état des fichiers surveillés : contenu, permissions, propriétaire ou attributs selon la configuration. Ouvrir la page, filtrer la période et l'agent, puis examiner les événements de création, modification ou suppression. Identifier le chemin et la nature du changement ; comparer avec une opération de maintenance prévue. Les informations sur l'utilisateur responsable et le détail du contenu dépendent des options configurées.

**En pratique :** ouvrir la page → choisir la machine et la période → ouvrir le changement → regarder le fichier et ce qui a changé → demander si la modification était prévue. Si elle ne l'était pas, faire examiner le changement par l'équipe.

**Exemple fictif :** un fichier de configuration change hors d'une fenêtre de maintenance. Vérifier qui a effectué l'opération et si elle est autorisée. Seuls les chemins configurés et effectivement collectés sont couverts.

## 6. Configuration Assessment — examiner les contrôles

SCA vérifie des paramètres de sécurité à partir de politiques. Sélectionner un agent, ouvrir une politique et consulter les contrôles échoués, leur justification et les recommandations disponibles. Évaluer l'impact d'une correction avant de l'appliquer, puis vérifier au scan suivant. Le score dépend de la politique et des contrôles évalués ; il ne constitue pas à lui seul une mesure complète de sécurité.

**En pratique :** choisir la machine → ouvrir sa politique de contrôle → lire un résultat Failed (échoué) → lire la recommandation → faire valider et appliquer la correction → vérifier au contrôle suivant. Passed signifie réussi.

## 7. IT Hygiene et agents — connaître le parc

IT Hygiene permet d'examiner les inventaires système et logiciel ainsi que les données de processus et de réseau disponibles. Les agents permettent de comprendre quelles machines remontent leurs informations. Un agent déconnecté ne garantit pas une collecte récente : vérifier la dernière activité et la connexion avant d'interpréter l'absence d'alertes.

## 8. Réponse et conformité

Active Response peut exécuter des actions configurées en réaction à certaines alertes, par exemple un blocage temporaire. Ce guide n'active ni ne déclenche ces actions : une réponse automatique doit être conçue et validée pour l'environnement.

Les pages PCI DSS, GDPR, HIPAA, NIST 800-53 et TSC regroupent les alertes associées à des exigences. Elles fournissent des éléments pour les audits ; respecter une réglementation exige aussi des procédures, des preuves et une évaluation humaine.

## Si la page est vide ou si vous êtes perdu

1. Vérifier la période. Un événement plus ancien que les dernières 24 heures ne sera pas affiché avec cette sélection.
2. Vérifier les filtres actifs. Un filtre de machine ou de règle peut cacher les autres résultats.
3. Cliquer sur Refresh.
4. Vérifier que l'agent est connecté et remonte des informations récentes.
5. Si cela ne suffit pas, faire vérifier la collecte ou l'intégration par l'administrateur Wazuh.

**Pour s'entraîner :** utiliser une machine de laboratoire et des événements autorisés. Les captures du dépôt servent à présenter les commandes ; elles ne remplacent pas la lecture des détails dans votre interface.
