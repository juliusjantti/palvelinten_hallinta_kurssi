# h7 Miniprojekti

Miniprojektin tarkoituksena luoda konfiguraatio linux tietokoneelle. Käytössä on kolme linux/debian virtuaalikonetta. Yksi master ja kaksi minion konetta.

Tavoitteena:
- Asentaa apache sekä luoda käyttäjälle automaattisesti oma kotisivu
- Asentaa ssh 
- Ladata muutama hyödyllinen komento
- Lisätä uusi käyttäjä
- Sekä lisätä yksi oma komento

## Aloitetaan kokeilemalla ensiksi käsin

Asennetaan paketit komennoilla:

'sudo salt '*' state.single pkg.installed apache2'

'sudo salt '*' state.single pkg.installed ssh'

'sudo salt '*' state.single pkg.installed curl'

'sudo salt '*' state.single pkg.installed tree'

'sudo salt '*' state.single pkg.installed snapd'

'sudo salt '*' state.single pkg.installed net-tools'

Jokainen komento toimi joten en jokaisesta laita näyttökaappausta.



![Näyttökuva 2023-12-8 kello 12 13 48](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/366801b2-0780-463f-a408-bd8411c8f18c)

Lisätään sitten uusi käyttäjä komennolla: sudo salt '*' state.single user.present masa

![Näyttökuva 2023-12-8 kello 12 15 27](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/a7b742a7-0ec8-4dbc-b628-236a61be91bf)

Luodaan masterilla oma shell-scripti ja siirretään se /usr/local/bin hakemistoon. Kokeillaan toimiiko scripti.

![Näyttökuva 2023-12-8 kello 12 21 28](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/eeaefd73-a2c0-4585-9f01-56fc50b50f18)

