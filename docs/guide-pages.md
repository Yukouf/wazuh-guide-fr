# Utiliser les pages Wazuh

## 1. Threat Hunting — rechercher des activités suspectes

**Objectif :** explorer les alertes collectées pour comprendre ce qui s'est passé. Le Dashboard affiche des indicateurs et graphiques ; Events permet de consulter les événements.

1. Ouvrir Threat Hunting depuis l'accueil.
2. Choisir une période correspondant au moment recherché. Last 24 hours est un point de départ.
3. Utiliser Add filter pour sélectionner un agent ou une règle ; cliquer sur Refresh pour appliquer la recherche.
4. Passer à Events et ouvrir un événement.
5. Examiner l'heure, l'agent, `rule.id`, `rule.level`, `rule.description` et les données du journal disponibles.
6. Comparer les événements avant et après celui étudié. Vérifier avec le contexte de la machine avant de conclure.

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
2. Utiliser Add filter pour une machine, un logiciel, une sévérité ou une CVE.
3. Examiner `agent.name`, `package.name`, `package.version`, `vulnerability.severity` et `vulnerability.id`.
4. Ouvrir Inspect vulnerability details pour lire les informations disponibles et la référence de la faille.
5. Vérifier l'applicabilité et les correctifs avec l'avis officiel de l'éditeur.
6. Prioriser selon la gravité, l'exposition, l'exploitation connue et la criticité de la machine.
7. Après correction, attendre l'actualisation de l'inventaire et vérifier le résultat.

**Exemple fictif :** une version vulnérable d'un navigateur est détectée sur POSTE-DEMO. Vérifier la version, appliquer le correctif approuvé, puis contrôler que le résultat est actualisé.

Un total peut compter plusieurs associations entre machines, paquets et CVE. Il ne correspond pas forcément au nombre de failles uniques. Une détection basée sur l'inventaire ne constitue pas un test d'exploitation.

## 3. Malware Detection — enquêter sur les indicateurs

**Objectif :** examiner les signaux associés à des fichiers malveillants, anomalies ou outils de détection intégrés. La page observée comporte Dashboard et Events ; des filtres de groupes de règles peuvent déjà être appliqués.

1. Ouvrir Malware Detection et choisir la période.
2. Lire les filtres actifs avant d'interpréter les graphiques.
3. Passer à Events, filtrer l'agent concerné, puis ouvrir une alerte.
4. Identifier le mécanisme à l'origine du signal : Rootcheck, règle, YARA, VirusTotal ou journal d'un antivirus selon la configuration.
5. Examiner le chemin, le hash, la règle et les éléments du journal lorsqu'ils existent.
6. Confirmer le signal avec le contexte et les outils de sécurité autorisés, puis suivre la procédure de réponse de l'organisation.

**Exemple fictif :** un fichier déclenche une règle YARA dans un laboratoire où cette intégration est configurée. Examiner la règle correspondante et les événements liés avant de qualifier l'incident.

Rootcheck recherche des anomalies et signatures ; certains signaux peuvent être des faux positifs. FIM seul détecte des changements, pas la nature malveillante d'un fichier. YARA et VirusTotal nécessitent une intégration. Wazuh peut également analyser les journaux de Microsoft Defender ou ClamAV. L'absence de résultats dans un panneau ne prouve pas l'absence de malware ni la désactivation d'un module. [Mécanismes documentés](https://documentation.wazuh.com/current/user-manual/capabilities/malware-detection/index.html).

## 4. MITRE ATT&CK — donner du contexte à une alerte

**Objectif :** rapprocher les alertes des comportements documentés des attaquants. Le référentiel classe les tactiques (objectifs) et techniques (moyens).

1. Ouvrir MITRE ATT&CK.
2. Utiliser Framework pour parcourir le référentiel et Intelligence pour consulter le contexte proposé.
3. Examiner Dashboard pour les alertes associées sur une période.
4. Ouvrir Events et filtrer une technique à partir de son identifiant présent dans `rule.mitre.id`.
5. Revenir au journal et à la machine pour vérifier ce qui est effectivement observé.

Une commande PowerShell peut être associée à une technique sans être malveillante. Le rattachement repose sur les règles ; il ne démontre ni une compromission ni une couverture complète du référentiel.

## 5. File Integrity Monitoring — suivre les changements

La surveillance d'intégrité compare l'état des fichiers surveillés : contenu, permissions, propriétaire ou attributs selon la configuration. Ouvrir la page, filtrer la période et l'agent, puis examiner les événements de création, modification ou suppression. Identifier le chemin et la nature du changement ; comparer avec une opération de maintenance prévue. Les informations sur l'utilisateur responsable et le détail du contenu dépendent des options configurées.

**Exemple fictif :** un fichier de configuration change hors d'une fenêtre de maintenance. Vérifier qui a effectué l'opération et si elle est autorisée. Seuls les chemins configurés et effectivement collectés sont couverts.

## 6. Configuration Assessment — examiner les contrôles

SCA vérifie des paramètres de sécurité à partir de politiques. Sélectionner un agent, ouvrir une politique et consulter les contrôles échoués, leur justification et les recommandations disponibles. Évaluer l'impact d'une correction avant de l'appliquer, puis vérifier au scan suivant. Le score dépend de la politique et des contrôles évalués ; il ne constitue pas à lui seul une mesure complète de sécurité.

## 7. IT Hygiene et agents — connaître le parc

IT Hygiene permet d'examiner les inventaires système et logiciel ainsi que les données de processus et de réseau disponibles. Les agents permettent de comprendre quelles machines remontent leurs informations. Un agent déconnecté ne garantit pas une collecte récente : vérifier la dernière activité et la connexion avant d'interpréter l'absence d'alertes.

## 8. Réponse et conformité

Active Response peut exécuter des actions configurées en réaction à certaines alertes, par exemple un blocage temporaire. Ce guide n'active ni ne déclenche ces actions : une réponse automatique doit être conçue et validée pour l'environnement.

Les pages PCI DSS, GDPR, HIPAA, NIST 800-53 et TSC regroupent les alertes associées à des exigences. Elles fournissent des éléments pour les audits ; respecter une réglementation exige aussi des procédures, des preuves et une évaluation humaine.
