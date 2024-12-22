---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet: Stockage
tags: []
---

Il y a des noms utilisés par les logiciels de manipulation des disques et partitions. Le répertoire `/dev/` contient les pseudos-fichiers représentant les disques et les partitions. On parle de _périphérique bloc_. Les périphériques SATA et USB sont `/dev/sda`, `/dev/sdb` ... Périphériques NVMe : `nvme0n1` ... Partitions : `sda1` ...

Il existe des commandes pour observer les disques et les partitions :

- `lsblk` (**list block device**) : Visualiser les périphériques de stockage et les partitions
- `blkid` (**block devices attribute**) : Visualiser des détails sur les partitions
- `df` (**disk free**) ⇒ Logiciel de base : Visualiser l'espace disque total, occupé, libre
  `-h` pour une lecture plus facile
- `mount` : Visualiser les montages

cf [[Les différents types d'interfaces de stockage pour les machines personnelles]]
