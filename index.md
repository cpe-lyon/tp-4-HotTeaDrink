# Exercice 1. Commandes de base

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