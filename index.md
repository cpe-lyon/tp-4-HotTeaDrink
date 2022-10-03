# **TP 4 - Gestion des paquets**

- [**TP 4 - Gestion des paquets**](#tp-4---gestion-des-paquets)
  - [Exercice 1. Commandes de base](#exercice-1-commandes-de-base)
  - [Exercice 2](#exercice-2)
  - [Exercice 3](#exercice-3)
  - [Exercice 4](#exercice-4)
  - [Exercice 5](#exercice-5)
  - [Exercice 6](#exercice-6)
  - [Exercice 7](#exercice-7)
  - [Exercice 8](#exercice-8)
    - [Creation d un paquet Debian avec dpkg-deb](#creation-d-un-paquet-debian-avec-dpkg-deb)
    - [Creation dossier personnel](#creation-dossier-personnel)
    - [Signature du dépôt avec GPG](#signature-du-dépôt-avec-gpg)

## Exercice 1. Commandes de base

1. Il suffit d'utiliser la commande suivante:

```BASH
sudo apt update && sudo apt upgrade
```

2. Pour crée cet alias de façon permanente, il faut allez modifier le fichier **.bashrc**.  
Dans ce fichier il faudra crée une section a la fin de celui-ci qui sera dédier à nos alias personnalisé.  

```BASH
# My custom aliases
alias maj="sudo apt update && sudo apt upgrade"
```

Apres cela, il faut mettre à jours le fichier à l'aide de:

```BASH
source ~/.bashrc
```

3. Les 5 derniers paquets installés était:

- libc-bin:amd64
- initramfs-tools:all
- install-info:amd64
- dbus:amd64
- man-db:amd64

4. Pour cela il faut allez regarder dans le fichier **/var/log/apt/history.log**. Pour cela, la commande suivante permet de visualisé imédiatement les commandes apt utilisé.

```BASH
grep " install " /var/log/apt/history.log
```

5. A l'aide de la commande suivante on obtient **625** paquet installé:

```BASH
sudo dpkg-query -l | wc -l
```

Et on obtient **618** paquet à l'aide de la commande suivante:

```BASH
sudo apt list --installed | wc -l
```

La petite différence de comptage entre apt et dpkg s'explique il y a des lignes warning que le wc -l compte

6. Il y a actuelement 69053 disponible.

```BASH
sudo apt list | wc -l
```

7. Glaces permet de d'obtenir des infos sur les processus en cours ainsi que les performances du pc.  
Tldr sert a raccoursir les pages de manuel en affichant des exemples.  
Hollywood permet de montrer un pc de Hacker comme vu par hollywood.

8. Il y a le **paquet sudoku** qui le permet.

## Exercice 2

La commande **ls** est installé à partir du paquet **coreutils**. Pour pouvoir trouver cela en une seule commande il suffit de tapper la commande suivante:

```BASH
dpkg -S /bin/ls
```

Le script demander est le suivant:

```BASH
#!/bin/bash

paquet=$(dpkg -S /bin/$1)

echo "$paquet"
```

## Exercice 3

```BASH
#!/bin/bash

test=$(dpkg -l $1) 

if [ $? -eq 0 ]
then
        echo "INSTALLÉ"
else
        echo "NON INSTALLÉ"
fi
```

## Exercice 4

On peut afficher les programmes à l'aide de la commande suivante:

```BASH
dpkg -L coreutils
```

Le paquet **[** correspond a un synonyme de test.

## Exercice 5

Emac et lynx sont tous deux des navigateur internet qui fonctionne dans un terminal

## Exercice 6

2. Le fichier contient les répositoris suivants:

```BASH
deb https://ppa.launchpadcontent.net/linuxuprising/java/ubuntu/ jammy main
# deb-src https://ppa.launchpadcontent.net/linuxuprising/java/ubuntu/ jammy main
```

## Exercice 7

## Exercice 8

### Creation d un paquet Debian avec dpkg-deb

2.

```BASH
Package: origine-commande #nom du paquet
Version: 0.1 #numéro de version
Maintainer: Foo Bar #votre nom
Architecture: all #les architectures cibles de notre paquet (i386, amd64...)
Description: Cherche l'origine d'une commande
Section: utils #notre programme est un utilitaire
Priority: optional #ce n'est pas un paquet indispendable
```

### Creation dossier personnel

3.

```BASH
Origin: Moua
Label: Command Origines
// Suite: stable
Codename: jammy
Architectures: i386 amd64
Components: universe
Description: Yummy
```

5.

```BASH
User@localhost:~/repo-cpe$ reprepro -b . includedeb jammy packages/origine-commande.deb
Exporting indices...
User@localhost:~/repo-cpe$ 
```

6.

 ```BASH
 deb file:/home/User/repo-cpe jammy universe
 ```

7.

 ```BASH
User@localhost:~$ sudo apt update 
Get:1 file:/home/User/repo-cpe jammy InRelease
Ign:1 file:/home/User/repo-cpe jammy InRelease
Get:2 file:/home/User/repo-cpe jammy Release [1,676 B]
Get:2 file:/home/User/repo-cpe jammy Release [1,676 B]
Get:3 file:/home/User/repo-cpe jammy Release.gpg
Ign:3 file:/home/User/repo-cpe jammy Release.gpg
Hit:4 https://ppa.launchpadcontent.net/linuxuprising/java/ubuntu jammy InRelease
Hit:5 http://us.archive.ubuntu.com/ubuntu jammy InRelease
Hit:6 http://us.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:7 http://us.archive.ubuntu.com/ubuntu jammy-backports InRelease
Hit:8 http://us.archive.ubuntu.com/ubuntu jammy-security InRelease
Reading package lists... Done
N: Download is performed unsandboxed as root as file '/home/User/repo-cpe/dists/jammy/InRelease' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)
E: The repository 'file:/home/User/repo-cpe jammy Release' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
User@localhost:~$ 
 ```

### Signature du dépôt avec GPG

1.

 ```BASH
User@localhost:~$ gpg --gen-key
gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Note: Use "gpg --full-generate-key" for a full featured key generation dialog.

GnuPG needs to construct a user ID to identify your key.

Real name: teapot
Email address: teapot@warm.tea
You selected this USER-ID:
    "teapot <teapot@warm.tea>"

Change (N)ame, (E)mail, or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/User/.gnupg/trustdb.gpg: trustdb created
gpg: key E1EF19A1ACB82F86 marked as ultimately trusted
gpg: directory '/home/User/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/User/.gnupg/openpgp-revocs.d/D7CBD6895D0AC5B9563C77D0E1EF19A1ACB82F86.rev'
public and secret key created and signed.
 ```
