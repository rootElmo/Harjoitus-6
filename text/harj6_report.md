# Harjoitus 6

## Ihan aluksi

Tässä harjoituksessa tavoitteena on oppia käyttämään muotteja, kun hallittavana on koneita, joissa pyörii useampi eri Linuxin levityspaketti. Tehtävää varten asensin itselleni uuden 64-bittisen Xubuntu orja-koneen, sekä 64-bittisen CentOs orja-koneen. Käytin Xubuntu-koneen konffaamiseen luomaani [Agent-Setter-skriptiä.](https://github.com/rootElmo/Agent-Setter) Asensin CentOsin käsin, sillä en ole aikaisemmin käyttänyt kyseistä levityspakettia.

Asennellessani Centosia kokeilin olisiko Xubuntu-koneeni tavoitettavissa normaalisti ajamalla komennon

	sudo salt 'e009' cmd.run 'whoami'

![scrshot1](../images/scrshot001.png)

Homma pelittää tähän asti.

Minulla oli pitkään vaikeuksia CenOS:in asennuksen kanssa, varsinkin mitä tuli Guest Additionseihin virtuaalikoneella. Käytin [If Not True Then Falsen](https://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/) ohjetta, joka toimi. Jouduin myös päivittämään VM VirtualBox ohjelmiston.

Asensin tämän jälkeen salt-minionin CentOS-koneelle [tämän ohjeen mukaan](https://repo.saltstack.com/#rhel).

Tyhjensin CentOS-koneelle salt-minionin asennuksessa luodun _minion_-tiedoston, kirjoitin sinne herra-koneen IP:n, sekä koneelle tunnuksen **cElmo001**.

	cElmo001 # cd /etc/salt/
	echo "" | tee minion

_minion_-tiedoston sisältö:

	id: cElmo001
	master: 192.168.1.103

Hyväksyin cElmo001:n herra-koneella komennolla

	master $ sudo salt-key -A

![scrshot2](../images/scrshot002.png)

Seuraavaksi testasin saltin kautta, onko minulla oikeasti yhteys molempiin asentamiini koneisiin tällä hetkellä:

	master $ sudo salt '*' cmd.run 'whoami'

Ja molemmat kertoivat olevansa root!

![scrshot3](../images/scrshot003.png)

## Lähteet

If Not True Then False: https://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/
