# Fiche technique du système

Fiche technique décrivant la totalité des paramétrages système
<h4 style="color: gray;">Paul Burgniard - Merwan CHEHBI - Maxime GERARD - Malo BERGER - Taha CHAUDHRY</h4>

## Sommaire:
- [[#Vue globale du projet :|Vue globale du projet :]]
- [[#Configuration des VMs :|Configuration des VMs :]]
- [[#Plan D'Adressage IP:|Plan D'Adressage IP:]]
- [[#Configuration OPNsense:|Configuration OPNsense:]]
	- [[#Configuration OPNsense:#Règles De Pare Feu:|Règles De Pare Feu:]]
	- [[#Configuration OPNsense:#Services:|Services:]]
- [[#Configuration Serveur Windows:|Configuration Serveur Windows:]]
	- [[#Configuration Serveur Windows:#Services:|Services:]]
		- [[#Services:#Active Directory:|Active Directory:]]
		- [[#Services:#DNS:|DNS:]]
		- [[#Services:#DHCP:|DHCP:]]
- [[#Configuration Linux 1:|Configuration Linux 1:]]
	- [[#Configuration Linux 1:#Service Reverse Proxy Nginx:|Service Reverse Proxy Nginx:]]
- [[#Configuration Linux 2:|Configuration Linux 2:]]
	- [[#Configuration Linux 2:#Service Docker:|Service Docker:]]


## Vue globale du projet :

Création d'un reseaux semblable a celui d'une entreprises séparés et mises en place de différents services internes et externes.
Cette approche est souvent utilisés pour améliorer la sécurité des communications au seins d'une entreprise.
Une fois l'installation effectué des services, il est nécessaire de tester et validés que la configuration réseaux soit fonctionnelles et sécurisé.

Lors de ce projet, nous travaillerons avec *Proxmox Virtual Environment* :
Vpo

Quelques abréviations afin de mieux comprendre :
- AD = Active Directory
- CLT = Client
- DHCP = Dynamic Host Configuration Protocol
- VMs = Virtuals Machines
- DMZ = Demilitarized Zone 

Voici la liste des VMs nécessaires pour le bon fonctionnement du projet (possible d'en ajouter si besoin):

- OPNsense : Notre Firewall
- Windows Serveur : Controleur de domaine de l'AD, serveur DNS et serveur DHCP
- Windows Client : Servant a etre le client de l'AD
- Serveur WEB : Permettant d'heberger notre site web (avec docker)
- Reverse Proxy : Servant de reverse proxy pour le Server WEB (avec nginx)




## Configuration des VMs :

|  🚀 Système D'Exploitation   | 💾 RAM  | 💽 Taille Disque |  🌐 Réseaux  |              📌IP statique              |
| :--------------------------: | :-----: | :--------------: | :----------: | :-----------------------------------: |
| **Opnsense-*opnsense 23.7*** | **2GB** |     **32GB**     |   **tous**   | *Les gateway de chaque réseau* |
|   **Linux1-*Debian 12.0***   | **4GB** |    **628MB**     |   **DMZ**    |             *192.168.3.2*             |
|   **Linux2-*Debian 12.0***   | **4GB** |    **628MB**     |   **DMZ**    |             *192.168.3.3*             |
|  **WindSERV-*Windows 11***   | **8GB** |     **32GB**     | **SERVEURS** |             *192.168.1.2*             |
|    **Wind1-*Windows 11***    | **4GB** |     **30GB**     | **CLIENT**  |                   ❌                   |



## Plan D'Adressage IP:

| 🖧 Réseaux |    🏷️ Gateway     |              📡 DHCP              |
| :--------: | :----------------: | :-------------------------------: |
|  **LAN**   | **192.168.1.1/24** |                 ❌                 |
|  **DMZ**   | **192.168.3.1/24** |                 ❌                 |
| **CLIENT** | **192.168.2.1/24** | **192.168.2.2 ➡️  192.168.2.254** |

## Configuration OPNsense:

### Règles De Pare Feu:

### Services:

## Configuration Serveur Windows:
### Services:
#### Active Directory:

#### DNS:

#### DHCP:

## Configuration Linux 1:

### Service Reverse Proxy Nginx:

## Configuration Linux 2:

### Service Docker:


