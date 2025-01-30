# Fiche technique du système

Fiche technique décrivant la totalité des paramétrages système
<h4 style="color: gray;">Paul Burgniard - Merwan CHEHBI - Maxime GERARD - Malo BERGER - Taha CHAUDHRY</h4>


## Sommaire:
*Vue globale du projet*

*Configuration des VMs*

*Configuration d'OPNsense*
## 

|  🚀 Système D'Exploitation   | 💾 RAM  | 💽 Taille Disque | 🌐 Réseaux |
| :--------------------------: | :-----: | :--------------: | :--------: |
| **Opnsense-*opnsense 23.7*** | **2GB** |     **32GB**     |            |
|   **Linux1-*Debian 12.0***   | **4GB** |    **628MB**     |            |
|   **Linux2-*Debian 12.0***   | **4GB** |    **628MB**     |            |
|  **WindSERV-*Windows 11***   | **8GB** |     **32GB**     |            |
|    **Wind1-*Windows 11***    | **4GB** |     **30GB**     |            |



## Plan D'Adressage IP


| 🖧 Réseaux |    🏷️ Gateway     |              📡 DHCP              |     |
| :--------: | :----------------: | :-------------------------------: | :-: |
|  **LAN**   | **192.168.1.1/24** |                 ❌                 |     |
|  **DMZ**   | **192.168.3.1/24** |                 ❌                 |     |
|  **CLT**   | **192.168.2.1/24** | **192.168.2.2 ➡️  192.168.2.254** |     |


