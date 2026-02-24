# Compte rendu -- Mise en place réelle de la maquette

## 1. Objectif

L'objectif de cette maquette est de mettre en place un réseau segmenté
en plusieurs VLAN et de tester l'aspect fonctionnel de notre maquette.

------------------------------------------------------------------------

## 2. Topologie générale

-   1 routeur Cisco 829
-   1 switch central (2960 catalyst)
-   1 switch annexe (VLAN 800 pour l'accés à internet )
-   Plusieurs postes clients répartis par VLAN
-   Des serveurs (DHCP, DNS, Apache)

Le routeur est relié au switch principal par un lien trunk permettant le
routage inter-VLAN (router-on-a-stick).

------------------------------------------------------------------------

## 3. Plan d'adressage IP et VLAN

### VLAN ADMIN

-   Réseau : 192.168.0.0/28
-   Passerelle : 192.168.0.1
-   Rôle : administration et serveurs

### VLAN PERSONNEL

-   Réseau : 192.168.0.32/27
-   Passerelle : 192.168.0.34
-   Rôle : postes du personnel

### VLAN VIDEO

-   Réseau : 192.168.0.80/28
-   Passerelle : 192.168.0.81
-   Rôle : équipements vidéo

### VLAN PRODUCTION

-   Réseau : 192.168.0.96/28
-   Passerelle : 192.168.0.97
-   Rôle : postes de production

------------------------------------------------------------------------

## 4. Configuration du routage inter-VLAN

Le routeur dispose d'interfaces virtuelles associées à chaque VLAN :
 - VLAN 10 : Personnel 
 - VLAN 20 : Admin 
 - VLAN 30 : Production 
 - VLAN 40 : Vidéo

Chaque interfaces virtuelles est configurée de façon à permettre un routage inter-vlan fonctionnel avec
l'adresse IP correspondant à la passerelle du VLAN.

------------------------------------------------------------------------

## 5. DHCP

Un serveur DHCP (isc-dhcp-server) est présent dans le VLAN ADMIN. 
- Attribution automatique des adresses IP 
- Distribution de la passerelle et du DNS 
- Fonctionnement validé sur l'ensemble des VLAN 

------------------------------------------------------------------------

## 6. NAT et accès extérieur

Le NAT est configuré sur l'interface GigabitEthernet4 du routeur :
- Adresse IP : 10.11.0.1
- Route par défaut : 0.0.0.0/0 via 10.11.0.0

Cela permet aux machines internes d'accéder à un réseau externe.

------------------------------------------------------------------------

## 7. Tests et validation

-   Ping intra-VLAN : OK
-   Ping inter-VLAN via le routeur : OK
-   Attribution DHCP : OK
-   Accès aux services serveurs : OK

------------------------------------------------------------------------

## 8. Conclusion

Cette maquette répond aux objectifs initiaux : 
- Segmentation logique du réseau 
- Accès contrôlé entre les VLAN
- Accés distant au materiel grace au SSH

