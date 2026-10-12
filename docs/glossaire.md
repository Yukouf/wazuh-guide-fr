# Glossaire simple

| Terme | Définition simple |
| --- | --- |
| Wazuh | Plateforme open source qui centralise et analyse des informations de sécurité. |
| SIEM | Gestion des informations et événements de sécurité : rassembler les journaux et aider à détecter et enquêter. |
| XDR | Détection et réponse étendues : rapprocher plusieurs sources de sécurité pour analyser les menaces et organiser la réponse. |
| Agent | Petit programme installé sur une machine pour collecter et transmettre ses informations. |
| Endpoint | Machine surveillée, par exemple un poste ou un serveur. |
| Manager / serveur | Composant Wazuh qui reçoit les données, les analyse et applique les règles. |
| Indexer | Composant qui stocke et indexe les données pour les recherches. |
| Dashboard | Interface web pour visualiser et consulter les résultats. |
| Log / journal | Trace d'un événement produit par un système ou une application. |
| Événement | Fait enregistré, par exemple une connexion ou une modification de fichier. |
| Alerte | Signal produit lorsqu'un événement correspond à une règle ; il nécessite une vérification. |
| Règle | Condition utilisée pour reconnaître un événement et lui attribuer un niveau ou un contexte. |
| Décodeur | Mécanisme qui extrait les champs utiles d'un journal. |
| Threat Hunting | Recherche méthodique d'activités suspectes dans les données disponibles. |
| Malware | Logiciel malveillant, par exemple un rançongiciel ou un cheval de Troie. |
| IOC | Indicateur de compromission : hash, domaine ou autre élément qui peut aider à reconnaître une activité malveillante. |
| Hash | Empreinte calculée à partir d'un fichier ; utile pour comparer des contenus. |
| Rootcheck | Module Wazuh qui recherche des anomalies et des signes de rootkits. |
| Rootkit | Ensemble d'outils utilisé pour cacher une présence ou conserver un accès non autorisé. |
| YARA | Outil et langage de règles servant à reconnaître des motifs dans des fichiers. |
| VirusTotal | Service de renseignement et d'analyse de fichiers et indicateurs, intégrable à Wazuh. |
| Vulnérabilité | Faiblesse pouvant être exploitée sous certaines conditions. |
| CVE | Identifiant public d'une vulnérabilité connue, généralement de forme CVE-année-numéro. |
| CVSS | Système de notation de la sévérité technique d'une vulnérabilité ; il ne représente pas à lui seul le risque métier. |
| Correctif / patch | Mise à jour destinée à corriger un problème. |
| MITRE ATT&CK | Base de connaissances sur les tactiques et techniques observées chez les attaquants. |
| Tactique | Objectif poursuivi, par exemple obtenir un accès ou conserver sa présence. |
| Technique | Méthode employée pour atteindre un objectif. |
| Sous-technique | Variante plus précise d'une technique. |
| FIM | Surveillance d'intégrité des fichiers : repérer les changements sur les fichiers surveillés. |
| SCA | Évaluation des configurations de sécurité selon des politiques et contrôles. |
| DQL | Langage de recherche utilisé dans l'interface pour filtrer les données. |
| Faux positif | Alerte dont l'analyse montre qu'elle ne correspond pas à la menace soupçonnée. |
| SOC | Équipe ou centre chargé de surveiller la sécurité et de traiter les incidents. |
| Active Response | Actions configurées pouvant être exécutées automatiquement en réponse à des alertes. |

**À retenir :** une CVE décrit une faiblesse connue ; MITRE ATT&CK décrit des comportements d'attaque. Ces deux référentiels répondent à des questions différentes.
