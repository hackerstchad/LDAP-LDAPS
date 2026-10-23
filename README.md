<!--
  ╔════════════════════════════════════════════════════════════════════════════╗
  ║                                                                            ║
  ║   README_LDAP.md — LDAP / LDAPS — Protocoles d'annuaire avancés            ║
  ║   Auteur : hackers_tchad                                                   ║
  ║   Style  : CMatrix Green Animated / Cyber-Tchad Terminal                   ║
  ║                                                                            ║
  ╚════════════════════════════════════════════════════════════════════════════╝
-->

<div align="center">

<pre style="color:#00ff00; background:#000000;">
██╗      ██████╗  █████╗ ██████╗     ██╗     ██████╗  █████╗ ██████╗ ███████╗
██║     ██╔═══██╗██╔══██╗██╔══██╗    ██║     ██╔══██╗██╔══██╗██╔══██╗██╔════╝
██║     ██║   ██║███████║██║  ██║    ██║     ██║  ██║███████║██████╔╝███████╗
██║     ██║   ██║██╔══██║██║  ██║    ██║     ██║  ██║██╔══██║██╔══██╗╚════██║
███████╗╚██████╔╝██║  ██║██████╔╝    ███████╗██████╔╝██║  ██║██║  ██║███████║
╚══════╝ ╚═════╝ ╚═╝  ╚═╝╚═════╝     ╚══════╝╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝

[L]ightweight [D]irectory [A]ccess [P]rotocol  —  Annuaire & Identité
[LDAPS] LDAP over SSL/TLS — Annuaire sécurisé

🟢 CMatrix Green Animated 🟢  //  hackers_tchad  //  Cyber-Tchad Edition
</pre>

</div>

---

# 📜 Table des matières

