# Fiche technique du système

Fiche technique décrivant la totalité des paramétrages système
<h4 style="color: gray;">Paul Burgniard - Merwan CHEHBI - Maxime GERARD - Malo BERGER - Taha CHAUDHRY</h4>


## Sommaire:
- *Vue globale du projet*

- *Configuration des VMs*

- *Configuration d'OPNsense*

- *Plan d'Adressage IP*

## Vue globale du projet :
Création d'un reseaux semblable a celui d'une entreprises séparés et mises en place de différents services internes et externes.
Cette approche est souvent utilisés pour améliorer la sécurité des communications au seins d'une entreprise.
Une fois l'installation effectué des servuces, il est necessaire de tester et validés que la configuration reseaux soit fonctionnelles et sécurisé.

Lors de ce projet, nous travaillerons avec *Proxmox Virtual Environment* :
Vpo

Quelques abréviations afin de mieux comprendre :
AD = Active Directory
CLT = Client
DHCP = Dynamic Host Configuration Protocol
VMs = Virtuals Machines
DMZ = Demilitarized Zone 

Voici la liste des VMs nécessaires pour le bon fonctionnement du projet (possible d'en ajouter si besoin):

- OPNsense : Notre Firewall
- Windows Serveur : Controleur de domaine de l'AD, serveur DNS et serveur DHCP
- Windows Client : Servant a etre le client de l'AD
- Serveur WEB : Permettant d'heberger notre site web (avec docker)
- Reverse Proxy : Servant de reverse proxy pour le Server WEB (avec nginx)




## Configuration des VMs :

|  🚀 Système D'Exploitation   | 💾 RAM  | 💽 Taille Disque | 🌐 Réseaux |
| :--------------------------: | :-----: | :--------------: | :--------: |
| **Opnsense-*opnsense 23.7*** | **2GB** |     **32GB**     |            |
|   **Linux1-*Debian 12.0***   | **4GB** |    **628MB**     |            |
|   **Linux2-*Debian 12.0***   | **4GB** |    **628MB**     |            |
|  **WindSERV-*Windows 11***   | **8GB** |     **32GB**     |            |
|    **Wind1-*Windows 11***    | **4GB** |     **30GB**     |            |



## Plan D'Adressage IP


| 🖧 Réseaux |    🏷️ Gateway     |              📡 DHCP              |     
| :--------: | :----------------: | :-------------------------------: | 
|  **LAN**   | **192.168.1.1/24** |                 ❌                 |     
|  **DMZ**   | **192.168.3.1/24** |                 ❌                 |     
|  **CLT**   | **192.168.2.1/24** | **192.168.2.2 ➡️  192.168.2.254** |     


