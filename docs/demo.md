# Présenter Wazuh en 10 minutes

| Temps | Écran ou support | Message à expliquer |
| --- | --- | --- |
| 0–1 min | README et architecture | Les machines remontent des données, Wazuh les analyse et un analyste examine les résultats. |
| 1–3 min | Threat Hunting | Choisir une période, ouvrir Events, filtrer une machine et expliquer comment lire une alerte. |
| 3–5 min | Vulnerability Detection | Ouvrir Inventory, montrer les colonnes et expliquer la différence entre faille connue et exploitation. |
| 5–7 min | Malware Detection | Expliquer les sources possibles et pourquoi une alerte nécessite une confirmation. |
| 7–8 min | MITRE ATT&CK | Distinguer objectif et méthode, puis montrer le passage du référentiel aux événements. |
| 8–9 min | FIM et SCA | Illustrer les changements de fichiers et les contrôles de configuration. |
| 9–10 min | Glossaire | Revenir sur SIEM, agent, CVE et MITRE ATT&CK, puis répondre aux questions. |

Utiliser les captures publiques du README ou un laboratoire dédié avec des données fictives. Pour une démonstration en direct, préparer la période et les filtres et vérifier que les informations affichées peuvent être partagées. Les exemples du [parcours débutant](parcours-debutant.md) peuvent servir de support aux questions.

## Exemple d'explication orale

« Wazuh est un point central pour surveiller la sécurité. Threat Hunting aide à comprendre les événements. Vulnerability Detection montre les logiciels associés à des failles connues. Malware Detection rassemble des signaux à examiner. MITRE ATT&CK nous aide à nommer les comportements que certaines règles détectent. L'analyste vérifie ensuite le contexte et décide de la réponse. »

## Questions fréquentes

**Est-ce que Wazuh bloque tout automatiquement ?** Les actions de réponse dépendent de la configuration ; visualiser une alerte ne signifie pas qu'un blocage a eu lieu.

**Une alerte rouge signifie-t-elle une attaque certaine ?** Il faut vérifier le journal, le contexte et les événements liés.

**Une page vide signifie-t-elle que tout va bien ?** Vérifier les filtres, la période et la collecte avant de conclure.

**Est-ce un antivirus ?** Wazuh peut intégrer différents mécanismes de détection et analyser des journaux d'antivirus ; ces fonctions dépendent de leur configuration.
