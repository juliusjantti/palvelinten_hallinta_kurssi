## TEHTÄVÄ
h3 Versio
a) Online. Tee uusi varasto GitHubiin (tai Gitlabiin tai mihin vain vastaavaan palveluun). Varaston nimessä ja lyhyessä kuvauksessa tulee olla sana "winter". Aiemmin tehty varasto ei kelpaa. (Muista tehdä varastoon tiedostoja luomisvaiheessa, esim README.md ja GNU General Public License 3)

b) Dolly. Kloonaa edellisessä kohdassa tehty uusi varasto itsellesi, tee muutoksia, puske ne palvelimelle, ja näytä, että ne ilmestyvät weppiliittymään.

c) Doh! Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset --hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.

d) Tukki. Tarkastele ja selitä varastosi lokia. Tarkista, että nimesi ja sähköpostiosoitteesi näkyy haluamallasi tavalla ja korjaa tarvittaessa.

e) Vapaaehtoinen: yhteistyötä: anna kaverillesi (tai alter egollesi) oikeus kirjoittaa varastoosi (commit access). Tehkää molemmat muutoksia varastoon gitillä.

f) Vapaaehtoinen: Suolattu rakki. Tee uusi moduli. Kloonaa varastosi toiselle koneelle (tai poista srv/salt ja palauta se kloonaamalla) ja jatka sillä. (Salt tiedostot mistä vain hakemistosta, huomaa suhteellinen polku: 'sudo salt-call --local --file-root srv/salt/ state.apply')

g) Vapaaehtoinen: Se toinen järjestelmä: kokeile Gittiä eri käyttöjärjestelmällä kuin sillä, millä teit muut harjoitukset. Selitä niin, että kyseistä järjestelmää osaamatonkin onnistuu. Mahdollisuuksia on runsaasti: Debian, Fedora, Windows, OSX...



***

a)
Tehtävän ensimmäisessä kohdassa luodaan uusi varasto, ja minä päätin luoda varaston GitHubiin. Varaston nimeksi tuli "WinterPonderland" ja lisäsin sinne heti luomisen yhteydessä "GNU General Public License"-lisenssitiedoston ja "README"-tiedoston. Kuvissa alhaalla varaston luonti ja valmis varasto.

![Näyttökuva 2023-11-9 kello 15 22 59](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/1a1d1782-f223-45ed-a4d6-e233ab22dd38)

![Näyttökuva 2023-11-9 kello 15 23 16](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b4c1f188-8a9d-43b8-b688-afecb6d85fcc)


b)
Tässä kohdassa taas piti kloonata aiempi varasto itselleen. Ensimmäiseksi latasin gitin virtuaalikoneelleni komennolla 'sudo apt-get install git'. Tämän jälkeen avasin varaston nettiselaimella ja kopioin sieltä ssh avaimen/osoitteen (mikskä sitä nyt kutsutaankaan?). Kuva alla.

![Näyttökuva 2023-11-9 kello 15 56 03](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/c873bbf8-ce74-4c4e-b86c-5bbc86631734)

Tämän jälkeen ajoin komennon 'git clone' jonka perään laiton kyseisen linkin aiemasta kuvasta.

![Näyttökuva 2023-11-9 kello 15 50 23](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/2ea424ba-77c8-40d9-bdde-bcca06001896)

Tämä ei tietenkään toiminut. Minulla ei ollut pääsyä varastoon koska en ollut vielä vahvistanut itseäni SSH avainpareilla. 

Joten loin virtuaalikoneella uuden avainparin 'ssh-keygen', ja kopioin itselleni julkisen avaimen. Tämän jälkeen menin oman github-käyttäjäni asetuksiin webbiselaimella ja lisäsin julkisen avaimeni sinne. 

Tallennettuani avaimen kokeilin aikasempaa 'git-clone' komentoa uudestaan. Ja tulos näkyy alhaalla.
![Näyttökuva 2023-11-9 kello 15 53 23](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/4fce621c-d5d2-4e1a-b086-e1bc927c010e)

Varasto oli ilmestynyt koneelleni.

Siirryin vielä kyseiseen "WinterPonderland" hakemistoon ja sieltä löytyivät kaikki samat tiedostot jotka näkyivät myös webbiselaimessa.
![Näyttökuva 2023-11-9 kello 15 53 54](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/b070b808-378c-408f-8c8f-f1f9fac8aa3a)

Sitten luodaan tiedosto "testi.txt" 'touch' komennolla ja lisätään siihen jotain tekstiä. Lisätään 'git add testi.txt' komennolla tiedosto varastoon. 

![Näyttökuva 2023-11-9 kello 16 14 45](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/0e3a05f3-9433-426d-a10f-08a69d52ecd0)

Tässävälissä ajetaan myös komennot 'git config --global user.email "sähköposti"' ja 'git config --global user.name "nimi"'. Näin saadaan asetettua nimi ja sähköposti.

