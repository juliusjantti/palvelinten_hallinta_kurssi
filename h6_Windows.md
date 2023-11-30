# H6 Windows tehtävä

## x) Lue ja tiivistä

Halonen, Rajala ja Ollikainen 2023: [Installing Windows 10 on a virtual machine](https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md)

Vain tämä Windowsin asennusohje. Samassa varastossa on hyökkäysohjelmia, joiden käsittely edellyttää, että osaa tehdä sen turvallisesti ja laillisesti, mm. eristää harjoituskoneita Internetistä. Nämä taidot oppii esim. kurssillani Tunkeutumistestaus. Tällä kurssilla ei käytetä hyökkäystyökaluja. Mutta tämä Windowsin asennus virtuaalikoneeseen on yksinkertaista ja turvallista.

LSB Workgroup, The Linux Foundation 2015: [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

Lue otsikot, katso sisältöä jos asia ei ilmene otsikosta
Poimi tiivistelmääsi sellaisten kansioiden määritelmät, joiden kanssa olet itse tekemisissä.

x) Vastaus

Windowsin asentaminen virtuaalikoneelle hyvin simppeliä. Lataa iso-tiedosto ja lisää se virtualboxiin. TÄmän jälkeen avaa virtuaalitietokone ja ota se käyttöön.

Käyttäjän kotihakemisto "/home"

"/etc" sisältää kaikki konfiguraatiotiedostot.

Hakemisto johon sys admin voi asentaa softaa paikallisesti "/usr/local"


***


## a) Asenna windows virtuaalikoneeseen

a) Vastaus

Tunnilla suoritettiin windowsin asentaminen virtuaalikoneeseen joten prosessista ei tullut napattua kuvankaappauksia. Asentaminen kuitenkin onnistui seuraamalla Halosen, Rajalan ja Ollikaisen [raporttia](https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md). Kaikki tarvittavat kohdat näkyvät ohjeissa.

Kuvankaappaus Windowsista virtualboxissa.

![Näyttökuva 2023-11-30 kello 16 05 38](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/6dd856f3-9cc4-4222-ba6b-c29a4eb6d544)

***

## b)  Asenna Salt Windowsille. Osoita 'salt-call --local' komentoa ajamalla, että asennus on onnistunut.

b) Vastaus

Aloitetaan avaamalla Windows virtuaalikoneella selain, ja googlettamalla "Salt windows download". Siirrytään Salt:in omille [sivuille](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html), josta voi ladata ja asentaa saltin.

![Näyttökuva 2023-11-30 kello 16 10 25](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/2e6e7522-fccc-477b-ab15-3ed2d79b3daa)

Kun saltti on asennettu, voi tiedoston avata ja klikkailla asennus eteenpäin.

![Näyttökuva 2023-11-30 kello 16 11 29](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/a0ed23ac-d31d-499d-afc0-52f45f2244c5)

Kun päästään kohtaan "Minion Settings" annetaan orjalle nimi sekä kirjoitetaan halutun herran IP osoite. Minun tapauksessa käytän aiempaa vagrantin herran ja kahden  orjan konfiguraatiota. Otetaan herran IP osoite ylös ajamalla herra-koneella komento 'Hostname -I'

![Näyttökuva 2023-11-30 kello 16 16 55](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/509f4074-09b0-4e29-9e77-881915577429)

Sitten hoidetaan asennus loppuun.

Kun Salt on asennettu Windows koneelle, avataan taas vanha kunnon Vagrant herra kone ja ajetaan komento 'sudo salt-key -A' Jolloin juuri asennettu Windows kone pitäisi ilmestyä näkyviin.

![Näyttökuva 2023-11-30 kello 16 23 14](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/4b68048a-eed7-422b-a75e-e0070a63ccf9)

Hyväksytään avaimet. Nyt meillä pitäisi olla kolmas orja. Minun tapauksessa nimeltään 'ikkuna'. Tehdään testi ja ajetaan komento 'sudo salt '*' test.ping'

![Näyttökuva 2023-11-30 kello 16 26 13](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/fc28eb81-382b-46e9-b6fb-613fb78cecbc)

Jahas ei näytä toimivan.

Ensimmäinen ajatus on että Saltin versiot eri virtuaalikoneilla ovat erilaiset. Linuxilla on versio 3002.6 ja windowsilla 3006.4. Joten poistetaan salt windowsilta ja yritetään ladata vanhempi versio. 

Tero Karvisen ohjeiden avulla löysin vanhemman version Saltista [täältä](https://archive.repo.saltproject.io/windows/)

Joten ladataan versio 3002.6 aiempien ohjeiden avulla, ja hyväksytään avaimet. Sitten kokeilleen 'test.ping' komentoa uudestaan. 

![Näyttökuva 2023-11-30 kello 17 52 15](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/13b6f2d8-3661-4ef9-92d2-20a62691636d)

Kappas näyttäisi toimivan.

'Salt-call --local' komento ei kuitenkaan tunnu toimivan.

![Näyttökuva 2023-11-30 kello 18 01 57](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/701b5608-7b5b-40f9-8612-819b56561069)

Mutta kun siirryin /salt hakemistoon komennolla 'cd /salt/' ja ajoin komennon sielä, se näyttäisi toimivan.

![Näyttökuva 2023-11-30 kello 18 05 32](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/a8a5e55e-8f35-437a-bbea-130564f1dbf5)

Ja vielä saltin versio komennolla 'salt-call -V'

![Näyttökuva 2023-11-30 kello 18 08 11](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/08d40992-fcaa-447e-8148-b7614db06bb6)

***

## c) Kerää Windows-koneesta tietoa grains.items -toiminnolla. Poimi 'grains.item' perään muutamia keskeisiä tietoja ja analysoi ne, eli selitä perusteellisesti mitä ne ovat. Kuvaile ja vertaile numeroita.

c) vastaus

Kokeillaan ensiksi klassinen komento jolla saadaan tietoon orjien käyttöjärjestelmä 'sudo salt '*' grains.item osfinger'

![Näyttökuva 2023-11-30 kello 18 09 56](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/e4c9a5a9-ab3b-4cbc-8925-4cc11db8e6d1)

sitten kokeillaan orjien id:

![Näyttökuva 2023-11-30 kello 18 13 35](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b0591bdc-2417-43b8-82a7-b173b674a04a)

ja vaikka vielä cpu_model. Näyttää kaikissa samaa varmaankin koska ne ovat virtuaalikoneita.

![Näyttökuva 2023-11-30 kello 18 14 25](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/62578c84-fb02-4e50-afe4-221c374423ba)

ja vielä bonuksena saltpath. Eli varmaankin missä salt sijaitsee?

![Näyttökuva 2023-11-30 kello 18 17 19](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/5028e9aa-8bf8-4705-9563-fce195775dcd)

***

## d) Kokeile Saltin file -toimintoa Windowsilla.

d)Vastaus

Kokeillaan komentoa 'sudo salt 'ikkuna' state.single file.managed 'C:\Users\jj\Desktop\testi.txt'' jolla luodaan tiedosto testi.txt windows koneen työpöydälle.

![Näyttökuva 2023-11-30 kello 20 39 23](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/cf4683be-ceb2-415f-b4f3-5346e01f7b32)


![Näyttökuva 2023-11-30 kello 20 40 17](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/ada50e56-8577-4567-a0b0-45ad1ab880fb)

Tiedosto ilmestyi työpöydälle


***

# Lähteet

Salt versions: https://archive.repo.saltproject.io/windows/

Tero Karvinen, 2018, [Control Windows with Salt](https://terokarvinen.com/2018/04/18/control-windows-with-salt/)