1. [Introduction](#1-introduction)
2. [Qu'est-ce que LDAP ?](#2-quest-ce-que-ldap-)
3. [Qu'est-ce que LDAPS ?](#3-quest-ce-que-ldaps-)
4. [Histoire et créateurs](#4-histoire-et-créateurs)
5. [Architecture LDAP / LDAPS](#5-architecture-ldap--ldaps)
6. [Modèle de données LDAP](#6-modèle-de-données-ldap)
7. [Fonctionnement du protocole](#7-fonctionnement-du-protocole)
8. [Schéma LDAP](#8-schéma-ldap)
9. [DIT — Directory Information Tree](#9-dit--directory-information-tree)
10. [LDAP vs Active Directory vs OpenLDAP](#10-ldap-vs-active-directory-vs-openldap)
11. [Cas d'usage](#11-cas-dusage)
12. [Qui utilise LDAP / LDAPS ?](#12-qui-utilise-ldap--ldaps-)
13. [Logiciels et implémentations serveur](#13-logiciels-et-implémentations-serveur)
14. [Clients LDAP / outils d'administration](#14-clients-ldap--outils-dadministration)
15. [Commandes de vérification (Linux)](#15-commandes-de-vérification-linux)
16. [Commandes de vérification (Windows)](#16-commandes-de-vérification-windows)
17. [Commandes de vérification (macOS)](#17-commandes-de-vérification-macos)
18. [Configuration d'OpenLDAP](#18-configuration-dopenldap)
19. [Configuration d'Active Directory LDAPS](#19-configuration-dactive-directory-ldaps)
20. [Sécurisation LDAP avec StartTLS et LDAPS](#20-sécurisation-ldap-avec-starttls-et-ldaps)
21. [Authentification LDAP dans des applications](#21-authentification-ldap-dans-des-applications)
22. [LDAP dans Docker / Kubernetes](#22-ldap-dans-docker--kubernetes)
23. [Scripting LDAP : Python, Bash, PHP](#23-scripting-ldap--python-bash-php)
24. [Dépannage / Troubleshooting](#24-dépannage--troubleshooting)
25. [Bonnes pratiques](#25-bonnes-pratiques)
26. [Ressources et liens officiels](#26-ressources-et-liens-officiels)
27. [Glossaire](#27-glossaire)
28. [Auteur et licence](#28-auteur-et-licence)

---

# 1. Introduction

Dans le monde des systèmes d'information modernes, la gestion des identités, des accès et des ressources constitue un enjeu stratégique majeur. Qu'il s'agisse d'authentifier un utilisateur, de centraliser un carnet d'adresses d'entreprise, de gérer des certificats ou de fédérer des services, les annuaires informatiques jouent un rôle central. Parmi les protocoles permettant d'interroger et de modifier ces annuaires, **LDAP** (Lightweight Directory Access Protocol) est devenu le standard incontournable.

LDAP est né du besoin de simplifier l'accès aux annuaires X.500, jugés trop lourds et complexes pour une utilisation sur des réseaux TCP/IP. Sa légèreté, sa robustesse et sa capacité à s'intégrer dans des environnements hétérogènes en ont fait le protocole de référence pour des solutions comme **OpenLDAP**, **Active Directory**, **389 Directory Server**, **ApacheDS** et de nombreux serveurs d'identité.

**LDAPS** représente la version sécurisée de LDAP, encapsulant le trafic dans une couche **SSL/TLS**. Bien que StartTLS (mise à niveau d'une connexion LDAP standard) soit aujourd'hui souvent préféré, LDAPS reste largement utilisé, notamment dans les environnements Windows Active Directory.

Ce document propose une exploration approfondie de LDAP et LDAPS : définitions, histoire, architecture, modèle de données, commandes pratiques, configuration, sécurité, outils, ressources et liens officiels. Il est conçu pour les administrateurs système, les ingénieurs sécurité, les développeurs et tous les passionnés de protocoles réseau.

---

# 2. Qu'est-ce que LDAP ?

**LDAP** est l'acronyme de **Lightweight Directory Access Protocol**, soit en français **Protocole léger d'accès aux annuaires**.

Il s'agit d'un protocole de couche application (niveau 7 du modèle OSI) qui permet d'accéder, de rechercher, de modifier et de gérer des informations stockées dans un **annuaire** distribué. LDAP fonctionne principalement sur le port **TCP/389** (LDAP standard) et utilise le modèle client-serveur.

## 2.1 Définition formelle

LDAP est défini par une série de RFCs (Request for Comments) publiées par l'IETF. La version actuellement la plus utilisée est **LDAPv3** (RFC 4510 à RFC 4519).

- **RFC 4510** : Technical Specification Road Map
- **RFC 4511** : LDAPv3 Protocol Specification
- **RFC 4512** : Directory Information Models
- **RFC 4513** : Authentication Methods and Security Mechanisms
- **RFC 4514** : String Representation of Distinguished Names
- **RFC 4515** : String Representation of Search Filters
- **RFC 4516** : Uniform Resource Locator
- **RFC 4517** : Syntaxes and Matching Rules
- **RFC 4518** : Internationalized String Preparation
- **RFC 4519** : User Applications Attribute Types

## 2.2 Caractéristiques principales

- **Léger** : moins complexe que DAP (Directory Access Protocol) utilisé avec X.500.
- **Basé sur TCP/IP** : contrairement à X.500 qui utilise OSI.
- **Orienté lecture** : optimisé pour un grand nombre de recherches rapides.
- **Modèle hiérarchique** : les données sont organisées en arbre (DIT).
- **Extensible** : grâce aux schémas, aux contrôles et aux mécanismes d'extension.
- **Multiplateforme** : implémenté sur Linux, Windows, macOS, BSD, etc.

## 2.3 Opérations LDAP de base

LDAP définit un ensemble d'opérations que le client peut envoyer au serveur :

| Opération     | Description                                      |
|---------------|--------------------------------------------------|
| Bind          | Authentification du client auprès du serveur     |
| Unbind        | Fermeture de la session                          |
| Search        | Recherche d'entrées dans l'annuaire              |
| Compare       | Comparaison d'une valeur d'attribut              |
| Add           | Ajout d'une nouvelle entrée                      |
| Delete        | Suppression d'une entrée                         |
| Modify        | Modification d'attributs d'une entrée            |
| Modify DN     | Renommage ou déplacement d'une entrée            |
| Abandon       | Annulation d'une opération en cours              |
| Extended      | Opérations étendues (StartTLS, Whoami, etc.)     |

## 2.4 Comparaison LDAP vs base de données relationnelle

| Critère              | LDAP                              | Base de données relationnelle (SQL) |
|----------------------|-----------------------------------|-------------------------------------|
| Modèle de données    | Hiérarchique (arborescent)        | Relationnel (tables)                |
| Requêtes             | Recherche par filtre              | Requêtes SQL complexes              |
| Optimisé pour        | Lecture rapide, nombreuses recherches | Transactions, écritures             |
| Schéma               | Flexible, extensible              | Rigidité plus forte                 |
| Langage              | LDAP Filter (RFC 4515)            | SQL                                 |
| Exemples             | OpenLDAP, AD, 389 DS              | PostgreSQL, MySQL, Oracle           |

## 2.5 Versions de LDAP

- **LDAPv1** : première version expérimentale.
- **LDAPv2** (RFC 1777, 1995) : première version largement déployée.
- **LDAPv3** (RFC 2251, 1997 ; révisé RFC 4510-4519, 2006) : version actuelle, supporte SASL, TLS, Unicode, référents, etc.

---

# 3. Qu'est-ce que LDAPS ?

**LDAPS** signifie **LDAP over SSL/TLS**, c'est-à-dire LDAP encapsulé dans une couche de chiffrement SSL ou TLS.

Contrairement à LDAP standard qui transite en clair sur le port **389**, LDAPS utilise le port **636** par défaut. Toutes les opérations LDAP (bind, search, modify, etc.) sont chiffrées avant d'être transmises sur le réseau.

## 3.1 Pourquoi LDAPS ?

Lorsqu'un client LDAP s'authentifie auprès d'un annuaire, il transmet souvent des informations sensibles : nom d'utilisateur, mot de passe, certificats, informations personnelles. Si ces données transitent en clair, elles peuvent être interceptées par un attaquant (écoute réseau, MITM).

LDAPS résout ce problème en :
- **Chiffrant** les communications.
- **Authentifiant** le serveur grâce à son certificat.
- **Permettant** l'authentification mutuelle par certificat client.

## 3.2 LDAPS vs StartTLS

Il existe deux méthodes pour sécuriser LDAP :

| Mécanisme  | Port | Description                                                                 |
|------------|------|-----------------------------------------------------------------------------|
| LDAPS      | 636  | LDAP encapsulé nativement dans TLS dès l'établissement de la connexion.     |
| StartTLS   | 389  | Connexion LDAP standard qui est ensuite "mise à niveau" vers TLS.           |

**StartTLS** est recommandé par l'IETF car il permet de sécuriser une connexion sans changer de port. Cependant, **LDAPS** reste très répandu, surtout dans les environnements Active Directory et pour des raisons de compatibilité.

## 3.3 Ports et protocoles

| Service           | Port  | Protocole | Description                          |
|-------------------|-------|-----------|--------------------------------------|
| LDAP              | 389   | TCP       | LDAP en clair                        |
| LDAPS             | 636   | TCP       | LDAP sur SSL/TLS                     |
| LDAP (Global Catalog) | 3268 | TCP    | Catalogue global AD en clair         |
| LDAPS (Global Catalog) | 3269 | TCP   | Catalogue global AD sur SSL/TLS      |

## 3.4 Certificats et PKI

Pour déployer LDAPS, il est nécessaire de disposer de certificats X.509. Ces certificats peuvent être :
- Auto-signés (test, labo).
- Émis par une **PKI interne** (autorité de certification d'entreprise).
- Émis par une **autorité publique** (rare pour LDAP interne).

---

# 4. Histoire et créateurs

## 4.1 Origines : X.500 et DAP

Avant LDAP, le standard dominant pour les annuaires était **X.500**, développé par l'**UIT-T** (Union internationale des télécommunications). X.500 définissait un modèle d'annuaire global, mais son protocole d'accès, **DAP** (Directory Access Protocol), reposait sur la pile OSI, ce qui le rendait lourd et peu adapté à Internet.

## 4.2 Naissance de LDAP

En **1993**, des ingénieurs de l'**University of Michigan** ont créé LDAP pour simplifier l'accès aux annuaires X.500 via TCP/IP. Les principaux contributeurs incluent :

- **Tim Howes**
- **Mark Smith**
- **Gordon Good**
- **Brian Beecher**

Le but était de conserver la puissance du modèle X.500 tout en réduisant la complexité du protocole.

## 4.3 Évolution vers LDAPv3

LDAPv3 a été publié en **1997** sous la forme des RFC 2251-2259. Il a ensuite été révisé en **2006** (RFC 4510-4519) pour corriger des ambiguïtés et ajouter le support d'Unicode.

## 4.4 Développement d'OpenLDAP

**OpenLDAP** est né en **1998** sous l'impulsion de **Kurt Zeilenga**. C'est aujourd'hui la suite logicielle LDAP open source la plus utilisée au monde. Elle comprend :
- **slapd** : serveur LDAP autonome.
- **libldap** : bibliothèque client.
- **OpenLDAP client utilities** : ldapsearch, ldapadd, ldapmodify, etc.

## 4.5 Active Directory et LDAP

Microsoft a intégré LDAP comme protocole d'accès principal à **Active Directory**, son annuaire d'entreprise, à partir de **Windows 2000**. Active Directory étend le schéma LDAP avec des attributs et classes propres à Windows.

## 4.6 LDAPS

LDAPS a émergé avec la généralisation de SSL dans les années 1990. Il est devenu un mécanisme standard pour sécuriser les communications avec Active Directory et les annuaires OpenLDAP.

---

# 5. Architecture LDAP / LDAPS

## 5.1 Vue d'ensemble

L'architecture LDAP repose sur le modèle **client-serveur**. Le serveur d'annuaire stocke les informations et répond aux requêtes des clients. Les clients peuvent être des applications, des outils d'administration, des services d'authentification ou des scripts.

```
┌─────────────────────────────────────────────────────────────────┐
│                        RÉSEAU TCP/IP                            │
│                                                                 │
│   ┌──────────────┐         LDAP (389) / LDAPS (636)         ┌──────────────┐
│   │   Client     │ ◄───────────────────────────────────────► │   Serveur    │
│   │  (ldapsearch)│                                           │   slapd / AD │
│   └──────────────┘                                           └──────────────┘
│          │                                                           │
│          │                                                           │
│   ┌──────────────┐                                           ┌──────────────┐
│   │ Application  │ ◄───────────────────────────────────────► │   Backend    │
│   │  (Web, VPN,  │         Authentification / Annuaire        │  (BDB, MDB,  │
│   │   Mail, etc.)│                                           │   SQL, etc.) │
│   └──────────────┘                                           └──────────────┘
└─────────────────────────────────────────────────────────────────┘
```

## 5.2 Composants d'une architecture LDAP

### 5.2.1 Serveur d'annuaire

Le serveur est le cœur du système. Il stocke le **DIT** (Directory Information Tree), gère les connexions, applique le schéma, contrôle les accès et répond aux requêtes.

Exemples de serveurs :
- **OpenLDAP / slapd**
- **Microsoft Active Directory**
- **Red Hat 389 Directory Server**
- **ApacheDS**
- **Oracle Internet Directory**
- **IBM Security Directory Server**

### 5.2.2 Client LDAP

Le client envoie des requêtes au serveur. Il peut être :
- Un outil en ligne de commande (ldapsearch, ldapadd).
- Une interface graphique (Apache Directory Studio, JXplorer).
- Une application (serveur Web, VPN, messagerie).
- Une bibliothèque dans un langage de programmation.

### 5.2.3 Schéma (Schema)

Le schéma définit les types d'objets et d'attributs que l'annuaire peut stocker. Il garantit la cohérence des données.

### 5.2.4 Backend / Base de données

Le backend est le moteur de stockage sous-jacent. OpenLDAP supporte plusieurs backends :
- **mdb** (Lightning Memory-Mapped Database) : backend par défaut, très rapide.
- **hdb** : backend hiérarchique basé sur Berkeley DB.
- **bdb** : ancien backend Berkeley DB.
- **sql** : mapping vers une base de données relationnelle.
- **passwd** : mapping vers /etc/passwd.

### 5.2.5 Overlays

Les overlays sont des modules qui ajoutent des fonctionnalités au serveur sans modifier le backend :
- **ppolicy** : gestion des politiques de mot de passe.
- **memberof** : maintien automatique des appartenances de groupes.
- **syncrepl** : réplication.
- **accesslog** : journalisation des accès.
- **refint** : intégrité référentielle.

## 5.3 Architecture avec réplication

Les annuaires LDAP peuvent être répliqués pour assurer la haute disponibilité et la répartition de charge.

```
┌──────────────────┐
│   Fournisseur    │
│  (Provider)      │
│  slapd master    │
└────────┬─────────┘
         │  syncrepl / delta-syncrepl
         ▼
┌──────────────────┐
│   Consommateur   │
│  (Consumer)      │
│  slapd replica   │
└──────────────────┘
```

Modes de réplication OpenLDAP :
- **syncrepl** : réplication basée sur le protocole LDAP.
- **delta-syncrepl** : réplication incrémentale efficace.
- **Mirror Mode** : multi-maître (N-way Multi-Master).

## 5.4 Architecture Active Directory

Active Directory utilise LDAP comme protocole d'accès, mais ajoute des concepts propres :
- **Domain Controller (DC)** : contrôleur de domaine.
- **Global Catalog (GC)** : catalogue global sur les ports 3268/3269.
- **Sites et sous-réseaux** : topologie de réplication.
- **Group Policy (GPO)** : stratégies de groupe.
- **Kerberos** : protocole d'authentification principal.
- **DNS** : intégration avec DNS pour la localisation des DC.

```
┌──────────────────────────────────────────────────────────────┐
│                    FORÊT ACTIVE DIRECTORY                    │
│                                                              │
│   ┌─────────────────┐        ┌─────────────────┐            │
│   │   Domaine A     │◄──────►│   Domaine B     │            │
│   │  (dc=domaineA,  │ Trust  │  (dc=domaineB,  │            │
│   │   dc=local)     │        │   dc=local)     │            │
│   └────────┬────────┘        └────────┬────────┘            │
│            │                          │                      │
│   ┌────────▼────────┐        ┌────────▼────────┐            │
│   │  Contrôleur     │        │  Contrôleur     │            │
│   │  de domaine 1   │◄──────►│  de domaine 2   │            │
│   │  LDAP/LDAPS/Kerberos      LDAP/LDAPS/Kerberos           │
│   └─────────────────┘        └─────────────────┘            │
└──────────────────────────────────────────────────────────────┘
```

## 5.5 Intégration LDAP dans une architecture SI

LDAP est souvent intégré à :
- **SSO (Single Sign-On)** : via Kerberos, SAML, OAuth/OpenID Connect.
- **Reverse Proxy / WAF** : authentification des utilisateurs.
- **VPN** : OpenVPN, pfSense, FortiGate, Cisco AnyConnect.
- **Messagerie** : Postfix, Dovecot, Exchange.
- **Applicatifs métiers** : ERP, CRM, RH, etc.
- **CIAM / IAM** : gestion des identités et accès.

---

# 6. Modèle de données LDAP

Le modèle de données LDAP est fondamental pour comprendre comment les informations sont organisées dans un annuaire.

## 6.1 Les entrées (Entries)

Une entrée LDAP est l'unité de base d'information. Chaque entrée correspond à un objet du monde réel : une personne, un groupe, un ordinateur, une imprimante, une unité organisationnelle, etc.

Chaque entrée est identifiée de manière unique par son **DN** (Distinguished Name).

## 6.2 Les attributs (Attributes)

Une entrée est composée d'un ensemble d'attributs. Chaque attribut a un nom et une ou plusieurs valeurs.

Exemple d'attributs pour une personne :
- `cn` : Common Name (nom commun).
- `sn` : Surname (nom de famille).
- `givenName` : prénom.
- `mail` : adresse email.
- `telephoneNumber` : numéro de téléphone.
- `uid` : identifiant utilisateur.
- `userPassword` : mot de passe.
- `objectClass` : classes d'objets.

## 6.3 Les classes d'objets (ObjectClasses)

Les classes d'objets définissent le type d'une entrée et les attributs obligatoires ou optionnels associés.

Types de classes d'objets :
- **Structural** : définit la nature de l'entrée (ex: `inetOrgPerson`, `organizationalUnit`).
- **Auxiliary** : ajoute des caractéristiques (ex: `posixAccount`, `shadowAccount`).
- **Abstract** : classe de base (ex: `top`).

Exemple d'entrée avec LDIF :

```ldif
dn: uid=jdoe,ou=users,dc=example,dc=com
objectClass: top
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
cn: John Doe
sn: Doe
givenName: John
uid: jdoe
uidNumber: 10001
gidNumber: 10001
homeDirectory: /home/jdoe
loginShell: /bin/bash
mail: jdoe@example.com
userPassword: {SSHA}xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## 6.4 DN et RDN

- **DN (Distinguished Name)** : nom unique complet d'une entrée dans l'annuaire.
- **RDN (Relative Distinguished Name)** : partie du DN relative à son parent.

Exemple :
- DN : `uid=jdoe,ou=users,dc=example,dc=com`
- RDN : `uid=jdoe`
- Parent : `ou=users,dc=example,dc=com`

## 6.5 Syntaxes et matching rules

Chaque attribut LDAP possède une syntaxe qui définit le type de données qu'il peut contenir :
- **Directory String** : chaîne de caractères.
- **IA5 String** : chaîne ASCII (ex: email).
- **Integer** : entier.
- **Boolean** : vrai/faux.
- **Binary** : données binaires.
- **DN** : distinguished name.
- **Generalized Time** : date/heure.

Les **matching rules** définissent comment les valeurs sont comparées (égalité, sous-chaîne, ordre, etc.).

---

# 7. Fonctionnement du protocole

## 7.1 Établissement d'une connexion

1. Le client ouvre une connexion TCP vers le serveur sur le port 389 (LDAP) ou 636 (LDAPS).
2. Le client envoie une opération **Bind** pour s'authentifier (anonyme, simple, SASL).
3. Le client effectue des opérations (search, add, modify, etc.).
4. Le client envoie **Unbind** pour fermer la session.

## 7.2 Opération Bind

Le Bind est l'opération d'authentification. Il existe plusieurs méthodes :

### 7.2.1 Bind anonyme

Aucune authentification. Généralement limité à la lecture de certaines informations.

```bash
ldapsearch -x -H ldap://ldap.example.com -b dc=example,dc=com
```

### 7.2.2 Bind simple

Authentification par DN et mot de passe.

```bash
ldapsearch -x -H ldap://ldap.example.com -D "uid=admin,dc=example,dc=com" -w password -b dc=example,dc=com
```

### 7.2.3 Bind SASL

Authentification via SASL (Simple Authentication and Security Layer), supportant Kerberos (GSSAPI), certificats client (EXTERNAL), etc.

```bash
ldapsearch -Y GSSAPI -H ldap://ldap.example.com
```

## 7.3 Opération Search

La recherche est l'opération la plus utilisée. Elle comprend :
- **Base DN** : point de départ de la recherche.
- **Scope** : portée (`base`, `one`, `sub`).
- **Filter** : filtre de recherche (RFC 4515).
- **Attributes** : attributs à retourner.

Exemple de filtre :
- `(objectClass=inetOrgPerson)` : toutes les personnes.
- `(&(objectClass=inetOrgPerson)(uid=jdoe))` : personne avec uid=jdoe.
- `(|(cn=John*)(cn=Jane*))` : personnes dont le cn commence par John ou Jane.
- `(!(objectClass=group))` : tout sauf les groupes.

Exemple de commande ldapsearch :

```bash
ldapsearch -x -H ldap://ldap.example.com -b ou=users,dc=example,dc=com \
  "(&(objectClass=inetOrgPerson)(uid=jdoe))" cn mail telephoneNumber
```

## 7.4 Opérations d'écriture

### 7.4.1 Add

Ajoute une nouvelle entrée à partir d'un fichier LDIF.

```bash
ldapadd -x -H ldap://ldap.example.com -D "cn=admin,dc=example,dc=com" -w password -f user.ldif
```

### 7.4.2 Modify

Modifie les attributs d'une entrée existante.

Exemple de fichier modify.ldif :

```ldif
dn: uid=jdoe,ou=users,dc=example,dc=com
changetype: modify
replace: mail
mail: jdoe.new@example.com
-
add: telephoneNumber
telephoneNumber: +235 66 12 34 56
```

```bash
ldapmodify -x -H ldap://ldap.example.com -D "cn=admin,dc=example,dc=com" -w password -f modify.ldif
```

### 7.4.3 Delete

Supprime une entrée.

```bash
ldapdelete -x -H ldap://ldap.example.com -D "cn=admin,dc=example,dc=com" -w password \
  "uid=jdoe,ou=users,dc=example,dc=com"
```

## 7.5 LDAP URL

LDAP peut être représenté sous forme d'URL (RFC 4516) :

```
ldap://host:port/dn?attributes?scope?filter?extensions
```

Exemple :

```
ldap://ldap.example.com:389/ou=users,dc=example,dc=com?cn,mail?sub?(objectClass=inetOrgPerson)
```

---

# 8. Schéma LDAP

## 8.1 Rôle du schéma

Le schéma LDAP définit :
- Les **objectClasses** disponibles.
- Les **attributeTypes** utilisables.
- Les **syntaxes** et **matching rules**.
- Les **DIT Structure Rules** et **Name Forms** (moins utilisés).

## 8.2 Schémas standards

OpenLDAP inclut par défaut plusieurs schémas :
- **core.schema** : classes et attributs de base.
- **cosine.schema** : extensions RFC 1274.
- **inetorgperson.schema** : personnes Internet (RFC 2798).
- **nis.schema** : compatibilité NIS / POSIX.
- **misc.schema**, **openldap.schema**, etc.

## 8.3 Schémas Microsoft Active Directory

AD étend le schéma LDAP avec des classes propres :
- `user`
- `computer`
- `group`
- `organizationalUnit`
- `contact`
- Attributs comme `sAMAccountName`, `userPrincipalName`, `memberOf`, etc.

## 8.4 Extension du schéma

Il est possible d'ajouter des attributs et classes personnalisés. Cela se fait via des fichiers LDIF de mise à jour du schéma.

Exemple de fichier schema.ldif :

```ldif
dn: cn=maschema,cn=schema,cn=config
objectClass: olcSchemaConfig
cn: maschema
olcAttributeTypes: ( 1.3.6.1.4.1.4203.666.1.100
  NAME 'employeeID'
  DESC 'Employee identifier'
  EQUALITY caseIgnoreMatch
  SUBSTR caseIgnoreSubstringsMatch
  SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
  SINGLE-VALUE )
olcObjectClasses: ( 1.3.6.1.4.1.4203.666.2.1
  NAME 'customPerson'
  DESC 'Custom person class'
  SUP inetOrgPerson
  STRUCTURAL
  MAY ( employeeID $ department )
  )
```

Application :

```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f schema.ldif
```

---

# 9. DIT — Directory Information Tree

## 9.1 Structure hiérarchique

Le DIT est l'arborescence dans laquelle sont stockées les entrées LDAP. Il ressemble à une structure de dossiers.

Exemple typique :

```
dc=example,dc=com
├── ou=users
│   ├── uid=jdoe
│   ├── uid=asmith
│   └── uid=mgarcia
├── ou=groups
│   ├── cn=admins
│   ├── cn=developers
│   └── cn=users
├── ou=computers
│   ├── cn=pc01
│   └── cn=pc02
├── ou=services
│   ├── cn=ldap
│   └── cn=mail
└── ou=roles
    ├── cn=admin
    └── cn=readonly
```

## 9.2 Composants du DIT

- **dc (domainComponent)** : composant de domaine (ex: dc=example,dc=com).
- **ou (organizationalUnit)** : unité organisationnelle.
- **cn (commonName)** : nom commun.
- **uid (userID)** : identifiant utilisateur.
- **o (organization)** : organisation.
- **c (countryName)** : pays.

## 9.3 Conception du DIT

Une bonne conception du DIT est essentielle pour :
- Faciliter les recherches.
- Gérer les permissions (ACL).
- Permettre la réplication.
- Assurer la scalabilité.

Conseils :
- Éviter les arbres trop profonds.
- Regrouper logiquement les entrées.
- Prévoir l'évolution (fusions, acquisitions).
- Standardiser les noms et attributs.

---

# 10. LDAP vs Active Directory vs OpenLDAP

| Critère                  | OpenLDAP                  | Active Directory                    | 389 Directory Server        |
|--------------------------|---------------------------|-------------------------------------|-----------------------------|
| Éditeur                  | OpenLDAP Project          | Microsoft                           | Red Hat / IBM               |
| Licence                  | Open source (OpenLDAP)    | Propriétaire (licence Windows)      | Open source                 |
| OS principal             | Linux, Unix, BSD          | Windows Server                      | Linux                       |
| Protocole principal      | LDAPv3                    | LDAP + Kerberos + DNS + SMB         | LDAPv3                      |
| Sécurité                 | TLS/StartTLS/SASL         | LDAPS / StartTLS / Kerberos         | TLS/StartTLS/SASL           |
| GPO                      | Non                       | Oui                                 | Non                         |
| Catalogue global         | Non natif                 | Oui                                 | Non                         |
| Réplication              | syncrepl, multi-maître    | Réplication inter-site AD           | Multi-maître                |
| Interface graphique      | Oui (interfaces tierces)  | Oui (ADUC, ADAC)                    | Oui (console web)           |
| Utilisation typique      | Linux, applicatifs        | Environnements Windows              | Grandes entreprises Linux   |

---

# 11. Cas d'usage

## 11.1 Authentification centralisée

LDAP permet de centraliser les comptes utilisateurs et mots de passe. Les systèmes Linux peuvent utiliser **SSSD**, **nslcd** ou **LDAP PAM** pour s'authentifier contre un annuaire.

## 11.2 Annuaire d'entreprise

Centralisation des informations employés : nom, email, téléphone, département, poste, manager, etc.

## 11.3 Authentification applicative

De nombreuses applications (GitLab, Jenkins, Nextcloud, WordPress, Confluence, Jira, etc.) supportent l'authentification LDAP/LDAPS.

## 11.4 VPN et accès réseau

Les solutions VPN (OpenVPN, WireGuard avec portail, FortiGate, pfSense) peuvent utiliser LDAP pour valider les credentials.

## 11.5 Messagerie

Postfix, Dovecot, Exchange peuvent consulter LDAP pour la résolution d'adresses, les alias et les listes de diffusion.

## 11.6 Gestion des certificats et PKI

LDAP peut stocker des certificats, des CRL et des informations PKI.

## 11.7 Fédération d'identités

LDAP est souvent utilisé en backend derrière des solutions IAM/SSO comme Keycloak, Authelia, LemonLDAP::NG, Shibboleth.

---

# 12. Qui utilise LDAP / LDAPS ?

LDAP est utilisé par :
- Les **entreprises** pour Active Directory.
- Les **universités** pour la gestion des étudiants et personnels.
- Les **administrations** pour les annuaires d'agents.
- Les **FAI** et **hébergeurs** pour la gestion clients.
- Les **projets open source** pour l'authentification centralisée.
- Les **opérateurs télécoms** pour les annuaires X.500 modernisés.
- Les **hôpitaux** pour la gestion des professionnels de santé.
- Les **ONG et associations** pour la gestion des adhérents.

---

# 13. Logiciels et implémentations serveur

## 13.1 OpenLDAP

Le serveur LDAP open source le plus populaire.

- Site : https://www.openldap.org/
- Composants : slapd, libldap, client utilities.
- Licence : OpenLDAP Public License.

## 13.2 Microsoft Active Directory

Annuaire intégré à Windows Server.

- Site : https://learn.microsoft.com/fr-fr/windows-server/identity/ad-ds/
- Protocoles : LDAP, LDAPS, Kerberos, DNS, SMB.

## 13.3 Red Hat 389 Directory Server

Serveur d'annuaire d'entreprise open source.

- Site : https://www.port389.org/
- Anciennement Fedora Directory Server, Netscape Directory Server.

## 13.4 ApacheDS

Serveur d'annuaire écrit en Java, projet Apache.

- Site : https://directory.apache.org/apacheds/

## 13.5 Oracle Internet Directory

Solution LDAP commerciale d'Oracle.

- Site : https://www.oracle.com/

## 13.6 IBM Security Directory Server

Solution LDAP d'IBM pour les grandes entreprises.

- Site : https://www.ibm.com/

## 13.7 Univention Corporate Server (UCS)

Distribution Linux avec annuaire OpenLDAP intégré et interface de gestion.

- Site : https://www.univention.com/

## 13.8 FreeIPA

Solution d'identité pour Linux basée sur 389 DS, Kerberos, DNS et PKI.

- Site : https://www.freeipa.org/

---

# 14. Clients LDAP / outils d'administration

## 14.1 Outils en ligne de commande (OpenLDAP)

| Outil        | Usage                                      |
|--------------|--------------------------------------------|
| ldapsearch   | Rechercher des entrées                     |
| ldapadd      | Ajouter des entrées                        |
| ldapmodify   | Modifier des entrées                       |
| ldapdelete   | Supprimer des entrées                      |
| ldapcompare  | Comparer des valeurs d'attributs           |
| ldapwhoami   | Identifier l'utilisateur authentifié       |
| ldappasswd   | Changer un mot de passe                    |

## 14.2 Interfaces graphiques

- **Apache Directory Studio** : https://directory.apache.org/studio/
- **JXplorer** : http://jxplorer.org/
- **LDAP Admin** (Windows) : http://www.ldapadmin.org/
- **phpLDAPadmin** : https://phpldapadmin.sourceforge.io/
- **LDAP Account Manager (LAM)** : https://www.ldap-account-manager.org/
- **FusionDirectory** : https://www.fusiondirectory.org/

## 14.3 Bibliothèques de programmation

- **Python** : `ldap3`, `python-ldap`
- **Java** : JNDI, UnboundID LDAP SDK
- **Node.js** : `ldapjs`
- **PHP** : extension `ldap`
- **Go** : `go-ldap`
- **Ruby** : `net-ldap`
- **C/C++** : OpenLDAP client libraries

---

# 15. Commandes de vérification (Linux)

## 15.1 Installation des outils

### Debian / Ubuntu

```bash
sudo apt update
sudo apt install ldap-utils slapd
```

### RHEL / CentOS / Rocky / AlmaLinux

```bash
sudo dnf install openldap-clients openldap-servers
```

### Arch Linux

```bash
sudo pacman -S openldap
```

## 15.2 Vérifier que le service LDAP écoute

```bash
sudo ss -tlnp | grep -E '389|636'
sudo netstat -tlnp | grep -E '389|636'
```

## 15.3 Tester une connexion LDAP

```bash
ldapsearch -x -H ldap://localhost -b dc=example,dc=com -s base
```

## 15.4 Tester une connexion LDAPS

```bash
ldapsearch -x -H ldaps://localhost -b dc=example,dc=com -s base
```

Avec vérification de certificat désactivée (test uniquement) :

```bash
LDAPTLS_REQCERT=never ldapsearch -x -H ldaps://localhost -b dc=example,dc=com -s base
```

## 15.5 Tester StartTLS

```bash
ldapsearch -x -H ldap://localhost -ZZ -b dc=example,dc=com -s base
```

## 15.6 Authentification avec Bind simple

```bash
ldapsearch -x -H ldap://localhost -D "cn=admin,dc=example,dc=com" -w password -b dc=example,dc=com
```

## 15.7 Rechercher un utilisateur

```bash
ldapsearch -x -H ldap://localhost -b ou=users,dc=example,dc=com "uid=jdoe"
```

## 15.8 Vérifier le schéma

```bash
ldapsearch -x -H ldap://localhost -b cn=subschema -s base "(objectclass=*)" + | less
```

## 15.9 Vérifier les ACL / permissions

```bash
ldapsearch -x -H ldap://localhost -D "uid=jdoe,ou=users,dc=example,dc=com" -w password -b dc=example,dc=com
```

## 15.10 Capturer le trafic LDAP avec tcpdump

```bash
sudo tcpdump -i any -nn port 389 or port 636 -w ldap_traffic.pcap
```

Analyse avec Wireshark ou tshark :

```bash
tshark -r ldap_traffic.pcap -V ldap
```

## 15.11 Vérifier les certificats LDAPS avec OpenSSL

```bash
openssl s_client -connect ldap.example.com:636 -showcerts </dev/null
```

## 15.12 Vérifier la connexion LDAPS avec nmap

```bash
nmap -p 636 --script ssl-cert,ssl-enum-ciphers ldap.example.com
```

---

# 16. Commandes de vérification (Windows)

## 16.1 Outils natifs Windows

### Ldp.exe (LDAP Browser inclus dans RSAT / Support Tools)

Ldp.exe est un outil graphique pour tester les connexions LDAP/LDAPS.

```
1. Ouvrir ldp.exe
2. Connection > Connect
3. Entrer le serveur et le port (389 ou 636)
4. Connection > Bind
5. Entrer les credentials
```

### PowerShell

#### Module Active Directory

```powershell
Import-Module ActiveDirectory
Get-ADUser -Identity jdoe
Get-ADGroup -Identity "Domain Admins"
Get-ADObject -LDAPFilter "(objectClass=user)"
```

#### Tester une connexion LDAPS

```powershell
Test-NetConnection -ComputerName ldap.example.com -Port 636
```

#### Recherche LDAP avec ADSI

```powershell
$ldap = "LDAP://dc=example,dc=com"
$searcher = New-Object DirectoryServices.DirectorySearcher([ADSI]$ldap)
$searcher.Filter = "(sAMAccountName=jdoe)"
$result = $searcher.FindOne()
$result.Properties
```

## 16.2 Outils tiers Windows

- **LDAP Admin** : http://www.ldapadmin.org/
- **Apache Directory Studio**
- **JXplorer**
- **SoftPerfect Network Scanner**

## 16.3 Vérifier les ports avec netsh

```cmd
netstat -an | findstr "389 636 3268 3269"
```

## 16.4 Vérifier les certificats LDAPS

```powershell
Get-ChildItem -Path Cert:\LocalMachine\My
Get-ChildItem -Path Cert:\LocalMachine\Root
```

---

# 17. Commandes de vérification (macOS)

## 17.1 Installation des outils

```bash
brew install openldap
```

## 17.2 Tester LDAP / LDAPS

```bash
ldapsearch -x -H ldap://ldap.example.com -b dc=example,dc=com -s base
ldapsearch -x -H ldaps://ldap.example.com -b dc=example,dc=com -s base
```

## 17.3 Utiliser ldapsearch intégré

macOS inclut une version de ldapsearch dans `/usr/bin/ldapsearch`.

```bash
/usr/bin/ldapsearch -x -H ldap://localhost -b dc=example,dc=com
```

## 17.4 Vérifier les certificats

```bash
openssl s_client -connect ldap.example.com:636
```

---

# 18. Configuration d'OpenLDAP

## 18.1 Installation sur Debian/Ubuntu

```bash
sudo apt update
sudo DEBIAN_FRONTEND=noninteractive apt install -y slapd ldap-utils
sudo dpkg-reconfigure slapd
```

## 18.2 Structure de configuration (slapd.d)

OpenLDAP utilise une configuration en ligne (OLC — OnLine Configuration) stockée dans `/etc/ldap/slapd.d/`.

```
/etc/ldap/
├── slapd.d/
│   └── cn=config/
│       ├── cn=module{0}.ldif
│       ├── cn=schema/
│       ├── olcDatabase={0}config.ldif
│       └── olcDatabase={1}mdb.ldif
├── slapd.conf        # ancienne méthode (obsolète)
└── ldap.conf         # configuration client
```

## 18.3 Configurer le domaine de base

Lors du reconfigure, définir :
- Domaine DNS : `example.com`
- Organisation : `Example Inc`
- Mot de passe administrateur

## 18.4 Ajouter des unités organisationnelles

Fichier `base.ldif` :

```ldif
dn: ou=users,dc=example,dc=com
objectClass: organizationalUnit
ou: users

dn: ou=groups,dc=example,dc=com
objectClass: organizationalUnit
ou: groups

dn: ou=computers,dc=example,dc=com
objectClass: organizationalUnit
ou: computers
```

Application :

```bash
ldapadd -x -D "cn=admin,dc=example,dc=com" -w password -f base.ldif
```

## 18.5 Activer les schémas

```bash
sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/cosine.ldif
sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/inetorgperson.ldif
sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/nis.ldif
```

## 18.6 Configurer TLS / StartTLS

### Générer un certificat auto-signé

```bash
sudo openssl req -newkey rsa:2048 -nodes -keyout /etc/ldap/ldap.key -x509 -days 365 -out /etc/ldap/ldap.crt
sudo chown openldap:openldap /etc/ldap/ldap.key /etc/ldap/ldap.crt
sudo chmod 600 /etc/ldap/ldap.key
```

### Appliquer la configuration TLS

Fichier `tls.ldif` :

```ldif
dn: cn=config
changetype: modify
add: olcTLSCACertificateFile
olcTLSCACertificateFile: /etc/ldap/ldap.crt
-
add: olcTLSCertificateFile
olcTLSCertificateFile: /etc/ldap/ldap.crt
-
add: olcTLSCertificateKeyFile
olcTLSCertificateKeyFile: /etc/ldap/ldap.key
```

```bash
sudo ldapmodify -Y EXTERNAL -H ldapi:/// -f tls.ldif
```

Vérification :

```bash
sudo systemctl restart slapd
ldapsearch -x -H ldap://localhost -ZZ -b dc=example,dc=com -s base
```

## 18.7 Configurer LDAPS

LDAPS nécessite un certificat configuré ci-dessus. Le serveur écoute alors sur le port 636 si `slapd` est démarré avec `-h "ldap:/// ldaps:///"`.

Modifier `/etc/default/slapd` :

```bash
SLAPD_SERVICES="ldap:/// ldapi:/// ldaps:///"
```

Puis redémarrer :

```bash
sudo systemctl restart slapd
```

## 18.8 Configurer les ACL

Exemple d'ACL dans `acl.ldif` :

```ldif
dn: olcDatabase={1}mdb,cn=config
changetype: modify
replace: olcAccess
olcAccess: {0}to attrs=userPassword,shadowLastChange
  by self write
  by anonymous auth
  by dn="cn=admin,dc=example,dc=com" write
  by * none
olcAccess: {1}to dn.base="" by * read
olcAccess: {2}to *
  by self write
  by dn="cn=admin,dc=example,dc=com" write
  by * read
```

```bash
sudo ldapmodify -Y EXTERNAL -H ldapi:/// -f acl.ldif
```

---

# 19. Configuration d'Active Directory LDAPS

## 19.1 Prérequis

- Un contrôleur de domaine Windows Server.
- Un certificat serveur installé dans le magasin personnel de l'ordinateur local.
- Le certificat doit avoir l'EKU "Server Authentication".
- Le nom du sujet ou SAN doit correspondre au FQDN du contrôleur de domaine.

## 19.2 Installer un certificat via AD CS

1. Installer le rôle **Active Directory Certificate Services**.
2. Configurer une autorité d'émission d'entreprise.
3. Demander un certificat pour le contrôleur de domaine via le modèle **Domain Controller**.

## 19.3 Vérifier que LDAPS est actif

```powershell
Test-NetConnection -ComputerName dc.example.com -Port 636
```

Ou avec Ldp.exe :

```
Connection > Connect
Server : dc.example.com
Port : 636
Cochez SSL
Connection > Bind
```

## 19.4 Désactiver LDAP en clair (optionnel)

Via la stratégie de groupe ou le registre :

```powershell
# Signer toujours les données LDAP
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\NTDS\Parameters" -Name "LDAPServerIntegrity" -Value 2
```

## 19.5 Ports AD à connaître

| Port | Protocole | Usage                              |
|------|-----------|------------------------------------|
| 389  | TCP/UDP   | LDAP standard                      |
| 636  | TCP       | LDAPS                              |
| 3268 | TCP       | Global Catalog LDAP                |
| 3269 | TCP       | Global Catalog LDAPS               |
| 88   | TCP/UDP   | Kerberos                           |
| 445  | TCP       | SMB                                |
| 53   | TCP/UDP   | DNS                                |

---

# 20. Sécurisation LDAP avec StartTLS et LDAPS

## 20.1 Bonnes pratiques de sécurité

- **Désactiver LDAP en clair** en production si possible.
- **Forcer TLS/SSL** sur le port 636 ou StartTLS.
- **Utiliser des certificats valides** signés par une AC de confiance.
- **Restreindre les binds anonymes**.
- **Appliquer des politiques de mot de passe fortes**.
- **Limiter les ACL** au strict nécessaire.
- **Activer les journaux d'audit**.
- **Surveiller les tentatives d'énumération**.

## 20.2 Désactiver le bind anonyme

Dans OpenLDAP, ajouter dans la configuration :

```ldif
dn: cn=config
changetype: modify
add: olcRequires
olcRequires: authc
```

## 20.3 Politique de mot de passe (ppolicy)

Activer l'overlay ppolicy :

```bash
sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/ppolicy.ldif
```

Configurer l'overlay :

```ldif
dn: olcOverlay=ppolicy,olcDatabase={1}mdb,cn=config
objectClass: olcOverlayConfig
objectClass: olcPPolicyConfig
olcOverlay: ppolicy
olcPPolicyDefault: cn=default,ou=policies,dc=example,dc=com
olcPPolicyHashCleartext: TRUE
olcPPolicyUseLockout: TRUE
```

## 20.4 Sécuriser Active Directory

- Activer **LDAP signing** et **LDAP channel binding**.
- Utiliser des certificats émis par l'AC interne.
- Surveiller les événements de sécurité Windows.
- Restreindre les connexions réseau via des pare-feu.

---

# 21. Authentification LDAP dans des applications

## 21.1 Linux : SSSD

`/etc/sssd/sssd.conf` :

```ini
[sssd]
services = nss, pam
config_file_version = 2
domains = example

[domain/example]
id_provider = ldap
auth_provider = ldap
ldap_uri = ldaps://ldap.example.com
ldap_search_base = dc=example,dc=com
ldap_default_bind_dn = cn=sssd,ou=services,dc=example,dc=com
ldap_default_authtok = password
```

## 21.2 Linux : libnss-ldap / nslcd

`/etc/nslcd.conf` :

```ini
uri ldaps://ldap.example.com
base dc=example,dc=com
binddn cn=nslcd,ou=services,dc=example,dc=com
bindpw password
```

## 21.3 GitLab

Dans `/etc/gitlab/gitlab.rb` :

```ruby
gitlab_rails['ldap_enabled'] = true
gitlab_rails['ldap_servers'] = {
  'main' => {
    'label' => 'LDAP',
    'host' => 'ldap.example.com',
    'port' => 636,
    'uid' => 'sAMAccountName',
    'encryption' => 'simple_tls',
    'bind_dn' => 'cn=gitlab,ou=services,dc=example,dc=com',
    'password' => 'password',
    'base' => 'ou=users,dc=example,dc=com'
  }
}
```

## 21.4 Nextcloud

Via l'application **LDAP user and group backend**.

## 21.5 Jenkins

Plugin **LDAP** : configurer serveur, DN de base, bind DN, filtres de groupe.

## 21.6 WordPress

Plugins : **LDAP Login for Intranet**, **Active Directory Integration**, etc.

---

# 22. LDAP dans Docker / Kubernetes

## 22.1 OpenLDAP avec Docker

```bash
docker run -d --name openldap \
  -p 389:389 -p 636:636 \
  -e LDAP_ORGANISATION="Example Inc" \
  -e LDAP_DOMAIN="example.com" \
  -e LDAP_ADMIN_PASSWORD="password" \
  osixia/openldap:1.5.0
```

## 22.2 Docker Compose

```yaml
version: '3.8'
services:
  openldap:
    image: osixia/openldap:1.5.0
    container_name: openldap
    ports:
      - "389:389"
      - "636:636"
    environment:
      LDAP_ORGANISATION: "Example Inc"
      LDAP_DOMAIN: "example.com"
      LDAP_ADMIN_PASSWORD: "password"
    volumes:
      - ldap_data:/var/lib/ldap
      - ldap_config:/etc/ldap/slapd.d

  phpldapadmin:
    image: osixia/phpldapadmin:0.9.0
    ports:
      - "6443:443"
    environment:
      PHPLDAPADMIN_LDAP_HOSTS: openldap

volumes:
  ldap_data:
  ldap_config:
```

## 22.3 Kubernetes

Utiliser un Helm Chart Bitnami :

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-openldap bitnami/openldap \
  --set global.storageClass=standard \
  --set adminPassword=password \
  --set replicaCount=2
```

---

# 23. Scripting LDAP : Python, Bash, PHP

## 23.1 Python avec ldap3

Installation :

```bash
pip install ldap3
```

Recherche :

```python
from ldap3 import Server, Connection, ALL

server = Server('ldap.example.com', port=636, use_ssl=True, get_info=ALL)
conn = Connection(server, user='cn=admin,dc=example,dc=com', password='password', auto_bind=True)

conn.search('ou=users,dc=example,dc=com', '(objectClass=inetOrgPerson)', attributes=['cn', 'mail'])

for entry in conn.entries:
    print(entry.cn, entry.mail)

conn.unbind()
```

## 23.2 Bash avec ldapsearch

```bash
#!/bin/bash
LDAP_URI="ldaps://ldap.example.com"
BASE_DN="dc=example,dc=com"
BIND_DN="cn=admin,dc=example,dc=com"
BIND_PW="password"

ldapsearch -x -H "$LDAP_URI" -D "$BIND_DN" -w "$BIND_PW" -b "$BASE_DN" \
  "(objectClass=inetOrgPerson)" cn mail | tee resultats.ldif
```

## 23.3 PHP

```php
<?php
$ldap = ldap_connect("ldaps://ldap.example.com", 636);
ldap_set_option($ldap, LDAP_OPT_PROTOCOL_VERSION, 3);
ldap_set_option($ldap, LDAP_OPT_REFERRALS, 0);

$bind = ldap_bind($ldap, "cn=admin,dc=example,dc=com", "password");
if ($bind) {
    $result = ldap_search($ldap, "ou=users,dc=example,dc=com", "(uid=jdoe)", ["cn", "mail"]);
    $entries = ldap_get_entries($ldap, $result);
    print_r($entries);
}
ldap_unbind($ldap);
?>
```

---

# 24. Dépannage / Troubleshooting

## 24.1 Erreurs courantes

| Code / Message                         | Cause probable                              | Solution                                      |
|----------------------------------------|---------------------------------------------|-----------------------------------------------|
| 32 (No such object)                    | DN de base incorrect                        | Vérifier le suffixe de l'annuaire             |
| 34 (Invalid DN syntax)                 | DN mal formé                                | Corriger la syntaxe du DN                     |
| 49 (Invalid credentials)               | Mauvais mot de passe ou DN de bind          | Vérifier credentials                          |
| 50 (Insufficient access)               | ACL trop restrictives                       | Ajuster les ACL                               |
| 51 (Server busy)                       | Serveur surchargé                           | Attendre ou optimiser                         |
| 52 (Unavailable)                       | Serveur indisponible                        | Vérifier le service                           |
| 53 (Unwilling to perform)              | Opération non autorisée                     | Vérifier le schéma et les ACL                 |
| 68 (Entry already exists)              | Entrée déjà présente                        | Supprimer ou modifier                         |
| Can't contact LDAP server              | Pare-feu, service arrêté, mauvais port      | Vérifier connectivité et service              |
| TLS: hostname does not match CN        | Certificat invalide                         | Utiliser le bon FQDN ou certificat valide     |

## 24.2 Activer le mode debug

OpenLDAP :

```bash
slapd -d 256 -h "ldap:/// ldaps:///"
```

Niveaux de debug courants :
- 0 : aucun
- 256 : stats
- 512 : stats2
- 16384 : trace

## 24.3 Vérifier les logs

```bash
sudo journalctl -u slapd -f
sudo tail -f /var/log/syslog | grep slapd
```

## 24.4 Problèmes de certificat

```bash
openssl x509 -in /etc/ldap/ldap.crt -text -noout
openssl s_client -connect ldap.example.com:636 -CAfile /etc/ssl/certs/ca.crt
```

---

# 25. Bonnes pratiques

## 25.1 Conception

- Définir un DIT clair et pérenne.
- Documenter le schéma personnalisé.
- Prévoir la croissance future.
- Utiliser des conventions de nommage.

## 25.2 Sécurité

- Utiliser LDAPS ou StartTLS.
- Limiter les binds anonymes.
- Appliquer des politiques de mot de passe.
- Restreindre les ACL.
- Auditer les accès.
- Protéger les comptes de service.

## 25.3 Performance

- Choisir le backend adapté (mdb recommandé).
- Créer des index sur les attributs fréquemment recherchés.
- Surveiller les requêtes lentes.
- Utiliser la réplication pour la charge et la haute dispo.

## 25.4 Maintenance

- Sauvegarder régulièrement la base (`slapcat`).
- Tester les restaurations (`slapadd`).
- Planifier les mises à jour de sécurité.
- Documenter les procédures.

---

# 26. Ressources et liens officiels

## 26.1 RFCs LDAPv3

- RFC 4510 : https://tools.ietf.org/html/rfc4510
- RFC 4511 : https://tools.ietf.org/html/rfc4511
- RFC 4512 : https://tools.ietf.org/html/rfc4512
- RFC 4513 : https://tools.ietf.org/html/rfc4513
- RFC 4514 : https://tools.ietf.org/html/rfc4514
- RFC 4515 : https://tools.ietf.org/html/rfc4515
- RFC 4516 : https://tools.ietf.org/html/rfc4516
- RFC 4517 : https://tools.ietf.org/html/rfc4517
- RFC 4518 : https://tools.ietf.org/html/rfc4518
- RFC 4519 : https://tools.ietf.org/html/rfc4519

## 26.2 Documentation OpenLDAP

- Site officiel : https://www.openldap.org/
- Admin Guide : https://www.openldap.org/doc/admin24/
- Man pages : https://www.openldap.org/software/man.cgi

## 26.3 Documentation Microsoft

- Active Directory : https://learn.microsoft.com/fr-fr/windows-server/identity/ad-ds/
- LDAPS : https://learn.microsoft.com/en-us/troubleshoot/windows-server/identity/enable-ldap-over-ssl-3rd-certification-authority

## 26.4 Outils et logiciels

- Apache Directory Studio : https://directory.apache.org/studio/
- phpLDAPadmin : https://phpldapadmin.sourceforge.io/
- LDAP Account Manager : https://www.ldap-account-manager.org/
- FusionDirectory : https://www.fusiondirectory.org/
- FreeIPA : https://www.freeipa.org/
- Univention : https://www.univention.com/

## 26.5 Communautés et forums

- OpenLDAP mailing lists : https://www.openldap.org/lists/
- Server Fault (LDAP tag) : https://serverfault.com/questions/tagged/ldap
- Stack Overflow (LDAP tag) : https://stackoverflow.com/questions/tagged/ldap

---

# 27. Glossaire

| Terme       | Définition                                                       |
|-------------|------------------------------------------------------------------|
| LDAP        | Lightweight Directory Access Protocol                            |
| LDAPS       | LDAP over SSL/TLS                                                |
| DIT         | Directory Information Tree                                       |
| DN          | Distinguished Name                                               |
| RDN         | Relative Distinguished Name                                      |
| LDIF        | LDAP Data Interchange Format                                     |
| OLC         | OnLine Configuration                                             |
| SASL        | Simple Authentication and Security Layer                         |
| TLS         | Transport Layer Security                                         |
| SSL         | Secure Sockets Layer                                             |
| ACL         | Access Control List                                              |
| Schema      | Définition des classes et attributs LDAP                         |
| ObjectClass | Classe définissant le type d'une entrée                          |
| Attribute   | Propriété d'une entrée LDAP                                      |
| Entry       | Unité d'information dans l'annuaire                              |
| slapd       | Standalone LDAP Daemon (serveur OpenLDAP)                        |
| OU          | Organizational Unit                                              |
| CN          | Common Name                                                      |
| DC          | Domain Component                                                 |
| UID         | User Identifier                                                  |
| AD          | Active Directory                                                 |
| GC          | Global Catalog                                                   |
| GPO         | Group Policy Object                                              |
| PKI         | Public Key Infrastructure                                        |
| CA          | Certificate Authority                                            |
| SSO         | Single Sign-On                                                   |
| IAM         | Identity and Access Management                                   |
| SSSD        | System Security Services Daemon                                  |
| PAM         | Pluggable Authentication Modules                                 |

---

# 28. Auteur et licence

**Auteur** : `hackers_tchad`

Ce document a été rédigé pour fournir une référence complète, pratique et avancée sur les protocoles **LDAP** et **LDAPS**. Il s'adresse aux administrateurs système, aux ingénieurs sécurité, aux développeurs et à toute personne souhaitant maîtriser les annuaires LDAP.

**Style** : CMatrix Green Animated — Cyber-Tchad Terminal Edition

**Licence** : Ce README est fourni à titre éducatif. Vous êtes libre de l'utiliser, le modifier et le partager en citant l'auteur `hackers_tchad`.

```
╔════════════════════════════════════════════════════════════════════════════╗
║  Merci d'avoir lu ce guide LDAP / LDAPS !                                  ║
║  N'oubliez pas : un annuaire bien conçu est la clé d'une IAM réussie.      ║
║  hackers_tchad — CMatrix Green Animated                                    ║
╚════════════════════════════════════════════════════════════════════════════╝
```

---

# Annexes complémentaires

## Annexe A : Exemple de fichier LDIF complet

```ldif
# Organisation de base
dn: dc=example,dc=com
objectClass: top
objectClass: dcObject
objectClass: organization
o: Example Inc
dc: example

# Unité organisationnelle Users
dn: ou=users,dc=example,dc=com
objectClass: organizationalUnit
ou: users

# Unité organisationnelle Groups
dn: ou=groups,dc=example,dc=com
objectClass: organizationalUnit
ou: groups

# Utilisateur John Doe
dn: uid=jdoe,ou=users,dc=example,dc=com
objectClass: top
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
cn: John Doe
sn: Doe
givenName: John
uid: jdoe
uidNumber: 10001
gidNumber: 10001
homeDirectory: /home/jdoe
loginShell: /bin/bash
mail: jdoe@example.com
userPassword: {SSHA}xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Groupe admins
dn: cn=admins,ou=groups,dc=example,dc=com
objectClass: top
objectClass: posixGroup
cn: admins
gidNumber: 20001
memberUid: jdoe
```

## Annexe B : Filtres LDAP avancés

```
(objectClass=inetOrgPerson)
(&(objectClass=inetOrgPerson)(uid=jdoe))
(|(cn=John*)(cn=Jane*))
(&(objectClass=inetOrgPerson)(|(mail=*@example.com)(mail=*@example.org)))
(!(objectClass=posixGroup))
(&(objectClass=user)(memberOf=cn=admins,ou=groups,dc=example,dc=com))
(&(objectClass=inetOrgPerson)(telephoneNumber=*))
```

## Annexe C : Commandes OpenLDAP essentielles

```bash
# Tester la connectivité
ldapsearch -x -H ldap://localhost -b "" -s base

# Lister les entrées
ldapsearch -x -H ldap://localhost -b dc=example,dc=com

# Ajouter un utilisateur
ldapadd -x -D cn=admin,dc=example,dc=com -w password -f user.ldif

# Modifier un utilisateur
ldapmodify -x -D cn=admin,dc=example,dc=com -w password -f modify.ldif

# Supprimer un utilisateur
ldapdelete -x -D cn=admin,dc=example,dc=com -w password uid=jdoe,ou=users,dc=example,dc=com

# Changer un mot de passe
ldappasswd -x -D cn=admin,dc=example,dc=com -w password -s newpassword uid=jdoe,ou=users,dc=example,dc=com

# Exporter la base
sudo slapcat > backup.ldif

# Importer la base
sudo slapadd -l backup.ldif

# Vérifier la configuration
slaptest -u
```

## Annexe D : Intégration LDAP avec PAM (Linux)

Installation :

```bash
sudo apt install libpam-ldap libnss-ldap ldap-utils nscd
```

Configuration `/etc/ldap.conf` :

```ini
base dc=example,dc=com
uri ldaps://ldap.example.com
ldap_version 3
binddn cn=nslcd,ou=services,dc=example,dc=com
bindpw password
rootbinddn cn=admin,dc=example,dc=com
pam_login_attribute uid
pam_member_attribute memberUid
pam_password crypt
```

Mise à jour NSS :

```bash
sudo sed -i 's/^passwd:.*/passwd:         files ldap/' /etc/nsswitch.conf
sudo sed -i 's/^group:.*/group:          files ldap/' /etc/nsswitch.conf
sudo sed -i 's/^shadow:.*/shadow:         files ldap/' /etc/nsswitch.conf
```

## Annexe E : LDAPS avec OpenSSL — Génération de certificats

```bash
# Créer une clé privée
openssl genrsa -out ldap.key 2048

# Créer une demande de certificat
openssl req -new -key ldap.key -out ldap.csr -subj "/CN=ldap.example.com/O=Example Inc/C=TD"

# Signer le certificat (auto-signé)
openssl x509 -req -in ldap.csr -signkey ldap.key -out ldap.crt -days 365

# Combiner certificat et clé (optionnel)
cat ldap.crt ldap.key > ldap.pem
```

## Annexe F : Réplication OpenLDAP (syncrepl)

Configuration du fournisseur :

```ldif
dn: olcDatabase={1}mdb,cn=config
changetype: modify
add: olcSyncRepl
olcSyncRepl: rid=001
  provider=ldap://provider.example.com:389/
  type=refreshAndPersist
  retry="5 5 300 5"
  searchbase="dc=example,dc=com"
  attrs="*,+"
  bindmethod=simple
  binddn="cn=replicator,dc=example,dc=com"
  credentials=password
```

Configuration du consommateur :

```ldif
dn: cn=module{0},cn=config
changetype: modify
add: olcModuleLoad
olcModuleLoad: syncprov
```

## Annexe G : Superviser LDAP

Métriques importantes :
- Temps de réponse des requêtes.
- Nombre de connexions actives.
- Taux d'erreurs d'authentification.
- Utilisation CPU/mémoire du serveur.
- Taille de la base de données.
- Latence de réplication.

Outils de supervision :
- **Prometheus** + exporter custom.
- **Nagios / Icinga** : plugins check_ldap.
- **Zabbix** : templates LDAP.
- **Grafana** : tableaux de bord.

## Annexe H : Commandes réseau complètes pour LDAP/LDAPS

### nc / ncat

```bash
nc -vz ldap.example.com 389
nc -vz ldap.example.com 636
```

### curl (LDAP URL)

```bash
curl -v "ldap://ldap.example.com/ou=users,dc=example,dc=com??sub?(uid=jdoe)"
```

### openssl

```bash
openssl s_client -connect ldap.example.com:636 -CAfile ca.crt
```

### nmap scripts

```bash
nmap -p 389 --script ldap-search,ldap-rootdse ldap.example.com
nmap -p 636 --script ssl-cert,ssl-enum-ciphers ldap.example.com
```

---

# Rappel des commandes essentielles par plateforme

## Linux

```bash
# Installation
sudo apt install ldap-utils slapd          # Debian/Ubuntu
sudo dnf install openldap-clients openldap-servers  # RHEL/CentOS

# Tests
ldapsearch -x -H ldap://localhost -b dc=example,dc=com
ldapsearch -x -H ldaps://localhost -b dc=example,dc=com
ldapsearch -x -H ldap://localhost -ZZ -b dc=example,dc=com

# Ports
sudo ss -tlnp | grep -E '389|636'

# Certificats
openssl s_client -connect ldap.example.com:636
```

## Windows

```powershell
# Tester port
Test-NetConnection -ComputerName ldap.example.com -Port 636

# Recherche AD
Get-ADUser -Identity jdoe
Get-ADObject -LDAPFilter "(objectClass=user)"

# GUI
ldp.exe
```

## macOS

```bash
# Installation
brew install openldap

# Tests
ldapsearch -x -H ldap://ldap.example.com -b dc=example,dc=com
ldapsearch -x -H ldaps://ldap.example.com -b dc=example,dc=com

# Certificats
openssl s_client -connect ldap.example.com:636
```

---

# Conclusion

LDAP et LDAPS constituent les fondations de la gestion des identités et des annuaires dans la plupart des entreprises et organisations. Maîtriser ces protocoles, leur architecture, leur sécurité et leurs outils est indispensable pour tout professionnel de l'infrastructure et de la cybersécurité.

Ce guide a couvert :
- Les définitions et différences entre LDAP et LDAPS.
- L'histoire et les créateurs.
- L'architecture et le modèle de données.
- Les commandes de vérification sur Linux, Windows et macOS.
- La configuration d'OpenLDAP et d'Active Directory LDAPS.
- La sécurisation, le scripting, le dépannage et les bonnes pratiques.
- Une multitude de ressources et liens officiels.

N'hésitez pas à approfondir chaque section en consultant les RFCs et documentations officielles. Continuez à apprendre, à expérimenter en labo et à sécuriser vos annuaires.

```
╔════════════════════════════════════════════════════════════════════════════╗
║                                                                            ║
║   FIN DU README_LDAP.md                                                    ║
║   Auteur : hackers_tchad                                                   ║
║   Style  : CMatrix Green Animated — Cyber-Tchad Terminal                   ║
║   Sujet  : LDAP / LDAPS — Protocoles d'annuaire avancés                    ║
║                                                                            ║
╚════════════════════════════════════════════════════════════════════════════╝
```
