<!-- theme: uncover -->

# Histoires d'un sysadmin perfectionniste sous pression

_3 avril 2022 - Frédéric Zind - JDLL (Lyon)_

![logo JDLL](img/jdll.jpg)

##

![openzfs logo](img/openzfs.png)

---

# 👨 Qui suis-je ?

* 🔧 2000: technicien en mécanique
* 🐍 2018: apprenti charmeur de serpent
* 🧰 2019: dev django
* 🚑️ 2020: Soigneur de _pool_ ZFS (sys admin)

---

# C'est quoi ZFS

- Stockage en _pool_
    * Fonctionnalité de système de fichiers + gestionnaire de volume en un seul
    * Les systèmes de fichiers allouent et libèrent l'espace du _pool_
- Modèle d'objet transactionnel
    * Toujours cohérent sur le disque (pas de FSCK, jamais)
    * Universel - fichier, bloc, NFS, SMB, iSCSI, FC, …
- Intégrité des données de bout en bout
    * Détection et correction de la corruption silencieuse des données
- Administration simple
    * Exprimer l'intention de manière concise
    * Structures de données évolutives

---

# 🔀 Différences

- combine gestionnaire de volume et système de fichiers
    * conscient de la structure sous-jacente des disques
    * RAID: plusieurs disques mais OS n'en voit que 1
- Pool
    * gere les disques
        - peut s'agrandir
        - maintenance préventive
    * contient des système de fichiers (_datasets_)
        - possède des propriétés
- Systèmes de fichiers séparés vs système de fichiers monolithique.
- Copy-on-write

---

# 📝 Histoire

- 2001 : le développement commence avec 2 ingénieurs
- 2005 : Le code source de ZFS est publié.
- 2008 : ZFS est publié dans FreeBSD 7.0.
- 2010 : Oracle cesse de contribuer au code source de ZFS.
- 2010 : illumos successeur d'OpenSolaris
- 2013 : ZFS open-source se regroupe pour former OpenZFS.
- 2014 : OpenZFS pour Mac OS X
- 2020 : OpenZFSv2 FreeBSD + Linux

---

# 💡Concepts:

- Copy-On-Write
- Dataset
    * file system (monté localement)
    * volume
    * snapshot
    * clone
* Reservation / Quota (dataset/reference)
* Compression
* Deduplication
* Copies
* Checksum
* Scrub

- Cache: ARC = MFU & MFU vs LFU
- ZIL
- vdev:
    * miroir
    * _RAID-Z
    * _spare_ (chaud ou froid)
    * Log (ZIL)
    * Cache (L2ARC)
Resilver
Status
    Online
    Offline
    Faulted
    Degraded

- Feature Flags

---


# ⚠️

- ZFS 💚 RAM
- vdev = IOPS ou stockage
- compression coute moins cher que la déduplication
- snapshots != sauvegardes
- Ce n'est pas parce que c'est possible qu'il faut le faire
- Pas de magie !

---

# 💩 Faites gaffe quand même…

* [Gandi - Postmortem: September 30 storage incident](https://news.gandi.net/en/2020/10/postmortem-september-30-storage-incident/)
* [LTT - Our data is GONE... Again](https://www.youtube.com/watch?v=Npu7jkJk5nM)

---

# 🤝 Références & merci

* [Matt Ahrens](https://openzfs.org/wiki/User:Mahrens) & [George Wilson]() pour: [OpenZFS Basics at SCALE16x, March 2018](https://www.youtube.com/watch?v=MsY-BafQgj4)
* [FreeBSD Handbook - The Z File System (ZFS)](https://docs.freebsd.org/en/books/handbook/zfs/)
* [Things Nobody Told You About ZFS](http://nex7.blogspot.com/2013/03/readme1st.html)
* PU.storage

---

# Merci !

---

# ⁉️ Questions , remarques, réclamations, etc.

![QRcode](img/qrcode-pro.zind.fr.png)

http://pro.zind.fr