Sitten tuhotaan vanhat virtuaalikoneet ja luodaan tilalle uudet "puhtaat" koneet. Käytetään komentoa 'vagrant destroy'. Tämän jälkeen otetaan uudet virtuaalikoneet käyttöön seuraamalla Tero Karvisen [ohjetta](https://terokarvinen.com/2023/salt-vagrant/).

***

## Sitten ruvetaan automatisoimaan

Luodaan ensiksi /srv hakemistoon uusi hakemisto nimeltään /salt, jonne ruvetaan keräämään moduuleta.

Tehdään ensiksi /apache hakemisto jonne luodaan init.sls tiedosto. Kyseiseen tiedostoon lisätään komennot [Teron](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/) ohjeita seuraten. 

Kokeillaan ensiksi vain yhdelle virtuaalikoneelle toimiiko tila.

![Näyttökuva 2023-12-8 kello 12 34 35](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/9f5f9de8-a1f1-4f17-94f0-bdbab9df4bcb)

Toimii. Sitten siirrytään seuraavaan, eli muiden pakettien asennukseen.

Luodaan /srv/salt hakemistoon uusi /ohjelmat kansio ja sinne taas init.sls tiedosto

![Näyttökuva 2023-12-8 kello 12 39 17](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/c4595358-69b5-4461-b126-c69260fb6aec)

kokeillaan jälleen kerran ajaa tila vain toiselle virtuaalikoneelle.

![Näyttökuva 2023-12-8 kello 12 39 41](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/edf45d73-6a54-43b0-98a0-cad79bdffed9)

Sitten siirrytään uuden käyttäjän luomiseen.

Jälleen uusi moduli /salt/srv hakemistoon nimeltä /kayttaja, ja sinne init.sls tiedosto

![Näyttökuva 2023-12-8 kello 12 49 57](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b395f199-968f-432f-aa44-e467e8923c96)

Ja testataan jälleen toimivuus

![Näyttökuva 2023-12-8 kello 12 50 13](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b363bb91-eace-4119-b6c2-e803b2f87451)

Ja viimeiseksi vielä oman komennon luominen. Tehdään /srv/salt/komento hakemisto ja sinne init.sls tiedosto sekä itse komento.

![Näyttökuva 2023-12-8 kello 12 56 14](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/fa21c935-2206-4dff-ab27-f5e2497af89f)

Ja jälleen kokeillaan:

![Näyttökuva 2023-12-8 kello 13 00 00](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/ab6c5a1c-2a96-4794-85a2-be0fb659b39f)

Tässä vaiheessa moduulit alkavat olla valmiina. 

***

Luodaan kuitenkin vielä top.sls tiedosto jotta saadaan kaikki ajettua yhdellä komennolla. Luodaan /srv/salt hakemistoon top.sls jonka sisältö on seuraava:

![Näyttökuva 2023-12-8 kello 13 03 38](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/591a652f-ffcf-4847-a89a-be82d8ab931e)

Sitten vihdoin ajetaan komento 'sudo salt 'orja2' state.apply'

![Näyttökuva 2023-12-8 kello 13 06 34](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/8a912aa5-a96e-4962-8946-b0406aeb7124)

Ja kaikki vaadittavat tilat näyttää olevan ajettu. 

***

Kokeillaan vielä lisätä konfiguraatiot git:tiin jotta ne voidaan tulevaisuudessa ladata sieltä.

Seurasin kurssilla aiemmin tehdyn oman [tehtäväni ohjeita](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/blob/main/h3_versio.md).

Kopioin lopulta /srv/salt hakemiston sisällön, Miniprojekti-hakemistoon komennolla 'cp -r /srv/salt /home/vagrant/Miniprojekti'. Hakemisto "Miniprojekti" on Github sivuilla oleva repository. 

![Näyttökuva 2023-12-8 kello 13 21 35](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/12710077-031b-4fb6-ba3b-877fa24f842b)

Lopulta tiedostot ovat githubissa.
[Linkki repositoryyn](https://github.com/juliusjantti/Miniprojekti)

***

Testataan vielä kerran konfiguraation toimivuutta uusilla virtuaalikoneilla. Ajetaan 'vagrant destroy' ja 'vagrant up' komennot

Kirjaudutaan sisään uuteen herra-koneeseen ja ladataan ensiksi Git komennolla 'sudo apt-get install git'. Tämän jälkeen ladataan "Miniprojekti" repon tiedostot komennolla 'git clone (repon ssh linkki)'


![Näyttökuva 2023-12-8 kello 14 41 53](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/27ceea16-dd22-4da3-a92a-f08395c93abb)

Kopioidaan kyseinen /salt kansio /srv hakemistoon.

![Näyttökuva 2023-12-8 kello 14 43 49](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/a9090e93-a419-4589-a5d4-d21c0b9acc96)

Tämän jälkeen voidaan ajaa 'sudo salt '*' state.apply'.


![Näyttökuva 2023-12-8 kello 14 46 59](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/5241387e-b2ec-4507-a1f2-42951bf39875)

Komento näyttäisi toimivan.

Otetaan vielä ssh yhteys "orja1" koneeseen ja tarkistetan toimiiko kaikki.

![Näyttökuva 2023-12-8 kello 14 51 12](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/e7b692ef-4254-4dce-b5c8-daf753355c7b)

Tässä hieman testailua. Apache näytäisi toimivan, curl ja tree komennot toimivat, joulupukki käyttäjä löytyy, sekä oma komento toimii.





# Lähteet

Tero Karvinen, 2023, [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/)

Tero Karvinen, 2018, [Apache User Homepages Automatically – Salt Package-File-Service Example](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/)

Tero Karvinen, 2023, [Infra as a code](https://terokarvinen.com/2023/configuration-management-2023-autumn/)

Linuxzie, 2018, [How to list users in Linux](https://linuxize.com/post/how-to-list-users-in-linux/)

Julius Jäntti, 2023, [Miniprojekti](https://github.com/juliusjantti/Miniprojekti/tree/main)

Julius Jäntti, 2023, [h3_versio](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/blob/main/h3_versio.md)

Julius Jäntti, 2023, [h5_CSI-kerava](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/blob/main/h5_CSI-kerava.md)

Ask Cloud Architecture, 2023, [How to Download Files from Github: 4 Easy Methods](https://www.youtube.com/watch?v=eWiPHP0us_0)








