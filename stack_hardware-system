# Fiche technique — Matériel de virtualisation Proxmox pour Stack LowWatt (SLW)

## 1. Objectif matériel retenu

Mettre en place un cluster **Proxmox VE de 3 nœuds identiques**, au format **mini-PC professionnel 1L reconditionné**, avec un budget cible de **moins de 300 € par unité**, tout en conservant :

- un encombrement minimal
- une consommation maîtrisée
- une fiabilité correcte
- une capacité suffisante pour héberger :
  - Proxmox VE
  - un SIEM léger à intermédiaire
  - Home Assistant
  - Traefik
  - Jellyfin
  - services annexes

---

## 2. Choix matériel retenu

### Choix principal recommandé

- **Modèle** : Lenovo ThinkCentre M920q Tiny
- **CPU cible** : Intel Core i5-8500T ou i5-9500T
- **RAM cible** : 16 Go DDR4 minimum
- **Stockage cible** : SSD NVMe 256 Go minimum, idéalement 512 Go
- **Évolutivité visée** : au moins 1 nœud à 32 Go de RAM pour le SIEM ou Jellyfin

### Alternatives valides

- Dell OptiPlex 7060 Micro
- HP EliteDesk 800 G4 Mini
- Lenovo ThinkCentre M720q Tiny

---

## 3. Pourquoi ce choix

### Format mini-PC professionnel 1L

**Choix technique :**
Utiliser des mini-PC professionnels reconditionnés au lieu de serveurs classiques.

**Justification :**
- format très compact
- faible consommation électrique
- bruit réduit
- matériel professionnel éprouvé
- coût d’achat bien inférieur à un serveur rack ou tour
- très bon rapport prix / performance en occasion

---

### CPU Intel Core i5 série T

**Choix technique :**
Privilégier un **Intel Core i5 8e ou 9e génération**, idéalement en version **T**.

**Justification :**
- consommation plus faible
- performances suffisantes pour Proxmox et plusieurs VM / CT
- présence d’un **iGPU Intel UHD 630**
- compatibilité avec **Intel Quick Sync** pour Jellyfin
- très bon compromis entre coût, chauffe et performances

---

### 16 Go de RAM minimum par nœud

**Choix technique :**
Démarrer avec **16 Go de RAM par machine**.

**Justification :**
- suffisant pour un cluster Proxmox léger à intermédiaire
- permet de répartir les charges entre les 3 nœuds
- cohérent avec le budget imposé
- laisse la possibilité d’augmenter à **32 Go** sur le nœud le plus chargé

**Recommandation :**
- 2 nœuds à 16 Go
- 1 nœud à 32 Go dès que possible pour absorber :
  - SIEM
  - Jellyfin
  - services plus lourds

---

### SSD NVMe prioritaire

**Choix technique :**
Installer un **SSD NVMe** dans chaque nœud.

**Justification :**
- bien meilleures performances qu’un SATA classique
- meilleur confort pour Proxmox et les VM
- démarrage plus rapide
- meilleure réactivité globale
- indispensable pour éviter un cluster lent ou saturé rapidement

**Capacité recommandée :**
- minimum : **256 Go**
- conseillé : **512 Go**

---

## 4. Cas spécifique Jellyfin / “Netflix local”

### Problématique

Le point critique pour Jellyfin n’est pas principalement la RAM, mais le **transcodage vidéo**.

### Choix technique retenu

Utiliser un **CPU Intel avec iGPU actif** pour exploiter **Intel Quick Sync**.

### Justification

- permet le **transcodage matériel**
- réduit fortement la charge CPU
- améliore la fluidité en lecture distante ou sur clients incompatibles
- rend viable Jellyfin sur mini-PC compact

### Règle à retenir

Pour Jellyfin :
- **Direct Play** = idéal
- **Direct Stream** = acceptable
- **Transcodage logiciel CPU** = à éviter
- **Transcodage matériel Intel Quick Sync** = recommandé

### Conséquence matérielle

Le nœud qui héberge Jellyfin doit :
- avoir un **Intel iGPU**
- être prioritaire pour une montée en **32 Go RAM**
- idéalement héberger moins de charges lourdes que le nœud SIEM

---

## 5. Architecture matérielle recommandée

### Cluster PVE proposé

- **Nœud 1** : Proxmox + SIEM léger / logs / sécurité
- **Nœud 2** : Proxmox + Nextcloud + Traefik + services web
- **Nœud 3** : Proxmox + Jellyfin + Home Assistant + services annexes

### Justification

- meilleure répartition des charges
- meilleure résilience
- moins de saturation sur un seul hôte
- maintenance plus simple
- cohérent avec une logique homelab semi-professionnelle

---

## 6. Limites assumées

### Ce qu’il faut accepter avec ce budget

Avec des nœuds à moins de 300 € :
- pas de très forte densité de VM
- pas de gros SIEM à forte volumétrie
- pas de transcodage massif 4K multiple
- pas de cluster Ceph sérieux

### Conséquence

La bonne logique n’est **pas** :
- Ceph
- hyperconvergence ambitieuse
- stockage distribué lourd

La bonne logique est :
- **cluster Proxmox simple**
- **réplication Proxmox**
- **sauvegardes externes**
- **services répartis intelligemment**

---

## 7. Recommandation finale

### Matériel à acheter

#### Option prioritaire
- **3 × Lenovo ThinkCentre M920q Tiny**
- Intel Core i5
- 16 Go RAM minimum
- SSD NVMe 256 ou 512 Go

#### Alternatives acceptables
- **3 × Dell OptiPlex 7060 Micro**
- **3 × HP EliteDesk 800 G4 Mini**
- **3 × Lenovo M720q Tiny**

---

## 8. Synthèse courte

### Choix retenu
- mini-PC professionnels 1L reconditionnés
- Intel Core i5 8e/9e génération
- 16 Go RAM minimum par nœud
- SSD NVMe obligatoire
- 3 nœuds Proxmox identiques

### Justification principale
Ce choix offre le meilleur compromis entre :
- prix
- compacité
- sobriété énergétique
- fiabilité
- performances suffisantes pour un homelab semi-professionnel

### Point clé Jellyfin
Pour un “Netflix local” fluide :
- choisir un CPU Intel avec iGPU
- utiliser Intel Quick Sync
- limiter le transcodage logiciel
- privilégier Direct Play quand possible
