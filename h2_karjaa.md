# h2 Karjaa tehtävä

Cattle, not pets.

x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
Slater 2017: What is the definition of "cattle not pets"?. (Vain tuo yksi vastaus DevOps Stack Exchangen kysymykseen)

Karvinen 2017: Vagrant Revisited – Install & Boot New Virtual Machine in 31 seconds (Suosittelen koneeksi 'vagrant init debian/bullseye64')

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves

a) Asenna Vagrant. (Toiminee parhaiten isäntäkäyttöjärjestelmässä, siis siinä, joka pyörii raudalla)

b) Yksi maankiertäjä. Asenna yksi kone Vagrantilla, ota siihen SSH-yhteys, osoita että netti toimii.

c) Oma orjansa. Asenna Salt herra ja orja samalle koneelle.

d) Asenna Saltin herra-orja arkkitehtuuri toimimaan verkon yli.

e) Aja useita idempotentteja (state.single) komentoja verkon yli.

f) Kerää teknistä tietoa orjista verkon yli (grains.item)

g) Aja shell-komento orjalla verkon yli.

h) Hello, IaC. Tee infraa koodina kirjoittamalla /srv/salt/hello/init.sls. Aja tila jollekin orjalle. Tila voi esimerkiksi tehdä esimerkkitiedoston johonkin hakemistoon. Testaa toisella komennolla, että pyytämäsi muutos on todella tehty.

# Vastaukset:

x) "Cattle not pets" viittaa siihen että palvelimia on parempi kohdella karjana eikä lemmikkeinä. Palvelimiin ei saa kiintyä liikaa vaan ne pitää olla korvattavia ja helposti alas ajettavia tarvittaessa.

a) 
Ladataan vagrant virallisilta Vagrantin [sivuilta](https://developer.hashicorp.com/vagrant/downloads) ja asennetaan oikea versio tietokoneelle. Minun tapauksessa Mac OS AMD64 arkkitehtuurille. Kokeillaan asennuksen jälkeen terminaalissa että onnistuiko asennus. Kokeillaan komentoa 'vagrant'. Komento otettu Vagrantin virallisilta [sivuilta](https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-install)

![Näyttökuva 2023-11-1 kello 16 18 32](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/4fd4e185-f7cf-4f73-a18f-d5412cbd9a23)
Näyttäisi onnistuvan.

***

b) 
Asennetaan Vagrantilla yksi kone ja otetaan siihen yhteys. Käytetään komentoja [Teron sivuilta](https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/) Ensiksi komento 'vagrant init debian/bullseye64' sitten 'vagrant up'.

![Näyttökuva 2023-11-1 kello 17 20 31](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/e264bebb-05e7-423c-97c8-b8e638b34115)
VirtualBoxiin ilmestyi uusi virtuaalikone.

Tämän jälkeen otetaan koneeseen yhteys komennolla 'vagrant ssh'

![Näyttökuva 2023-11-1 kello 17 22 52](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b4cdf205-3714-4769-aeff-9f94a6474a50)
Yhteys näyttäisi toimivan.

Lopuksi vielä poistetaan virtuaalikone komennolla 'vagrant destroy'.

***

c)
Asennetaan salt herra ja orja yhdelle koneelle. Käytetään komentoja 'sudo apt-get update' ja 'sudo apt-get install salt-minion'. Kokeillaan toimivuutta komennolla '$ sudo salt-call --local -l info state.single pkg.installed tree'

![Näyttökuva 2023-11-1 kello 17 56 06](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/5c286b44-bede-41d5-b8a6-b5934b9e174d)

***

d)
Ensiksi etsin Vagrantfilen ja poistan sieltä default konfigutaatiot. Sitten copypastean tilalle [Teron sivulta](https://terokarvinen.com/2023/salt-vagrant/) otetun konfiguraation kahdelle orjalle ja yhdelle herralle. Ja tämän jälkeen ajoin Terminal-komennon 'vagrant up' jotta koneet lähtevät käyntiin.

![Näyttökuva 2023-11-1 kello 18 06 21](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b01389c3-524a-40bd-9b3c-d13a69903e39)

Otetaan yhteys 'vagrant ssh tmaster' ja toimitaan aikaisempien ohjeiden mukaisesti. Vastaanotetaan avaimet.

![Näyttökuva 2023-11-1 kello 18 09 59](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/816e3945-22c0-4d12-92dd-b0f9c68be9c1)

Kokeillaan vielä yhteys komennolla '$ sudo salt '*' test.ping'
![Näyttökuva 2023-11-1 kello 18 11 59](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/2d88eaa2-a439-46c1-9fb0-4bb2b98a80d7)


## LÄHTEET
Download Vagrant: https://developer.hashicorp.com/vagrant/downloads

Install Vagrant tutorial: https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-install

Github, Basic writing an formatting syntax: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

Vagrant Tutorial | How to Setup a Basic Vagrant VM | 10-Minute Tutorials: https://www.youtube.com/watch?v=AlRejC0lIGk
