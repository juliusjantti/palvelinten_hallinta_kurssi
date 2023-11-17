# Tehtävä 4 Demoni

x) x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves, vain kohdat
Infra as Code - Your wishes as a text file
top.sls - What Slave Runs What States
Salt contributors: Salt overview, kohdat
Rules of YAML
YAML simple structure
Lists and dictionaries - YAML block structures
Salt contributors: Salt states, kohdat
State modules
The state SLS data structure
Organizing states
The top.sls file
Create the SSH state, Create the Apache state
Katso näitä alakohtia kriittisin silmin. Teron huomioita ja suosituksia:
Namevar: itse asia tilan id:ksi, name arvoksi tulee automaattisesti sama
Puuttuko esimerkeistä service-watch? Jos asetustiedosto päivittyy herralla, tuleeko se koskaan käyttöön orjilla?
Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port
Käytä omaa sshd_config:ia pohjana. Tässä on jonkun toisen Linux-version tiedosto.

x) Vastaukset

***

## a) Hello SLS! Tee Hei maailma -tila kirjoittamalla se tekstitiedostoon, esim /srv/salt/hello/init.sls.

a) vastaus

Ensiksi luodaan /srv/salt tiedostoon uusi hakemisto komennolla 'mkdir hello' ja lisätään sinne tiedosto komennolla 'sudoedit init.sls'. Lisätään tiedostoon oheinen teksti:

![Näyttökuva 2023-11-17 kello 16 23 51](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/91de4898-0c6c-40de-b99d-801f0b903811)

Kokeillaan toimiiko tilan luominen komennolla 'sudo salt '*' state.apply hello'

![Näyttökuva 2023-11-17 kello 16 26 37](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/d6387b94-ab42-469a-a426-e51d5b8ff21f)

Komento näyttäisi toimivan. Käydään vielä katsomassa /srv/salt hakemistosta ilmestyikö sinne tiedosto.

![Näyttökuva 2023-11-17 kello 16 27 26](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/773c9338-56ae-49c2-bf46-819e93559cf2)

Näyttäisi toimivan. 

(ps kirjoitin tämän kohdan jo kerran mutta onnistuin poistamaan koko tehtävän joten tämä uudelleenkirjoitus on hieman karkeampi.)


