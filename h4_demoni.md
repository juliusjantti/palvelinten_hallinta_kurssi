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

Käytetään apuna Tero Karvisen artikkelia [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file), sekä myös omaan päähän jääneitä viime oppitunnin asioita.

Ensiksi siirrytään /srv/salt hakemistoon ja luodaan uusi hakemisto komennolla 'mkdir hello' ja lisätään sinne uusi tiedosto komennolla 'sudoedit init.sls'. Lisätään tiedostoon oheinen teksti:

![Näyttökuva 2023-11-17 kello 16 23 51](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/91de4898-0c6c-40de-b99d-801f0b903811)

Kokeillaan toimiiko tilan luominen komennolla 'sudo salt '*' state.apply hello'

![Näyttökuva 2023-11-17 kello 16 26 37](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/d6387b94-ab42-469a-a426-e51d5b8ff21f)

Komento näyttäisi toimivan. Käydään vielä katsomassa /srv/salt hakemistosta ilmestyikö sinne tiedosto.

![Näyttökuva 2023-11-17 kello 16 27 26](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/773c9338-56ae-49c2-bf46-819e93559cf2)

Näyttäisi toimivan. 

(ps kirjoitin tämän kohdan jo kerran mutta onnistuin poistamaan koko tehtävän joten tämä uudelleenkirjoitus on hieman karkeampi.)

***

## b) Top. Tee top.sls niin, että tilat ajetaan automaattisesti, esim komennolla "sudo salt '*' state.apply".

b) vastaus

Käytetään taas apuna Tero Karvisen artikkelia [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file)

Luodaan ensiksi /srv/salt hakemistoon top.sls tiedosto komennolla 'sudoedit top.sls'. Alla tiedoston sisältö. Muistetaan että toisella rivillä on ensiksi 2 välilyöntiä, ja kolmannella rivillä 4 välilyöntiä.

![Näyttökuva 2023-11-19 kello 10 11 45](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/96915b75-a74d-4894-80b0-95d7cf6b36cf)

Sitten kokeillaan ajaa 'sudo salt '*' state.apply'komento.

![Näyttökuva 2023-11-19 kello 10 12 35](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/6d3b84b5-c222-4a95-8fb2-893c0e702a10)

Näyttäisi toimivan. Komento ajaa init.sls tiedoston sisältämän tilan. Ja minun tapauksessa se asentaa apache2 paketin ja tarkistaa onko kyseinen paketti käynnissä.

![Näyttökuva 2023-11-19 kello 10 14 57](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/26fa2aa5-a555-4bfa-985b-290af0b4c6c9)

***

## c) Apache. Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy

Otetaan ssh yhteys molempiin orjiin ja katsotaan että apache2 ei ole asennettu kummallekaan.

![Näyttökuva 2023-11-19 kello 10 20 36](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/73f47834-c340-42b5-8a5c-56d43707bcea)

Asennetaan sitten apache2 ensiksi käsin komennolla 'sudo apt-get install apache2' ja katsotaan toimiiko se.

![Näyttökuva 2023-11-19 kello 10 23 04](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/a969e8dd-6168-4615-8523-36cd39fa72c8)

Käydään muokkaamassa apachen aloitussivua index.html hakemistossa /var/www/html/. Muutetaan tiedostoa 'sudoedit index.html' ja lisätään sinne jotain tekstiä.

![Näyttökuva 2023-11-19 kello 10 27 00](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/85eee814-efbf-482c-98ec-7ce03b5ddf70)

Ja sitten kokeillaan toimiiko se komennolla 'curl localhost'. (Jos curl komentoa ei löydy sen voi asentaa komennolla 'sudo apt-get install curl').

![Näyttökuva 2023-11-19 kello 10 27 52](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/219063e3-b6a0-467b-af57-b22e7f0e5057)

Kaikki näyttäisi toimivan käsin tehtynä. Tämän jälkeen poistetaan apache2 komennolla 'sudo apt-get remove apache2', ja siirrytään tekemään aiempi kohta automaattisesti.

Kokeillaan ensiksi toimiiko apache orjilla:

![Näyttökuva 2023-11-19 kello 10 33 21](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b3dcb8b5-84b8-4163-8cc4-f805e0f45a1b)

Negatiivista näyttää.

Siirrytään orjalla /srv/salt/hello hakemistoon muokkaamaan init.sls tiedostoa, ja lisätään sinne seuraavat tekstit.

![Näyttökuva 2023-11-19 kello 10 36 17](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b71658c9-d748-4b25-8db8-5127c14c8ffa)

Nyt koska /salt hakemistossa on jo top.sls tiedosto aiemmasta tehtävästä pitäisi komennon 'sudo salt '*' state.apply' asentaa apache, korvata tekstisivu ja tarkistaa että demoni on käynnissä.

![Näyttökuva 2023-11-19 kello 10 40 01](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/8287ebfd-d548-45c9-a3e8-8cb10cba8f37)

Komento näyttäisi toimivan.

![Näyttökuva 2023-11-19 kello 10 43 41](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/d36d4969-4f95-4566-a9eb-77d579180161)

Apache2 tuli asennettua molemmalle orjalle ja tekstisivu tuli korvattua.

***

## d) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.

Aloitetaan seuraamalla ohjeita Tero Karvisen [artikkelista](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)

Ohjeessa suositeltiin käyttämään virtuaalikonetta jota Vagrant ei ohjaa, joten kirjaudutaan kurssin alussa luotuun Debian 12 virtuaalikoneen sisään. Ensimmäiseksi ajetaan päivitykset 'sudo apt-get update/upgrade' komennoilla. 

Luodaan /srv/salt hakemistoon tiedosto sshd.sls ja lisätään sinne teksti Teron sivulta.

![Näyttökuva 2023-11-19 kello 11 25 40](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/2bd1b6c0-7704-494f-87ab-88020e455003)

Sitten konfiguroidaan sshd_config tiedostoa. Etsitään se /etc/ssh hakemisosta ja käydään muuttamassa sieltä porttinumeroa. 

![Näyttökuva 2023-11-19 kello 11 25 40](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/452c8eb1-69cd-4211-a5c7-54269209b77c)

Tarkistetaan vielä sshd.servicen tila komennolla 'sudo systemctl status sshd.service'

![Näyttökuva 2023-11-19 kello 11 36 17](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/51e0018d-9f36-42a4-9689-c48d7286d59c)

lopuksi testi

![Näyttökuva 2023-11-19 kello 11 38 58](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/aef7ea46-84f3-41fd-8e96-ae8862379118)

Tässä tehtävässä käytin apuna käyttäjän "hautadata" [raporttia](https://github.com/hautadata/palvelintenhallinta-jh/blob/main/h4-demonit.md).

Kokeilin useaa eri tapaa suorittaa tehtävää mutta en oikein päässyt edistymään. En ihan täysin ymmärrä mitä tehtävässä yritetään tehdä. Joten jätän tämän nyt tähän.



# Lähteet

Tero Karvinen 2023: [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file)

Tero Karvinen 2018: [Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)

Pipe2grep 2019: [SaltStack_NOOBS_3: Understanding the Top File and Highstates](https://www.youtube.com/watch?v=BbMcIBrnnhw)

Pipe2grep 2019: [SaltStack_NOOBS_2- Writing Your First Salt State (file.managed)](https://www.youtube.com/watch?v=tknfj0sSAjY)
