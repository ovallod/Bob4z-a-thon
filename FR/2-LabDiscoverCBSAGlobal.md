# Lab : Analyse Complète de l'Application CBSA avec IBM Bob Premium Package pour Z

## Vue d'ensemble du Lab

Ce lab vous guide à travers une analyse complète de l'application **CICS Banking Sample Application (CBSA)** en utilisant **Bob pour Z**,
l'assistant IA spécialisé pour les systèmes mainframe IBM Z. 
En complément du **LabDiscoverCBSA**, ce lab intègre en plus la partie front-end (Java, React, API,....).
Vous apprendrez à utiliser différents modes de Bob et à formuler des prompts efficaces pour obtenir des analyses détaillées, de la documentation et des diagrammes d'architecture.

---

## Prérequis

- ✅ VSCode avec l'extension **IBM Bob Premium Package for Z** installée
- ✅ Projet CBSA cloné localement (cf **LabDiscoverCBSA**)
- ✅ Accès au mode **Z Code** de Bob
- ✅ Connaissance de base de COBOL, JCL et architecture mainframe (recommandé mais non obligatoire)

---

## Durée Estimée

**Temps total : 2-3 heures**

---

## Table des Matières

0. [Préparation 0 : Récupération du font-end de l'application](#preparation-0)  
1. [Exercice 1 : Initialisation et Création du Fichier AGENTS.md](#exercice-1)
2. [Exercice 2 : Génération du Dictionnaire de Données](#exercice-2)
3. [Exercice 3 : Inventaire des Programmes COBOL](#exercice-3)
4. [Exercice 4 : Inventaire du Frontend](#exercice-4)
5. [Exercice 5 : Diagrammes d'Architecture](#exercice-5)
6. [Exercice 6 : Analyse Fonctionnelle - Transfert Local](#exercice-6)
7. [Exercice 7 : Guide Utilisateur](#exercice-7)
8. [Exercice 8 : Analyse Technique - Credit Score](#exercice-8)

---



<a name="Préparation-0"></a>
## Préparation 0 : Récupération du font-end de l'application

## 🎯 Objectif

Récupérer le code source de la partie front-end de l'application CBSA depuis GitHub et préparer le workspace pour le lab.

### 🔧 Mode Bob à Utiliser

**Mode : 💻 Code**

Le mode Code permet d'exécuter des commandes système et de manipuler des fichiers.

### 📝 Contexte

Avant de commencer l'analyse, vous devez récupérer le code source de l'application CBSA depuis le repository GitHub officiel. Nous allons utiliser Bob pour automatiser cette préparation. 
Ouvrir Bob, cliquer sur le menu **File>Open Folder** et choisissez le répertoire ~/CBSA.


### 💬 Prompt Bob 

```
Récupère les répertoires nommés "src/bank-application-frontend",  "src/webui", "src/Z-OS-Connect-Customer-Services-Interface", "src/Z-OS-Connect-Payment-Interface", "src/Z-OS-Connect-Payment-Interface", et  "src/zosconnect_artefacts" du repository GitHub https://github.com/cicsdev/cics-banking-sample-application-cbsa.git et place les dans ce workspace.
```

### ✅ Résultat Attendu 

Bob exécute les commandes suivantes :

```bash
# Cloner le repository dans un répertoire temporaire
rm -rf /tmp/cbsa-temp && git clone --depth 1 --filter=blob:none --sparse https://github.com/cicsdev/cics-banking-sample-application-cbsa.git /tmp/cbsa-temp
cd /tmp/cbsa-temp && git sparse-checkout set src/bank-application-frontend src/webui src/Z-OS-Connect-Customer-Services-Interface src/Z-OS-Connect-Payment-Interface src/zosconnect_artefacts

mkdir -p ./src && cp -r /tmp/cbsa-temp/src/bank-application-frontend /tmp/cbsa-temp/src/webui /tmp/cbsa-temp/src/Z-OS-Connect-Customer-Services-Interface /tmp/cbsa-temp/src/Z-OS-Connect-Payment-Interface /tmp/cbsa-temp/src/zosconnect_artefacts ./src/

```

**Console de sortie** :
```
Les 5 répertoires suivants ont été récupérés depuis le repository GitHub et placés dans le workspace :
1.	bank-application-frontend/ - Application frontend bancaire
2.	webui/ - Interface web utilisateur
3.	Z-OS-Connect-Customer-Services-Interface/ - Interface z/OS Connect pour les services clients
4.	Z-OS-Connect-Payment-Interface/ - Interface z/OS Connect pour les paiements
5.	zosconnect_artefacts/ - Artefacts z/OS Connect


```



### 🎓 Ce que vous apprenez

- **Automatisation** : Bob peut exécuter des commandes Git et système
- **Préparation de workspace** : Bob peut organiser les fichiers pour le lab
- **Vérification** : Bob peut valider que tout est en place
- **Gain de temps** : 5 minutes au lieu de 15-20 minutes manuellement

### ✅ Prérequis Techniques

Avant de commencer le lab, assurez-vous d'avoir :

- **Bob** installé avec l'extension **IBM Z Open Editor**
- **Bob Premium for Z** activé dans Bob
- **Git** installé sur votre système
- **Accès Internet** pour cloner le repository

### 🎯 Vous êtes prêt !

Une fois le workspace préparé avec Bob, si vous avez déjà fait le LabDicoverCBSA dans cet espace de travail,  vous pouvez commencer directement à <a name="exercice-4">l'exercice 4 Inventaire du Frontend</a>.
Sinon commencez à l'Exercice 1. 

<a name="exercice-1"></a>
## Exercice 1 : Initialisation et Création du Fichier AGENTS.md


### Objectif
Créer un fichier AGENTS.md qui documente la structure du projet, les commandes de build, les standards de codage et les emplacements clés pour guider Bob dans ses futures analyses.

### Mode Bob à Utiliser
🧰 **Z Code**

### Prompt Recommandé
```
/init
```

### Ce que Bob va Faire
1. Analyser la structure complète du projet
2. Détecter les langages utilisés (COBOL, JCL, Java, etc.)
3. Identifier les commandes de build (Maven, scripts shell)
4. Localiser le dictionnaire de données (bobz/DD.json)
5. Mapper les programmes COBOL à leur documentation technique
6. Créer le fichier AGENTS.md avec toutes ces informations

### Résultat Attendu
**Fichier créé :** `AGENTS.md`

**Contenu attendu :**
- Type de workspace (IBM Enterprise COBOL for z/OS)
- Langages détectés (COBOL, JCL, BMS, Java 17)
- Commandes de build (build.sh, Maven)
- Structure des répertoires
- Emplacement du dictionnaire de données
- Mapping des programmes COBOL vers la documentation
- Règles de documentation (langue française par défaut)

### Validation
✅ Le fichier AGENTS.md existe à la racine du projet  
✅ Il contient une section "Workspace Type"  
✅ Il contient une section "Build Commands"  
✅ Il contient une table de mapping COBOL → Documentation  
✅ Il mentionne l'emplacement du dictionnaire de données

### Temps Estimé
⏱️ 5-10 minutes

---

<a name="exercice-2"></a>
## Exercice 2 : Génération du Dictionnaire de Données

### Objectif
Créer un dictionnaire de données pour documenter les variables COBOL avec des descriptions en français, facilitant la compréhension du code mainframe.

### Mode Bob à Utiliser
🧰 **Z Code**

### Prompt Recommandé
```
Crée un dictionnaire de données pour le programme BNKMENU
```

### Ce que Bob va Faire
1. Vérifier si un dictionnaire existe déjà
2. Scanner le programme COBOL BNKMENU.cbl
3. Extraire les variables les plus importantes (top 15)
4. Générer des descriptions en français pour chaque variable
5. Créer le fichier bobz/DD.json
6. Mettre à jour AGENTS.md avec l'emplacement du dictionnaire

### Résultat Attendu
**Fichier créé :** `bobz/DD.json`

**Contenu attendu :**
```json
{
  "version": "2.0.0",
  "entries": [
    {
      "name": "COMM-EYE",
      "type": "variable",
      "shortDescription": "Communication Eyecatcher",
      "longDescription": "Identifiant de contrôle pour la zone de communication...",
      "origin": "AI",
      "scope": [{"programName": "BNKMENU"}]
    },
    ...
  ]
}
```

**Nombre d'entrées :** 15 variables documentées

### Validation
✅ Le fichier bobz/DD.json existe  
✅ Il contient au moins 15 entrées  
✅ Chaque entrée a une description courte et longue en français  
✅ Le champ "scope" contient "BNKMENU"  
✅ AGENTS.md a été mis à jour avec l'emplacement du dictionnaire

### Temps Estimé
⏱️ 10-15 minutes

---

<a name="exercice-3"></a>
## Exercice 3 : Inventaire des Programmes COBOL

### Objectif
Créer un inventaire complet de tous les programmes COBOL avec leurs dépendances, classifications et relations.

### Mode Bob à Utiliser
🧰 **Z Code**

### Prompt Recommandé
```
Fais l'inventaire de tous les programmes COBOL
```

### Ce que Bob va Faire
1. Scanner tous les programmes COBOL (29 programmes)
2. Analyser les dépendances (copybooks, tables Db2, fichiers VSAM)
3. Classifier les programmes (BMS, services, utilitaires, batch)
4. Créer des matrices de dépendances
5. Générer un arbre de dépendances
6. Documenter chaque programme avec son rôle

### Résultat Attendu
**Fichier créé :** `docs/COBOL_INVENTORY.md`

**Contenu attendu :**
- Vue d'ensemble (29 programmes)
- Classification par type :
  - Programmes BMS (11)
  - Programmes de services (13)
  - Programmes utilitaires (4)
  - Programme batch (1)
- Dépendances détaillées pour chaque programme :
  - Copybooks utilisés
  - Tables Db2 accédées (READ/WRITE)
  - Fichiers VSAM accédés
  - Programmes appelés
- Matrices de dépendances
- Arbre de dépendances
- Documentation détaillée par programme

### Validation
✅ Le fichier docs/COBOL_INVENTORY.md existe  
✅ Il liste les 29 programmes COBOL  
✅ Chaque programme a ses dépendances documentées  
✅ Les types d'accès (READ/WRITE) sont spécifiés  
✅ Les matrices de dépendances sont présentes

### Temps Estimé
⏱️ 15-20 minutes

---

<a name="exercice-4"></a>
## Exercice 4 : Inventaire du Frontend

### Objectif
Documenter l'architecture frontend complète incluant les APIs REST, les modèles JSON et les couches d'accès aux données.

### Mode Bob à Utiliser
🧰 **Z Code**

### Prompt Recommandé
```
faire l'inventaire du front end
```

### Ce que Bob va Faire
1. Analyser les ressources REST JAX-RS (5 ressources)
2. Documenter tous les endpoints avec méthodes HTTP
3. Analyser les modèles JSON (13 classes)
4. Documenter la couche d'accès aux données (8 classes)
5. Identifier les interfaces COBOL (8 classes)
6. Créer une documentation structurée complète

### Résultat Attendu
**Fichier créé :** `docs/FRONTEND_INVENTORY.md`

**Contenu attendu :**

**1. Ressources REST (5) :**
- AccountsResource : 5 endpoints
- CustomerResource : 5 endpoints
- ProcessedTransactionResource : 3 endpoints
- CompanyNameResource : 1 endpoint
- SortCodeResource : 1 endpoint

**2. Modèles JSON (13) :**
- AccountJSON, DebitCreditAccountJSON, TransferLocalJSON
- CustomerJSON
- ProcessedTransactionJSON (6 variantes)
- CreditScore, CreditScoreCICS540

**3. Couche d'accès aux données (8) :**
- Account.java, AccountList.java (Db2)
- Customer.java, CustomerList.java (VSAM)
- GetUserSortCode.java
- HBankDataAccess.java

**4. Interfaces COBOL (8) :**
- CRECUST.java, CUSTOMER.java, PROCTRAN.java
- GetCompany.java, GetSortCode.java
- NewAccountNumber.java, NewCustomerNumber.java
- CustomerControl.java

### Validation
✅ Le fichier docs/FRONTEND_INVENTORY.md existe  
✅ Les 5 ressources REST sont documentées avec tous leurs endpoints  
✅ Les 13 modèles JSON sont listés avec leurs attributs  
✅ Les 8 classes d'accès aux données sont documentées  
✅ Les 8 interfaces COBOL sont listées  
✅ Les patterns d'architecture sont expliqués

### Temps Estimé
⏱️ 15-20 minutes

---

<a name="exercice-5"></a>
## Exercice 5 : Diagrammes d'Architecture

### Objectif
Créer des diagrammes Draw.io visualisant l'architecture globale et l'architecture détaillée du frontend.

### Mode Bob à Utiliser
🧰 **Z Code**

### Exercice 5A : Diagramme d'Architecture Globale

#### Prompt Recommandé
```
générer un diagramme global (en draw.io) intégrant le front-end et le backend en distinguant les différentes couches de l'application
```

#### Résultat Attendu
**Fichier créé :** `docs/CBSA_Architecture_Diagram.drawio`

**Contenu attendu :**
- 5 couches distinctes avec codes couleur :
  1. **Couche Présentation** (Bleu) : BMS 3270, Carbon React UI, Spring Boot UI, Mobile
  2. **Couche API REST** (Jaune) : 5 ressources JAX-RS, z/OS Connect
  3. **Couche Logique Métier** (Rose) : 29 programmes COBOL
  4. **Couche Accès Données** (Violet) : Db2, VSAM, Interfaces COBOL
  5. **Couche Stockage** (Vert) : Tables Db2, Fichiers VSAM, Maps BMS
- Flèches montrant les flux de données entre couches
- Légende complète
- Notes techniques

#### Validation
✅ Le fichier s'ouvre correctement dans Draw.io  
✅ Les 5 couches sont visibles et distinctes  
✅ Les flux de données sont représentés par des flèches  
✅ La légende est présente et complète

### Exercice 5B : Diagramme Frontend Détaillé

#### Prompt Recommandé
```
fais une diagramme détaillé de la partie front end
```

#### Résultat Attendu
**Fichier créé :** `docs/CBSA_Frontend_Detailed_Diagram.drawio`

**Contenu attendu :**
- 5 couches avec détails complets :
  1. **Client** : 4 types d'interfaces
  2. **API REST** : Tous les endpoints détaillés
  3. **Modèles JSON** : 13 classes avec attributs
  4. **Accès Données** : 8 classes avec méthodes
  5. **Backend COBOL** : 29 programmes classifiés
- Flux HTTP/REST, JCICS LINK, SQL/VSAM
- Technologies utilisées (JAX-RS, JCICS, Carbon Design System)
- Statistiques complètes

#### Validation
✅ Le fichier s'ouvre correctement dans Draw.io  
✅ Tous les endpoints REST sont listés  
✅ Les 13 modèles JSON sont représentés  
✅ Les flux de communication sont clairs  
✅ Les technologies sont documentées

### Temps Estimé
⏱️ 20-25 minutes (10-12 min par diagramme)

---

<a name="exercice-6"></a>
## Exercice 6 : Analyse Fonctionnelle - Transfert Local

### Objectif
Comprendre en profondeur le fonctionnement de la transaction de transfert local de fonds.

### Mode Bob à Utiliser
🧰 **Z Code**

### Prompt Recommandé
```
en quoi consiste la transaction Transfer local?
```

### Ce que Bob va Faire
1. Lire les fichiers sources (TransferLocalJSON.java, XFRFUN.cbl, BNK1TFN.cbl)
2. Analyser le flux de la transaction
3. Identifier les validations effectuées
4. Documenter la gestion des erreurs
5. Expliquer la stratégie anti-deadlock
6. Détailler les mécanismes de sécurité (SYNCPOINT, ROLLBACK)

### Résultat Attendu
**Réponse de Bob contenant :**

**1. Composants Impliqués :**
- TransferLocalJSON.java (modèle)
- BNK1TFN.cbl (interface BMS)
- XFRFUN.cbl (logique métier)

**2. Flux de Transaction :**
- Validation initiale (montant > 0, comptes différents)
- Ordre de mise à jour (prévention deadlock)
- Mise à jour compte source (débit)
- Mise à jour compte destination (crédit)
- Enregistrement audit (PROCTRAN)

**3. Gestion des Erreurs :**
- Code '1' : Compte source introuvable
- Code '2' : Compte destination introuvable
- Code '3' : Erreur inattendue
- Code '4' : Montant invalide

**4. Mécanismes de Sécurité :**
- Transaction atomique (ACID)
- SYNCPOINT ROLLBACK
- Prévention des deadlocks
- Audit trail complet

### Validation
✅ L'explication couvre les 3 composants principaux  
✅ Le flux de transaction est détaillé étape par étape  
✅ Les 4 codes d'erreur sont expliqués  
✅ Les mécanismes de sécurité sont documentés  
✅ La stratégie anti-deadlock est expliquée

### Temps Estimé
⏱️ 10-15 minutes

---

<a name="exercice-7"></a>
## Exercice 7 : Guide Utilisateur

### Objectif
Créer un guide utilisateur complet pour la fonction de transfert local, destiné aux utilisateurs finaux.

### Mode Bob à Utiliser
🧰 **Z Code**

### Prompt Recommandé
```
Fais moi un guide utilisateur du transfert local.
```

### Ce que Bob va Faire
1. Créer une structure de guide professionnel
2. Documenter les prérequis
3. Expliquer l'accès via les 3 interfaces (BMS, Web, API)
4. Détailler la procédure étape par étape
5. Lister tous les messages d'erreur avec solutions
6. Fournir des exemples pratiques
7. Ajouter une FAQ et des conseils de sécurité

### Résultat Attendu
**Fichier créé :** `docs/GUIDE_UTILISATEUR_TRANSFERT_LOCAL.md`

**Contenu attendu (500 lignes) :**

**1. Sections Principales :**
- Vue d'ensemble
- Prérequis
- Accès à la fonction (BMS 3270, Web, API REST)
- Procédure de transfert (4 étapes détaillées)
- Validation et confirmation
- Messages d'erreur (6 types)
- Exemples pratiques (3 scénarios)
- Questions fréquentes (8 questions)
- Conseils de sécurité

**2. Éléments Visuels :**
- Captures d'écran BMS simulées
- Exemples de requêtes API REST
- Tableaux de raccourcis clavier
- Exemples de calculs de soldes

**3. Informations Techniques :**
- Programmes COBOL impliqués
- Tables de base de données
- Codes de transaction CICS

### Validation
✅ Le fichier fait environ 500 lignes  
✅ Les 3 interfaces sont documentées (BMS, Web, API)  
✅ La procédure est détaillée en 4 étapes  
✅ Les 6 messages d'erreur sont expliqués avec solutions  
✅ 3 exemples pratiques sont fournis  
✅ La FAQ contient au moins 8 questions  
✅ Les conseils de sécurité sont présents

### Temps Estimé
⏱️ 15-20 minutes

---

<a name="exercice-8"></a>
## Exercice 8 : Analyse Technique - Credit Score

### Objectif
Comprendre le système de notation de crédit et son implémentation technique avec l'API asynchrone JCICS.

### Mode Bob à Utiliser
🧰 **Z Code**

### Exercice 8A : Fonctionnement Général

#### Prompt Recommandé
```
que fait la fonction Credit Score?
```

#### Résultat Attendu
**Réponse de Bob contenant :**

**1. Architecture :**
- CreditScore.java (point d'entrée)
- CreditScoreCICS540.java (implémentation avancée)
- CRDTAGY1-5.cbl (5 agences simulées)

**2. Processus :**
- Lancement de 5 transactions asynchrones
- Chaque agence génère un score 1-999
- Délai aléatoire 0-3 secondes par agence
- Collecte des résultats avec getAny()
- Calcul de la moyenne des scores

**3. Caractéristiques :**
- Parallélisme (API Async JCICS)
- Résilience (continue si une agence échoue)
- Fallback (mode de secours si CICS < 5.4)
- Performance (3 sec max au lieu de 15 sec séquentiel)

### Exercice 8B : Échelle de Valeurs

#### Prompt Recommandé
```
Quelle est l'échelle de valeur des scores de crédit?
```

#### Résultat Attendu
**Réponse de Bob contenant :**

**1. Plage de Valeurs :**
- Minimum : 1
- Maximum : 999
- Type : Nombre entier

**2. Calcul :**
```
Score Final = (Score1 + Score2 + Score3 + Score4 + Score5) / 5
```

**3. Interprétation Suggérée :**
- 1-199 : Très Faible
- 200-399 : Faible
- 400-599 : Moyen
- 600-799 : Bon
- 800-999 : Excellent

**4. Comparaison :**
- CBSA : 1-999 (fictif)
- FICO : 300-850 (USA)
- Experian : 0-999 (UK)

### Validation
✅ L'architecture à 3 niveaux est expliquée  
✅ Le processus asynchrone est détaillé  
✅ L'échelle 1-999 est documentée  
✅ La formule de calcul est fournie  
✅ Une interprétation des scores est proposée  
✅ La comparaison avec les systèmes réels est faite

### Temps Estimé
⏱️ 15-20 minutes (7-10 min par sous-exercice)

---

## Récapitulatif des Livrables

À la fin de ce lab, vous aurez créé les fichiers suivants :

| # | Fichier | Type | Taille |
|---|---------|------|--------|
| 1 | AGENTS.md | Documentation | ~150 lignes |
| 2 | bobz/DD.json | Dictionnaire | 15 entrées |
| 3 | docs/COBOL_INVENTORY.md | Inventaire | ~800 lignes |
| 4 | docs/FRONTEND_INVENTORY.md | Inventaire | ~600 lignes |
| 5 | docs/CBSA_Architecture_Diagram.drawio | Diagramme | 5 couches |
| 6 | docs/CBSA_Frontend_Detailed_Diagram.drawio | Diagramme | 5 couches |
| 7 | docs/GUIDE_UTILISATEUR_TRANSFERT_LOCAL.md | Guide | ~500 lignes |

**Total : 7 fichiers documentant complètement l'application CBSA**

---

## Compétences Acquises

À l'issue de ce lab, vous saurez :

✅ Initialiser un projet mainframe avec Bob  
✅ Créer et maintenir un dictionnaire de données  
✅ Générer des inventaires complets de code COBOL  
✅ Documenter des architectures frontend/backend  
✅ Créer des diagrammes d'architecture professionnels  
✅ Analyser des transactions CICS complexes  
✅ Rédiger des guides utilisateur détaillés  
✅ Comprendre l'API asynchrone JCICS  
✅ Utiliser efficacement les différents modes de Bob  
✅ Formuler des prompts précis et efficaces

---

## Conseils pour Réussir

### 1. Formulation des Prompts
- ✅ **Soyez précis** : "Fais l'inventaire du frontend" plutôt que "Analyse le code"
- ✅ **Utilisez le français** : Bob est configuré pour répondre en français
- ✅ **Une tâche à la fois** : Ne combinez pas plusieurs demandes complexes

### 2. Utilisation des Modes
- 🧰 **Z Code** : Pour toutes les analyses mainframe et génération de documentation
- 📐 **Z Architect** : Pour les analyses d'architecture et de design (non utilisé dans ce lab)
- ❓ **Ask** : Pour des questions sans modification de code

### 3. Validation des Résultats
- ✅ Vérifiez toujours que les fichiers sont créés
- ✅ Ouvrez les fichiers pour valider leur contenu
- ✅ Testez les diagrammes Draw.io dans l'éditeur
- ✅ Lisez les explications de Bob pour comprendre le contexte

### 4. Gestion du Temps
- ⏱️ Suivez les temps estimés pour chaque exercice
- ⏱️ Prenez des pauses entre les exercices longs
- ⏱️ N'hésitez pas à demander des clarifications à Bob

---

## Dépannage

### Problème : Bob ne répond pas
**Solution :** Vérifiez que vous êtes en mode Z Code et que le projet est ouvert dans VSCode

### Problème : Le fichier n'est pas créé
**Solution :** Vérifiez les permissions d'écriture et l'espace disque disponible

### Problème : Le diagramme Draw.io ne s'ouvre pas
**Solution :** Installez l'extension Draw.io Integration dans VSCode

### Problème : Bob génère du contenu en anglais
**Solution :** Rappelez à Bob : "Réponds en français s'il te plaît"

---

## Ressources Complémentaires

- **Documentation CBSA** : `doc/CBSA_Architecture_guide.md`
- **Guide d'installation** : `etc/install/base/doc/README.md`
- **Guide utilisateur BMS** : `etc/usage/base/doc/CBSA_BMS_User_Guide.md`
- **Documentation Bob** : Extension IBM Bob Premium Package for Z

---

## Conclusion

Ce lab vous a permis de découvrir la puissance de Bob pour Z dans l'analyse et la documentation d'applications mainframe complexes. Vous avez appris à :

- Utiliser différents types de prompts pour obtenir des résultats précis
- Générer automatiquement de la documentation professionnelle
- Créer des diagrammes d'architecture visuels
- Comprendre des transactions CICS complexes
- Documenter des APIs REST et des modèles de données

**Prochaines Étapes :**
- Appliquez ces techniques à vos propres projets mainframe
- Explorez les autres modes de Bob (Z Architect, Ask)
- Créez vos propres skills personnalisés avec le skill-builder
- Partagez vos découvertes avec votre équipe

---

**Version du Lab :** 1.0  
**Date de Création :** 12 mai 2026  
**Auteur :** Bob - Assistant IA pour IBM Z  
**Durée Totale :** 2-3 heures

---

© 2026 IBM - CICS Banking Sample Application Lab
