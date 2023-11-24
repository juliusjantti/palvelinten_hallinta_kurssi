# h5 CSI kerava

## x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
Karvinen 2018: [Apache User Homepages Automatically – Salt Package-File-Service Example](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/)

x) Vastaus

  - Kuinka käyttää salttia luomaan käyttäjälle omat kotisivut apachess automaattisesti. Ensin kannattaa aina tehdä käsin, ja sitten vasta automatisoida.


***


## a) CSI Kerava. Näytä 'find' avulla viimeisimmäksi muokatut tiedostot /etc/-hakemistosta ja kotihakemistostasi. Selitä kaikki käyttämäsi parametrit ja format string 'man find' avulla.

a) Vastaus

Siirrytään virtuaalikoneella ensiksi /etc hakemistoon komennolla 'cd /etc'. Ja annetaan siellä komento 'find -printf "%T+ %p\n"|sort', mikä on komioitu suoraan teron [sivulta](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/). Alla näkyy tulos, josta en itse juurikaan ymmärrä mitään. 

![Näyttökuva 2023-11-24 kello 11 56 21](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/0b8ed5b9-5d05-4542-9fef-e1ccd1e09671)

Sitten siirrytään takaisin omaan kotihakemistoon komennolla 'cd' ja annetaan sama komento 'find -printf "%T+ %p\n"|sort'. Alla tulos.

![Näyttökuva 2023-11-24 kello 11 59 05](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/77b6bae3-97a1-45f6-a917-2ec19edd077c)

Alla vielä man-sivulta löydettyjä selityksiä parametreille.

![Näyttökuva 2023-11-24 kello 12 02 44](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/6f2c3d95-682e-4ab0-80b1-d5e04c481b9c)
![Näyttökuva 2023-11-24 kello 12 01 14](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/242b13ad-149f-4ccb-a640-d264ff573fda)
![Näyttökuva 2023-11-24 kello 12 01 14](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/e065eacb-2c53-4d80-aa1d-32c1f9f325d2)

%T+ = tiedoston muokkaamisaika
%p = tiedostonimi
\n = uusi rivi

***

## b) Gui2fs. Muokkaa asetuksia jostain graafisen käyttöliittymän (GUI) ohjelmasta käyttäen ohjelman valikoita ja dialogeja. Etsi tämä asetus tiedostojärjestelmästä.

b) Vastaus


Otetaan tehtävän ajaksi käyttöön kurssin alussa luotu Debian12 virtuaalikone, jotta päästään käyttämään graafista käyttöliittymää.

Avataan Virtuaalikoneella desktopissa "Documents" kansio ja luodan sinne uusi tiedosto nimeltä "testi.txt" käyttäen graafista käyttöliittymää ja hiirellä näppäillen.

![Näyttökuva 2023-11-24 kello 12 13 19](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/43e4e6a1-393c-4bda-a812-07369a59327f)

Sitten avataan Terminaali, siirrytään /Documents hakemistoon ja ajetaan komento 'find -printf "%T+ %p\n"|sort'. Tuloksena näkyy että viimeisin muokattu  asia on testi.txt tiedosto.

![Näyttökuva 2023-11-24 kello 12 15 19](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/52ab5f10-9978-41ce-84d2-64944c321f0c)


## c) Komennus. Tee Salt-tila, joka asentaa järjestelmään uuden komennon.


Aloitetaan ensin tekemällä käsin shell-scripti kotihakemistoon. Tehdään nanolla uusi tiedosto nimeltä "hei" ja lisätään sinne seuraavat komennot.

![Näyttökuva 2023-11-24 kello 12 44 47](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/98909929-f2d9-4605-ad35-20aae1400f2f)


Sitten kokeillaan toimiiko.

![Näyttökuva 2023-11-24 kello 12 43 04](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/39d6c79c-a17c-43f0-a0dd-62a204b5415e)


Sitten annetaan tiedostolle oikeat oikeudet komennolla 'chmod 755 hei', ja katsotaan menikö oikeudet perille. Omistajalla on kaikki oikeudet mutta ryhmillä ja muilla käyttäjillä on vain luku ja execute-oikeudet.

![Näyttökuva 2023-11-24 kello 12 39 03](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/f6231bc2-ed6d-4041-962d-ed26a121b3d3)


![Näyttökuva 2023-11-24 kello 12 43 13](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/5812f3a7-049b-45a7-b777-ec73545e7dd1)

Shell scripti näyttäisi toimivan 

Sitten siirretään scripti vielä /usr/local/bin hakemistoon. Ja kokeillaan toimiiko komento 'hei'

![Näyttökuva 2023-11-24 kello 12 47 29](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/9c7e8e0e-dafc-4572-ae2a-a1440b02c6a2)

Kaikki näyttäisi toimivan. Sitten siirrytään automatisaatioon. Mennään ensiksi /srv/salt hakemistoon ja luodaan sinne uusi hakemisto nimeltään "tervehdys". Käytetään komentoa 'sudo mkdir tervehdys'. Siirrytään tähän "tervehdys" hakemistoon ja luodaan sinne init.sls tiedosto 'sudoedit init.sls' komennolla. Init.sls sisältö alla:

![Näyttökuva 2023-11-24 kello 12 54 37](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/2b31955e-20ec-4f5d-8078-36946582a56c)

Sitten luodaan tiedosto "tervehdys" joka sisältää itse scriptin josta haluamme tehdä komennon.

![Näyttökuva 2023-11-24 kello 12 56 19](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/30ad2e21-2469-4b6e-9fe7-086719755d4e)






***

# Lähteet

- 
