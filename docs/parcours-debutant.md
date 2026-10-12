# Premier parcours : du résultat à la décision

Ce parcours sert à comprendre Wazuh sans devoir connaître tous les termes techniques. Il utilise des exemples entièrement fictifs ; il ne décrit pas le parc présenté dans les captures.

## Ce qu'il faut pour suivre le guide

Une interface Wazuh accessible avec un compte autorisé à consulter les pages, une machine surveillée et des données récentes. Les résultats dépendent de la collecte et des modules configurés. Le compte utilisé pour lire les résultats n'a pas besoin de permettre des modifications d'administration.

Ce dépôt explique l'utilisation de l'interface ; il ne déploie pas Wazuh et ne configure pas les intégrations. Pour installer un environnement de démonstration, consulter le [guide officiel de démarrage](https://documentation.wazuh.com/current/quickstart.html).

## 1. Lire une alerte dans Threat Hunting

**Question :** « Pourquoi cette machine a-t-elle produit une alerte ? »

Ouvrir Threat Hunting → choisir la période → ouvrir Events → filtrer `agent.name` → ouvrir une ligne avec Inspect document details.

| Élément fictif | Ce qu'il faut comprendre |
| --- | --- |
| Machine : POSTE-DEMO | La machine sur laquelle chercher le contexte |
| Heure : 09:15 | Le moment à comparer avec les autres événements |
| Message : échecs d'authentification répétés | Le signal à vérifier, pas une conclusion sur sa cause |
| Connexion réussie peu après | Un fait supplémentaire à analyser |

Demander si un utilisateur a oublié son mot de passe ou si un service utilise d'anciens identifiants. Vérifier si la connexion réussie était attendue. Si la situation reste inexpliquée, transmettre les faits à l'équipe responsable. Si l'activité est légitime, noter la vérification ; une adaptation de la règle peut être étudiée par l'administrateur si les alertes se répètent.

## 2. Préparer une correction de vulnérabilité

**Question :** « Quel logiciel faut-il vérifier et mettre à jour ? »

Ouvrir Vulnerability Detection → Inventory → sélectionner une machine et une sévérité → ouvrir Inspect vulnerability details.

| Information à relever | Exemple fictif |
| --- | --- |
| Machine | POSTE-DEMO |
| Logiciel et version | Navigateur de démonstration, version installée |
| CVE | Identifiant réellement présent dans votre ligne, à relever |
| Correctif | Version corrigée indiquée dans l'avis de l'éditeur |
| Responsable | Équipe qui gère les mises à jour |
| Vérification finale | Version mise à jour et inventaire récent |

La sévérité aide au tri. Il faut aussi savoir si la machine est exposée, si elle est importante pour l'activité et si la faille est exploitée. Faire appliquer la correction, puis vérifier l'inventaire. Si la mise à jour ne peut pas être appliquée, faire décider d'une protection temporaire et d'une date de suivi.

## 3. Comprendre un signal Malware Detection

**Question :** « Cette anomalie indique-t-elle vraiment un logiciel malveillant ? »

Ouvrir Malware Detection → choisir la période → Events → ouvrir le signal.

Lire la machine, l'heure, le message, le fichier concerné et la source de la détection lorsqu'ils sont disponibles. Une anomalie Rootcheck et un résultat d'antivirus ne disent pas exactement la même chose. Faire vérifier le signal avec les outils de sécurité disponibles et suivre la procédure de l'organisation si une menace est confirmée.

Le graphique indique quand enquêter. Il ne dit pas, à lui seul, quel fichier supprimer ni quelle machine isoler.

## 4. Expliquer le contexte avec MITRE ATT&CK

**Question :** « Comment nommer le comportement observé ? »

Ouvrir MITRE ATT&CK → Framework pour le contexte → Events pour les alertes associées.

Par exemple, la sous-technique [PowerShell, T1059.001](https://attack.mitre.org/techniques/T1059/001/) décrit l'usage de PowerShell. Une règle associée à cette sous-technique peut signaler un comportement à examiner, mais PowerShell sert aussi à l'administration normale. Lire la commande et son contexte lorsqu'ils sont disponibles avant de conclure.

## Garder une trace utile

Dans un outil interne autorisé, noter : **machine, heure, message, source, vérification effectuée, décision et personne chargée du suivi**. Pour une vulnérabilité, ajouter le logiciel, sa version et la CVE. Partager seulement les éléments nécessaires avec les personnes responsables.

Après une correction, revenir dans Wazuh et vérifier avec des données récentes. La présence ou l'absence d'une alerte n'est pas, à elle seule, une validation complète de la sécurité de la machine.
