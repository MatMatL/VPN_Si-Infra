# 🌐 Projet VPN - Accès distant sécurisé à un réseau privé

## 📌 Objectif

Mettre en place une solution VPN permettant à un utilisateur distant de se connecter à un réseau privé via Internet, en garantissant la **sécurité**, la **traçabilité** et la **simplicité d’utilisation** à l'aide d'OpenVPN.

---

## 💽 Infrastructure mise en place

- **Serveur VPN** : Raspberry Pi 3B+ (hébergé à domicile, IP publique via redirection de port)
- **Service VPN** : OpenVPN
- **Client** : Ordinateur portable sous Windows 11
- **Nom de domaine dynamique** : via No-IP
- **Partage de fichiers** : Samba (dossier partagé sécurisé via VPN)
- **Firewall** : Ouverture du port 1194 (UDP) sur la box

---

## 📌 Fonctionnalités

- ✅ Connexion VPN distante sécurisée (OpenVPN)
- ✅ Authentification avec certificat client
- ✅ Redirection de port sur box Internet
- ✅ Partage de fichiers sécurisé en VPN via Samba
- ✅ Création d'utilisateurs VPN
- ✅ Ajout de logs de connexions
- ✅ Sécurisation des accès Samba par utilisateur/groupe

---

## 🔒 Sécurité

- Certificats TLS/SSL générés via `easy-rsa`
- Port 1194 protégé par la box (NAT/PAT)
- Droits utilisateurs restreints (Samba)

---

## ⚙️ Installation serveur (OpenVPN)

### Installalation OpenVPN sur Raspberry Pi

1. Installer l'installer OpenVPN : sudo curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh
2. Executer le fichier (après avoir ajouté les permissions) : sudo ./openvpn-installer.sh
3. Suivre les instructions de configuration

### Création d'un profile client (OpenVPN)

1. Executer le fichier (après avoir ajouté les permissions) : sudo ./openvpn-installer.sh
2. Indiquer le nom de l'utilisateur
3. Suivre les instructions de configuration
4. Transferer le fichier .ovpn créé sur la machine client (à l'aide de scp par exemple)

---

## 🔐 Connexion client

### Documentation utilisateur

1. Installer OpenVPN Connect (Windows / macOS)
2. Récupérer le fichier `.ovpn` fourni
3. Ajouter le profil dans l’application
4. Se connecter en un clic

---

## 📂 Partage de fichiers

- Dossier partagé : `/home/data`
- Accès limité au groupe `employe`
- Configuration Samba :

```ini
[data]
   path = /home/data
   browseable = yes
   writable = yes
   valid users = @employe
   create mask = 0660
   directory mask = 0770
   public = no
   guest ok = no
```

---

## 📄 Commandes utiles

### Ajouter un utilisateur système :

```bash
sudo adduser nom_utilisateur
```

### Ajouter à Samba :

```bash
sudo smbpasswd -a nom_utilisateur
```

### Ajouter au groupe :

```bash
sudo usermod -aG employe nom_utilisateur
```

---

## 📍 Logs VPN

Fichier de log : `/var/log/openvpn/openvpn.log`
Fichier de log status : `/var/log/openvpn/status.log`

### Voir les connexions :

```bash
cat /var/log/openvpn/openvpn.log | grep 'Peer Connection Initiated'
```

---

## 📦 Fichiers livrés

- `README.md` (ce document)
- Documentation d'exploitation 
- Documentation utilisateur 
- Schéma réseau
- Support de présentation (canva)

---

## 📚 Technologies utilisées

| Outil          | Rôle                                   |
| -------------- | -------------------------------------- |
| OpenVPN        | Tunnel VPN sécurisé                    |
| Samba          | Partage de fichiers LAN                |
| No-IP          | DNS dynamique                          |
| Raspberry Pi   | Hébergement du serveur VPN             |
| Livebox6       | Gestion du firewall / forwarding       |

---

## 🧑‍💼 Auteurs

- **Nom** : Lucas G / Mathieu L
- **Date** : Juin 2025

