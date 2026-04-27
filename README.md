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

## Mise en place du MFA

### Activation de la fonctionnalité

```
> System
> Advanced Settings
> Dans l'onglet Global Two Factor Authentication, cliquer sur Configure
> Cocher  Enable Two Factor Authentication Globally
> Save
```

### Génération du code

```
En haut à droite, cliquer sur Truenas_admin
Two Factor authentification
Copier le code qui se trouve en bas du QR Code

Ouvrir le widget Bitwarden et se connecter au compte bitwarden d'un utilisateur qui a les droits admin
Créer
Identifiant
    Nom d'utilisateur : truenas_admin
    Mot de passe : P@ssword*
    Clé d'autentification : saisir la clé copiée précédemment
    Site Web Uri : https://truenas2.bts.lan
    Enregistrer
```

## Mettre en français

```
> System
> General Settings
> Sur le champs Localization, cliquer sur Configure
    >  Language : French
    > Console Keyboard Map : French (Azerty)
    > Timezone : Europe/Paris
    > Format : dd-mm-yy
    > Save 
```

## Création d'un certificat auto-signé



### Étape 1 — créer un certificat

```
Dans TrueNAS :

Idendifiants
Certificats

Dans le champs Autorité de cerification, cliquer sur Ajouter
    Nom :  CA-INT-bts
    Type : AC Interne
    Profil : CA
    Cocher la case Ajouter au magasin de confiance
    Suivant
    Typé de clé : RSA
    Longueur de la clé : 2048
    Algorythme Digest : SHA256
    Durée de vie : 365
    Suivant
    Pays : France
    Etat : Ile-De-France
    Localité : Paris
    Organisation :Imie
    Email : admin@bts.lan
    Nom commun : truenas2.bts.lan
    Nom alternatif de sujet: 
        192.168.60.40
        truenas2.bts.lan
    Suivant
    Usage : SERVER_AUTH
    Laisser cocher les deux champs
    Key Usage COnfig : Laisser tel quel
    Suivant
    Enregistrer

Dans le champs certifiats, cliquer sur Ajouter
    Nom : truenas-cert
    Type : certificat interne
    Profil : HTTPS RSA Certificate
    Cocher la case Ajouter au magasin de confiance
    Suivant
    Normalement les champs sont pré-remplis, sauf la durée de vie où on va mettre 365
    Suivant
     Pays : France
    Etat : Ile-De-France
    Localité : Paris
    Organisation :Imie
    Email : w.mbakoptchouhane@gmail.com
    Nom commun : truenas2.bts.lan
    Nom alternatif de sujet: 
        192.168.60.40
        truenas2.bts.lan
    Suivant x2
    Enregistrer

    Télécharger le certficat d'AUTORITE créé
    Sur un client windows :
        Une fois créer, cliquer sur le fichier. crt et k'installer (Attention: ordinateur local)
    Sur un client linux : Aller dans le navigateur, parametre, vie privée et sécurité, dans la zone certificats, cliquer sur afficher les certificats et cliquer sur importer. Ensuite important le fichier .crt


Aller Dans Système
Paramètres généraux
Cliquer sur Paramètres dans la zone UI
Certificate SSL GUI : Sélectionner truenas_cert
Enregistrer
Dans la pop-up qui s'affiche, redémarrer les services
```

    
