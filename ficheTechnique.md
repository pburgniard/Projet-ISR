# Fiche technique du système

Fiche technique décrivant la totalité des paramétrages système
<h4 style="color: gray;">Paul BURGNIARD - Merwan CHEHBI - Maxime GERARD - Malo BERGER - Taha CHAUDHRY</h4>

## Sommaire:

- [Vue globale du projet :](#vue-globale-du-projet-)
- [Configuration des VMs :](#configuration-des-vms-)
- [Plan D'Adressage IP:](#plan-dadressage-ip)
- [Configuration OPNsense:](#configuration-opnsense)
	- [Règles De Pare Feu:](#r%C3%A8gles-de-pare-feu)
	- [Services:](#services)
- [Configuration Serveur Windows:](#configuration-serveur-windows)
	- [Services:](#services)
		- [Active Directory:](#active-directory)
		- [DNS:](#dns)
		- [DHCP:](#dhcp)
- [Configuration Linux 1:](#configuration-linux-1)
	- [Service Reverse Proxy Nginx:](#service-reverse-proxy-nginx)
- [Configuration Linux 2:](#configuration-linux-2)
	- [Service Docker:](#service-docker)




## Vue globale du projet :

Création d'un réseau semblable à celui d'une entreprise séparée et mise en place de différents services internes et externes.

Cette approche est souvent utilisée pour améliorer la sécurité des communications au sein d'une entreprise.
Une fois l'installation effectuée des services, il est nécessaire de tester et de valider que la configuration réseau soit fonctionnelle et sécurisée.

Lors de ce projet, nous travaillerons avec *Proxmox Virtual Environment* :
Cela nous permettra de faciliter la coopération et l'installation des VMs.

Quelques abréviations afin de mieux comprendre :
- AD = Active Directory
- CLT = Client
- DHCP = Dynamic Host Configuration Protocol
- VMs = Virtual Machines
- DMZ = Demilitarized Zone 

Voici la liste des VMs nécessaires au bon fonctionnement du projet (possible d'en ajouter si besoin) :

- OPNsense : Notre Firewall
- Windows Serveur : Contrôleur de domaine de l'AD, serveur DNS et serveur DHCP
- Windows Client : Servant a être le client de l'AD
- Serveur WEB : Permettant d’héberger notre site web (avec docker)
- Reverse Proxy : Servant de reverse proxy pour le Server WEB (avec nginx)




## Configuration des VMs :

|  🚀 Système D'Exploitation   | 💾 RAM  | 💽 Taille Disque |  🌐 Réseaux  |              📌IP statique              |
| :--------------------------: | :-----: | :--------------: | :----------: | :-----------------------------------: |
| **Opnsense-*Opnsense 23.7*** | **2GB** |     **32GB**     |   **tous**   | *Les gateway de chaque réseau* |
|   **Linux1-*Debian 12.0***   | **4GB** |    **628MB**     |   **DMZ**    |             *192.168.3.2*             |
|   **Linux2-*Debian 12.0***   | **4GB** |    **628MB**     |   **DMZ**    |             *192.168.3.3*             |
|  **WindSERV-*Windows 11***   | **8GB** |     **32GB**     | **SERVEURS** |             *192.168.1.2*             |
|    **Wind1-*Windows 11***    | **4GB** |     **30GB**     | **CLIENT**  |                   ❌                   |



## Plan D'Adressage IP:

|  🖧 Réseaux  |    🏷️ Gateway     |              📡 DHCP              |
| :----------: | :----------------: | :-------------------------------: |
| **SERVEURS** | **192.168.1.1/24** |                 ❌                 |
|   **DMZ**    | **192.168.3.1/24** |                 ❌                 |
|  **CLIENT**  | **192.168.2.1/24** | **192.168.2.2 ➡️  192.168.2.254** |

## Configuration OPNsense:
![Capture d'écran 2025-01-30 101012](https://github.com/user-attachments/assets/e59201a1-327f-4823-beb9-d22534c5d563)

### Règles De Pare Feu:
#### DMZ:
| Action | Source | Destination | Port | Description |
| ------ | ------ | ----------- | ---- | ----------- |
|        |        |             |      |             |
#### SERVEURS:
| Action | Source | Destination | Port | Description |
| ------ | ------ | ----------- | ---- | ----------- |
|        |        |             |      |             |
#### CLIENTS:
| Action | Source | Destination | Port | Description |
| ------ | ------ | ----------- | ---- | ----------- |
|        |        |             |      |             |

#### WAN:
| Action | Source | Destination | Port | Description |
| ------ | ------ | ----------- | ---- | ----------- |
|        |        |             |      |             |

### Services:

## Configuration Serveur Windows:
### Services:
#### Active Directory:

#### DNS:

#### DHCP:

## Configuration Linux 1:

### Service Reverse Proxy Nginx:
```nginx
server{
        listen 80;
        server_name web1.FROMAGELAND.com;
 
        location / {
                proxy_pass http://192.168.3.3:8080;
				proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
 
}
 
server{
        listen 80;
        server_name web2.FROMAGELAND.com;
 
        location / {
                proxy_pass http://192.168.3.3:8081;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
	            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
}
```
## Configuration Linux 2:

### Service Docker:
Le service est défini par le stack compose suivant :

```yaml
version: '3.8'

services:

  server1:
    image: httpd:alpine
    container_name: server1
    ports:
      - "8080:80"
    volumes:
      - ./server1:/usr/local/apache2/htdocs
    restart: always

  server2:
    image: httpd:alpine
    container_name: server2
    ports:
      - "8081:80"
    volumes:
      - ./server2:/usr/local/apache2/htdocs
    restart: always
```


