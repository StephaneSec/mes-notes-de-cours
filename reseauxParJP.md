# Réseau - Notes

## Marionett

* Logiciel un peu galère : peut planter et corrompre les savegardes
* Sauvegarder régulièrement **en changeant de nom**.


## Configuration réseau Debian

* Pour configurer une interface, écrire dans `/etc/network/interfaces` :

        auto eth0
        iface eth0 inet static
          address 192.168.1.1
          netmask 255.255.255.0
          gateway 192.168.1.254
        iface eth0 inet6 static
          address 2001:660:7101:0017:1::1
          netmask 80
          gateway 2001:660:7101:0017:1::abcd

puis lancer `service networking restart`.


* Pour activer le *port forwarding*, décommenter dans `/etc/sysctl.conf/` :

        net.ipv4.ip_forward=1
        net.ipv6.conf.all.forwarding=1

puis recharger avec `sysctl -p`.


* Pour ajouter une route, dans `/etc/network/interfaces`:

        up route add -net 10.10.0.0 netmask 255.255.255.0 gw 192.168.2.2


### Routage dynamique IPv6

Pour configurer RIP-NG, ajouter dans `/etc/quagga/ripngd.conf` :

    network eth2
    route 2001:660:7101:17:0/64
    distribute-list local-only out eth2

Puis dans `/etc/quagga/daemons` :

    ripngd=yes

Enfin, lancer la commande `service quagga restart`.

### La commande `iptables`

Pour interdir le trafic entrant par défaut :

    # iptables -P INPUT DROP


Pour autoriser le routage :

    # iptables -P FORWARD ACCEPT


Pour autoriser l’interface de loopback :

    # iptables -I INPUT 2 -i lo -j ACCEPT


Pour autoriser le retour des communications établies par l’utilisateur

    # iptables -A INPUT -m state --state ESTABLISHED -j ACCEPT


Pour autoriser le trafic entrant sur un port :

    # iptables -A INPUT -p tcp -i eth0 --dport ssh -j ACCEPT


Pour autoriser ICMP :

    iptables -A OUTPUT -p icmp -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
    iptables -A INPUT -p icmp -j ACCEPT