![Näyttökuva 2023-11-9 kello 16 17 05](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/9f3e5acf-ee67-4d0b-aeb6-ee3d0d421a57)

Sitten ajetaan 'git commit' ja kirjoitetaan mitä muutoksia tehtiin.

![Näyttökuva 2023-11-9 kello 16 20 34](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/06763551-01af-4188-9d10-ed1ceb1a4b1e)

Ja tämän jälkeen peräkkäin 'git pull' ja 'git push'

Ja sitten voidaan avata webbiselain taas ja tarkistaa näkyykö tiedosto siellä.

![Näyttökuva 2023-11-9 kello 16 23 16](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/ca3d948d-bb78-4c21-be51-27cebf7fc87f)

***

c)
Tässä kohtaa tehdään GITtiin muutoksia ja perutaan tehdyt muutokset ennen committia. komennolla 'git reset --hard'.

![Näyttökuva 2023-11-9 kello 16 37 25](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/bd490301-42bc-42e6-ac75-4e7d673d9002)

d) 
Tutkitaan oman varaston lokia.

![Näyttökuva 2023-11-9 kello 16 39 14](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/77e58dec-0c93-4b59-ae03-274e88c8ac1a)

Logissa näkyy kolme tekemääni committia. Ensimmäinen mikä oli varaston luonti, on tehty käyttäjällä "juliusjantti", eli se on tehty webbiselaimessa.

Toinen Committi on "testi.txt" tiedoston luominen, jonka tein komentorivillä. Muokaajan nimi on tässä vaiheessa "Testikayttaja" koska se oli nimi jonka annoin virtuaalikoneessa. 

Kolmas committi on myös komentorivillä tehty, ja kirjoittajana on taas testikäyttäjä. 

Commit messageissa lukee molemmissa englanniksi käskymuodossa mitä kussakin muutoksessa on tehty.

Jokaisen ohjeen kohdalla on seurattu tehtvänannon mukana tulevia [vinkkejä](https://terokarvinen.com/2023/configuration-management-2023-autumn/).

***

g)
Kokeillaan GITtiä toisella käyttöjärjestelmällä. Minun tilanseessa Mac Os:sällä. 

Asensin Gitin käyttämällä Homebrew:tä. Sen asentamiseen ohjeet, sekä tietoa siitä löytyy [täältä](https://brew.sh/).

Tässä vaiheessa käytetään apuna Youtubesta löytynyttä tutorial [videota.](https://www.youtube.com/watch?v=hMEyBtsuAJE)

Aloitetaan avaamalla Terminal ja asentamalla git komennolla 'brew install git' ja kokeillaan että se toimii komennolla 'git'.

![Näyttökuva 2023-11-10 kello 14 32 33](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/bf7b9248-cdd1-4c19-9d8d-06a8be5281e8)

Luodaan uusi hakemisto komennolla 'mkdir' ja annetaan sen nimeksi Git, ja siirrytään kyseiseen hakemistoon komennolla 'cd Git'. 

Jossain vaiheessa täytyi ilmoittaa oma nimi ja sähköposti komennoilla 'git config --global user.name/user.email' mutta ne unohtui hieman matkasta raporttia kirjoittaessa.

Kloonataan aiemmin käytetty "WinterPonderland" varasto myös tässäkin tehtävässä, joten luodaan SSH avainpari samalla tavalla kuin aikasemmassa tehtävässä komennolla 'ssh-keygen' ja käydään lisäämässä se oman GitHub käyttäjän avaimiin. Ja lopuksi ajetaan komento 'git clone "ssh linkki'".

Sitten siirrytään kyseiseen varastoon ja luodaan sinne uusi testitiedosto nimeltään "maccitesti.txt". Lisätään se gittiin komennolla 'git add .'

![Näyttökuva 2023-11-10 kello 15 02 49](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/5f339b64-d580-4834-a803-40de4ca1cc29)

Tämänjälkeen perinteiset 'git commit -m "commit viesti"', 'git pull' ja 'git push'.

![Näyttökuva 2023-11-10 kello 15 04 08](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/6abfa407-7e0b-4817-95b7-67cd292c5827)

Ja lopuksi nähdään miten tiedosto on ilmestynyt webiselaimeen.

![Näyttökuva 2023-11-10 kello 15 05 21](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/c772510f-0673-427e-89f6-4f519b2e29aa)







***

## LÄHTEET

An insightful techie, Git Commands - Beginners hands on git status git clone git commit git push git log git add and more: https://www.youtube.com/watch?v=Uz_mTOQL9Tw

Tero Karvinen, kohta h3 Versio, Vinkkejä: https://terokarvinen.com/2023/configuration-management-2023-autumn/

Code with Arjun, Install Git on MacOS (Macbook M1, M1 Max, M1 Pro, M2) and push project into Github | Homebrew: https://www.youtube.com/watch?v=hMEyBtsuAJE
