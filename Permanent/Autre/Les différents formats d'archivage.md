---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet: Archivage
tags: []
---

Pour l'archivage de fichiers, il existe de nombreux formats libres, tels que ZIP, TAR (TAR+GZIP, TAR+BZIP2, TAR+XZ, TAR+ZTSD) ou bien 7ZIP qui sont des logiciels libres, multi-OS et qui garantissant la pérennité des données. Cependant, il existe aussi des formats propriétaires ou bien non-documentés. Ces formats sont souvent liés à un logiciels propriétaire, généralement mono-OS, et ne garantissent pas la pérennité des données.

# L'utilisation de `ZIP`

`ZIP` permet la compression de chaque fichier indépendemment aux autres ce qui avantage la rapidéité d'extraction d'un fichier seul et moins de compression. Cependant, il n'archive pas les fichiers spéciauxu Unix/Linux et n'archive pas tous les attributs Unix/Linux

# L'utilisation de `TAR + LOGICIEL_COMPRESSION`

L'utilisation de `TAR` permet d'adoper une philosophie Unix qui permet de séparer chaque fonction dans un utilitaire précis. Il va également assurer l'archivage y compris les fichiers spéciaux et attributs Unix/Linux

Il y a plusieurs options de `tar` :

- `c` : Create
- `x` : Extract
- `v` : Verbose
- `f` : Fichiers

