
GITOYEN : Configuration BIRD d'un routeur de bordure
==========================================

Ce dépot contient la configuration d'un routeur de bordure de Gitoyen. Il s'agit d'une configuration prenant en compte :

  * La gestion des communautés ;
  * La gestion de livraisons (membres, clients) ;
  * La gestion des peering/transits.

N'hésitez pas à vous en inspirer.

## Nous contacter

Pour toutes questions / commentaires / discussions, vous pouvez nous contacter via :

* mél : contact (AT) gitoyen.net ;
* irc : gitoyen / geeknode ;
* www : http://www.gitoyen.net.

## Principe de fonctionnement

* Les routes importées depuis une session bgp sont étiquetées par une communauté indiquant sa provenance.
* Les routes exportées vers une session bgp sont filtrées sur la base des communautés en fonction de leur provenance.
  * Exemples : 
    * Les routes exportées vers une session avec un transitaire comprennent uniquement les routes étiquetées membres/clients/interne.
    * Les routes exportées vers une session avec un membre comprennent toutes les routes de l'Internet.
   
## Organisation

    $ cat etc/local/bird/bird.conf 
    # Gitoyen contact (AT) gitoyen.net
    #
    # vim: set ts=4:sw=4

    log syslog all;

    # Parametres specifiques au routeur
    include "/etc/local/bird/common/local.conf";

    # Filtres/Fonctions communs a tous les protocoles
    include "/etc/local/bird/bird/filters.conf";

    # Gestion des protocoles lies au noyau
    include "/etc/local/bird/common/kernel.conf";

    # Routes statiques
    include "/etc/local/bird/bird/static.conf";

    # OSPF (Backbone)
    include "/etc/local/bird/common/ospf.conf";

    # Filtres/Fonctions pour BGP
    include "/etc/local/bird/common/bgp-filters.conf";

    # BGP (Livraisons, Transit, Peering)
    include "/etc/local/bird/bird/bgp.conf";

