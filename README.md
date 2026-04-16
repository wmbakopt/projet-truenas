## Installation

**Iso : TrueNAS 25.04.2.6**

- Version stable (release)
- Basée sur la branche actuelle recommandée pour la production
- Correctifs de bugs et stabilité
- Compatible avec la majorité des configurations
- Moins de risques de problèmes


1 Disque de 60 Go
2 disques de 80 Go Chacun


```
> Install / Upgrade
> Sélectionner le disque de 60 Go
> Yes
> Administrative user (truenas_admin).
> Mot de passe : toto
> Yes x2
> Laisser l'instalation se terminer
> Sélectionner Reboot System et valider
```

## configuration statique de l'adresse IP

```
> Sélectionner 1 + Entrée
    Entrée
    Ipv4_dhcp : Mettre NO
    Ipv6_auto : Mettre NO
    Alias : Mettre 192.168.60.40/24
    Save
    Appuyer sur p puis a

> Sélectionner Option 2  + Entrée
    Hostname : truenas2
    Domaine : bts.lan
    ipv4 gateway : 192.168.60.254
    nameserver : 192.168.60.10
    Save
```

## Enregistrement de la VM dans le DNS sur le serveur AD

Le faire sur la vm svrad22


## Accès à l'interface Web de Truenas

```
Sur la vm zabbix2, ouvrir le navigateur et rentrer https://truenas2.bts.lan
    Avancé
    Continuer vers truenas.bts.lan (non sécurisé)
    Identifiant : truenas_admin
    Mot de passe : toto
```


    
