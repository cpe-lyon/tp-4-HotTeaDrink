# **TP 4 - Gestion des paquets**

- [**TP 4 - Gestion des paquets**](#tp-4---gestion-des-paquets)
  - [Exercice 1. Commandes de base](#exercice-1-commandes-de-base)
  - [Exercice 2](#exercice-2)
  - [Exercice 3](#exercice-3)
  - [Exercice 4](#exercice-4)
  - [Exercice 5](#exercice-5)

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

TODO demander ou est l'erreur dans l'enoncer
