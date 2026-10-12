# Glossaire simple

| Terme | Définition simple |
| --- | --- |
| Wazuh | Plateforme open source qui centralise et analyse des informations de sécurité. |
| SIEM | Security Information and Event Management : centraliser et analyser des journaux pour détecter des signaux et faciliter les enquêtes. |
| XDR | Extended Detection and Response : rapprocher des données de plusieurs sources pour détecter des menaces et faciliter la réponse. Les actions disponibles dépendent des intégrations et de la configuration. |
| Agent | Petit programme installé sur une machine pour collecter et transmettre ses informations. |
| Endpoint | Machine surveillée, par exemple un poste ou un serveur. |
| Manager / serveur | Le manager est le composant d'analyse du serveur Wazuh : il reçoit les données des agents et applique les règles. |
| Indexer | Composant qui stocke et indexe les données pour les recherches. |
| Dashboard | Interface web pour visualiser et consulter les résultats. |
| Log / journal | Un journal contient des traces produites par un système ou une application. Un log peut désigner une de ces traces. |
| Événement | Fait observé et enregistré, par exemple une connexion ou une modification de fichier. |
| Alerte | Résultat d'une détection qui attire l'attention sur un événement ou un ensemble d'événements. Elle doit être examinée. |
| Incident | Situation de sécurité identifiée après analyse et qui nécessite un traitement. Toute alerte n'est pas un incident. |
| Règle | Condition utilisée pour reconnaître un événement et lui attribuer un niveau ou un contexte. |
| Décodeur | Mécanisme qui extrait les champs utiles d'un journal. |
| Threat Hunting | Recherche proactive de menaces, souvent à partir d'une hypothèse, dans les données disponibles. Elle peut aller au-delà des alertes déjà connues. |
| Malware | Logiciel malveillant, par exemple un rançongiciel ou un cheval de Troie. |
| IOC | Indicator of Compromise : élément associé à une activité malveillante, par exemple un hash ou un domaine connu. Sa présence doit être interprétée avec le contexte. |
| Hash | Empreinte calculée à partir d'un fichier ; utile pour comparer des contenus. |
| Rootcheck | Module Wazuh qui recherche des anomalies et des signes de rootkits. |
| Rootkit | Ensemble d'outils utilisé pour cacher une présence ou conserver un accès non autorisé. |
| YARA | Outil et langage de règles servant à reconnaître des motifs dans des fichiers. |
| VirusTotal | Service de renseignement et d'analyse de fichiers et indicateurs, intégrable à Wazuh. |
| Vulnérabilité | Faiblesse pouvant être exploitée sous certaines conditions. |
| CVE | Common Vulnerabilities and Exposures : programme de référencement des vulnérabilités. Un identifiant CVE, de forme CVE-année-numéro, permet de retrouver la fiche d'une vulnérabilité. |
| CVSS | Common Vulnerability Scoring System : système de notation de la sévérité des vulnérabilités. Le score de base, de 0 à 10, mesure la sévérité technique ; il ne suffit pas à mesurer le risque pour l'organisation. |
| Sévérité | Gravité attribuée à un résultat selon un système de classement. Elle aide à comparer les résultats. |
| Risque | Possibilité d'un dommage dans un contexte donné : exposition de la machine, conditions d'exploitation et conséquences pour l'organisation. |
| Niveau de règle | Classement attribué par une règle Wazuh (`rule.level`). Il aide au tri des alertes et n'est pas un score CVSS. |
| Correctif / patch | Mise à jour destinée à corriger un problème. |
| MITRE ATT&CK | Base de connaissances sur les tactiques et techniques des attaquants, fondée sur des observations réelles. ATT&CK signifie Adversarial Tactics, Techniques, and Common Knowledge. |
| Tactique | Objectif poursuivi, par exemple obtenir un accès ou conserver sa présence. |
| Technique | Méthode employée pour atteindre un objectif. |
| Sous-technique | Variante plus précise d'une technique. |
| FIM | Surveillance d'intégrité des fichiers : repérer les changements sur les fichiers surveillés. |
| SCA | Évaluation des configurations de sécurité selon des politiques et contrôles. |
| DQL | Dashboards Query Language : langage de filtrage des résultats dans OpenSearch Dashboards. Il est différent du Wazuh Query Language (WQL) utilisé dans certains outils et API Wazuh. |
| Faux positif | Détection qui signale à tort la menace recherchée. Une activité autorisée correctement reconnue par une règle n'est pas forcément un faux positif. |
| SOC | Équipe ou centre chargé de surveiller la sécurité et de traiter les incidents. |
| Active Response | Actions configurées pouvant être exécutées automatiquement en réponse à des alertes. |
| Syscollector | Module de l'agent qui recueille l'inventaire du système et des logiciels, notamment pour la détection des vulnérabilités. |
| CTI | Cyber Threat Intelligence : informations sur les menaces et vulnérabilités utiles à leur analyse. |
| Remédiation | Correction d'un problème, par exemple installer un correctif ou corriger une configuration. |
| Mesure compensatoire | Protection qui réduit le risque lorsqu'une correction immédiate n'est pas possible. Elle doit être choisie selon le contexte. |

**À retenir :** une fiche CVE décrit une vulnérabilité, son identifiant permet de la retrouver ; MITRE ATT&CK décrit des comportements d'attaque. Une alerte est un signal, et un incident est une situation qualifiée après analyse.

## Sources pour aller plus loin

- [Composants Wazuh](https://documentation.wazuh.com/current/getting-started/components/index.html)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [Programme CVE](https://www.cve.org/)
- [CVSS : sévérité et risque, FIRST](https://www.first.org/cvss/user-guide.html)
- [Langage DQL, OpenSearch](https://docs.opensearch.org/latest/dashboards/dql/)
