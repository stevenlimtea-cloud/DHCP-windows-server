# 🖧 DHCP Windows Server – Déploiement et configuration

## 🎯 Objectif
Déployer un serveur DHCP sur Windows Server afin d’automatiser l’attribution des adresses IP et des paramètres réseau dans un environnement local.

---

## 🇬🇧 English summary
Deployment of a DHCP server on Windows Server with scope configuration, reservations and client validation.

---

## ⚙️ Environnement
- Windows Server (rôle DHCP)
- Client Windows 10
- Virtualisation (VirtualBox / VMware)
- Réseau : `192.168.10.0/24`

---

## 🧠 Principe

Le DHCP (Dynamic Host Configuration Protocol) permet d’attribuer automatiquement aux postes clients :
- une adresse IP
- un masque de sous-réseau
- une passerelle par défaut
- un serveur DNS

### 🔄 Fonctionnement (DORA)
1. Discover → recherche d’un serveur DHCP  
2. Offer → proposition d’une adresse IP  
3. Request → demande d’attribution  
4. Acknowledge → validation  

---

## 🔧 Mise en place

### 1. Configuration du serveur
Le serveur DHCP est configuré avec une **adresse IP statique** afin d’assurer sa disponibilité sur le réseau.

---

### 2. Installation du rôle DHCP

![Installation DHCP](images/installation-role-dhcp.png)

---

### 3. Création de l’étendue

- Nom : `LAN_Salarie`
- Plage : `192.168.10.50 → 192.168.10.150`
- Masque : `255.255.255.0`

![Création étendue](images/creation-etendue.png)

---

### 4. Exclusion d’adresses

- Plage exclue : `192.168.10.70 → 192.168.10.80`

![Exclusion](images/exclusion-plage.png)

---

### 5. Configuration des options DHCP

- Passerelle (option 003) : `192.168.10.254`
- DNS (option 006) : `8.8.8.8`

![Options DHCP](images/options-etendue.png)

---

### 6. Réservation DHCP

Attribution d’une adresse IP fixe via adresse MAC :

- IP réservée : `192.168.10.20`

![Réservation](images/reservation-pdg.png)

---

## ✅ Validation

### Vérification côté client

```powershell
ipconfig /all
✔ Résultat attendu :
- Adresse IP attribuée par DHCP  
- Passerelle correcte  
- DNS configuré  

![Client DHCP](images/ipconfig-client.png)

---

### Renouvellement du bail

```powershell
ipconfig /release
ipconfig /renew
