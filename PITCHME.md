<!-- theme: uncover -->

# openZFS / VTT 2023

[![openzfs logo](img/openzfs.png)](https://openzfs.org)                        [![logo Very Tech Trip 2023](img/vtt-2023.png)](https://verytechtrip.com/)


---

# Témoignages

---

# 🧑‍🦰

**Pour des images de VM**

> Dans une infra constituée de machines virtuelle il faut un espace de stockage avec de bonne performances sur des fichiers de grosse taille.

_- Camille, système virtualisés_

---

# 🧑🏿

**Des données brutes**

> On collecte de très grosse quantité de donné brutes du même type, un système idéal serait optimisé pour tirer partit de cette similarité des données.

_- Ali, traitement d'images_

---

# 🧑🏼‍🦲

**Pour de la base de donnée**

> Nos bases de données ont besoin d'un stockage performant pour répondre au plus vite aux utilisateurs, réaliser des sauvegarde ne doit pas se faire au détriment du service

_- Alex, DBA_

---

# 👨🏾‍🦱

**Construire un process de sauvegarde**

> Nos processus de sauvegarde utilise des _snapshot_ gère le chiffrement de bout en bout ou à certaines étapes dans certains cas. Gérer des pétaoctets n'est pas un problème.

_- Nat, équipe archivage_

---

# 🗣️ Qui suis-je ?

---

**🗣️ Qui suis-je ?**

🐔 🚑️ soigneur de pool ZFS chez OVHcloud depuis 2020 `VU.ops`/`PU.storage`

* 👪 père de famille
* 🛠️ construction et usage des outils
* 🐍 communauté francophone Python ([AFPy](http://afpy.org/))


---

**🔊 De quoi va-t on parler 🔊**

* 🔍 C'est quoi ZFS
* 💡 Principaux concepts ZFS
* 🛠️ Usages et choix chez OVH
* 💩 Faites gaffe quand même…

---

# 🔍 C'est quoi ZFS

* Gestionnaire de volume ET système de fichiers
* Stockage en _pool_
* _Copy-On-Write_
* Usage agressif de _cache_
* Administration simple

---

**📝 Historique**

- **2001**: **Naissance** chez Sun
- **2005**: Le **code source** de ZFS est **publié**
- **2008**: ZFS est publié dans **FreeBSD 7.0**
- **2010**: Rachat **Oracle** arrêt contributions ZFS
- **2010**: **Illumos** successeur d'OpenSolaris
- **2013**: Naissance **OpenZFS**
- **2020**: ZFS 2.0 Fusion du code **FreeBSD/Linux**

---

**💾 Gestion disques**

_volume_              vs.            _pool_

![](img/manager-vol.png)            ![](img/manager-pool.png)

---

# 💡 Principaux concepts ZFS

---

**💾 `VDEV`**

![](img/vdev.png)  

-> Virtual DEVice
* _mirror_
* _RAID-Z_
* _spare_
* Log / Cache

---

**🐔 Pool**

![](img/pool.png)

* Contient les `VDEVs`
* Peut s'agrandir +++
* Maintenance préventive
* Contient des _datasets_

---

**🗄️ Dataset**

![](img/dataset.png)

* File system, snapshot, clone, …
* Gigogne/arborescent avec héritage
* Propriétés: Reservation, Quota, Compression, dedup°, ACLs, perso, etc.

---

**⚡ Cache**

- L1ARC -> RAM
- L2ARC -> disque
- ZIL -> disque

---

**🎆 Copy-On-Write**

* ✅ Modèle transactionnel toujours cohérent (pas de FSCK, jamais)
* 📸 Snapshoting
* 🔁 Send / receive

---

**🤓 Administration simple**

* Actions à chaud/online
* 2 commandes `zpool` / `zfs`
* Délégation de droit: `zfs allow <user> <perm> <dataset>`

---

![](img/200-ovhcloud.png)  

#❓ 🤔

---

![](img/200-ovhcloud.png)  

* _Baremetal_
* _Digital core_ (Databases)
* _Storaqe_

---

_Baremetal_

* mirroirs d'image netboot (legacy)
* mirroirs d'image d'installation
    * Debian
    * 180T / 6TB 7200RPM SAS 12Gbps 256MB Cache
    * 1 scrub mensuel (1 jour)

---

_Storage_: produits

![Storage volume overview](img/202211-storage_overwiew.png)

---

_Storage_: backend

* DB zabbix / compression / mirroir / baremetal 2-3T
* serveur borg -> snap locaux  / petit volume / (RBX/BHS/SBG)
* ~128 VM
* rotation `zfs-autosnapshot`

---

`zfswatchd`

* 26/6/2016
* demon multi OS en python
* plusieurs vecteurs SMART, ZFS, OS spécifique
* pro-actif
* monitoring d'événement

---

_Helpdesk_: laptop sous linux/freeBSD

* et non…  😭

---

# 💩 Faites gaffe quand même…

---

[Gandi - Postmortem: September 30 storage incident](https://news.gandi.net/en/2020/10/postmortem-september-30-storage-incident/)

> 30/09/2020 @ 05:38 UTC, one of our storage units went down.
>
> 30/09/2020 @ 11:52 UTC we managed to bring the storage unit back online.

➡️  Erreur humaine: HDD -> ZIL (SSD)

---

**LTT - Our data is GONE... Again**

[![LTT - Our data is GONE Again - thumbnail](img/ltt-zfs-post_mortem.jpg)](https://www.youtube.com/watch?v=Npu7jkJk5nM)

➡️ Erreurs humaines

---

**Et enfin…**

# 🧑

> J’ai encore beaucoup de choses à apprendre, mais j’ai vu une présentation qui m’a expliqué les bases de ZFS. L'outil n'est pas magique, mais permet d'adresser plein de problématiques de stockage: **j'ai envie d'essayer 🛠️ 🚀**

_- Vous !_

---

# 🤝 Références & merci

- [Matt Ahrens](https://openzfs.org/wiki/User:Mahrens) & [George Wilson]() pour: [OpenZFS Basics at SCALE16x, March 2018](https://www.youtube.com/watch?v=MsY-BafQgj4)
- [Ubuntu — An overview of ZFS concepts](https://manpages.ubuntu.com/manpages/lateiist/en/man8/zfsconcepts.8.html)
- [FreeBSD Handbook — The Z File System (ZFS)](https://docs.freebsd.org/en/books/handbook/zfs/)
- [Things Nobody Told You About ZFS](http://nex7.blogspot.com/2013/03/readme1st.html)
- _PU.storage team_

---

# Merci !

---

# ⁉️ Questions , remarques, réclamations, etc.
