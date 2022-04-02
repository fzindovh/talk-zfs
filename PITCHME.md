<!-- theme: uncover -->

# Histoires d'un sysadmin perfectionniste sous pression

_2 avril 2022 - Frédéric Zind - JDLL (Lyon)_

![logo JDLL 2022](img/jdll-2022.jpg)

---

## Découvrez openZFS : un stockage fiable, puissant et accessible.

![openzfs logo](img/openzfs.png)

---

# 👨 Qui suis-je ?

* 🔧 2000: technicien en mécanique
* 🐍 2018: apprenti charmeur de serpent
* 🧰 2019: dev django
* 🚑️ 2020: Soigneur de _pool_ ZFS (sys admin)

---

# 🔍 C'est quoi ZFS

* Gestionnaire de volume ET système de fichiers
* Stockage en _pool_
* _Copy-On-Write_
* Usage agressif de _cache_ (la RAM)
* Administration simple

---

# 💾 Gestion traditionnelle

![](img/manager-vol.png)

---

# 📀 Gestion par pool

![](img/manager-pool.png)

---

### 📝 Historique

- 2001 : Naissance chez Sun
- 2005 : Le code source de ZFS est publié.
- 2008 : ZFS est publié dans FreeBSD 7.0.
- 2010 : Oracle rachète SUN, arrête de contribuer à ZFS.
- 2010 : illumos successeur d'OpenSolaris
- 2013 : Naissance OpenZFS.
- 2020 : Fusion codebase FreeBSD + Linux

---

# 💡Quelques concepts

---

# 💾 vdev

![](img/vdev.png)

---

## 💾 vdev

- miroir
- _RAID-Z_
- _spare_ (chaud ou froid)
- Log (ZIL)
- Cache (L2ARC)

---

# 🐔 Pool

![](img/pool.png)

---

## 🐔 Pool

* Gere les disques
* Peut s'agrandir +++
* Maintenance préventive
* Contient des _datasets_

---

# 🗄️ Dataset

![](img/dataset.png)

---

## 🗄️ Dataset

* File system, snapshot, clone, …
* < 2^48 datasets / pool
* Gigogne/arborescent avec héritage
* Propriétés
    - Reservation / Quota (dataset/reference)
    - Compression, deduplication
    - ACLs, personalisé `:`, …

---

# ⚡ Cache

- ARC
- L2ARC

---

# 🎆 Modèle d'objet transactionnel

* Copy-On-Write
    - Toujours cohérent sur le disque (pas de FSCK, jamais)
* Snapshoting
* Send / receive
    - Expedition de snapshots
    - Unidirectionnel
    - Redémarable

---

# 🤓 Administration simple

* Administration a chaud/online
* 2 commandes:
    - `zpool`: pool
    - `zfs`: filesystems
* Delegation

---

# 🤝 Communauté

* code base unique: FreeBSD / Linux
- macOS©®
- Windows©®

---

# ⚠️ Nota bene

* ZFS 💚 RAM
* vdev = IOPS ou stockage
* snapshots != sauvegardes
* compression coute moins cher que la déduplication
* Ce n'est pas parce que c'est possible qu'il faut le faire
* Pas de magie !

---

# 💩 Faites gaffe quand même…

[Gandi - Postmortem: September 30 storage incident](https://news.gandi.net/en/2020/10/postmortem-september-30-storage-incident/)

> 30/09/2020 @ 05:38 UTC, one of our storage units went down.
>
> 30/09/2020 @ 11:52 UTC we managed to bring the storage unit back online.

➡️ Erreur humaine: HDD -> ZIL (SSD)

---

# 💩 Faites gaffe quand même…

**LTT - Our data is GONE... Again**

[![LTT - Our data is GONE Again - thumbnail](img/ltt-zfs-post_mortem.jpg)](https://www.youtube.com/watch?v=Npu7jkJk5nM)

➡️ Erreurs humaines

---

# Merci !

---

# ⁉️ Questions , remarques, réclamations, etc.

![QRcode](img/qrcode-pro.zind.fr.png)

http://pro.zind.fr

---

# 🤝 Références & merci

* [Matt Ahrens](https://openzfs.org/wiki/User:Mahrens) & [George Wilson]() pour: [OpenZFS Basics at SCALE16x, March 2018](https://www.youtube.com/watch?v=MsY-BafQgj4)
* [Ubuntu — An overview of ZFS concepts](https://manpages.ubuntu.com/manpages/lateiist/en/man8/zfsconcepts.8.html)
* [FreeBSD Handbook — The Z File System (ZFS)](https://docs.freebsd.org/en/books/handbook/zfs/)i
* [Things Nobody Told You About ZFS](http://nex7.blogspot.com/2013/03/readme1st.html)
* _PU.storage team_
