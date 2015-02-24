
GITOYEN: BIRD configuration for a border router
===============================================

This repository contains the configuration for one of Gitoyen's border router. Configurations is made of:

  * BGP communities management;
  * Traffic delivery (members, clients) management;
  * Peering & transit management.

Feel free to take inspiration from it.

## Contact us

For any question / comment / discussion, you can reach us through:

* mail: contact (AT) gitoyen.net;
* irc: #gitoyen / irc.geeknode.net ;
* www: http://www.gitoyen.net

## Some principles

* Routes imported from a bgp session are tagged with a community according to the bgp peer.
* Routes exported to a bgp session are filtered using communities based on the bgp peer.
  * Examples
    * Routes exported to a transit operater session only contain properly tagged ones (members/clients/internal).
    * Routes exported to a member session are all Internet routes (full-view).

## Structure

    $ cat etc/local/bird/bird.conf 
    # Gitoyen contact (AT) gitoyen.net
    #
    # vim: set ts=4:sw=4

    log syslog all;

    # Router specific configuration
    include "/etc/local/bird/common/local.conf";

    # Filters/Functions common to all protocols
    include "/etc/local/bird/bird/filters.conf";

    # Kernel protocols management
    include "/etc/local/bird/common/kernel.conf";

    # Static routes
    include "/etc/local/bird/bird/static.conf";

    # OSPF (Backbone)
    include "/etc/local/bird/common/ospf.conf";

    # Filters/Functions for BGP
    include "/etc/local/bird/common/bgp-filters.conf";

    # BGP (Delivery, Transit, Peering)
    include "/etc/local/bird/bird/bgp.conf";
