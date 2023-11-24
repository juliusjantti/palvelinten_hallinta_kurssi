# h5 CSI kerava

## x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
Karvinen 2018: [Apache User Homepages Automatically – Salt Package-File-Service Example](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/)

x) Vastaus

  - Kuinka käyttää salttia luomaan käyttäjälle omat kotisivut apachess automaattisesti. Ensin kannattaa aina tehdä käsin, ja sitten vasta automatisoida.


## a) CSI Kerava. Näytä 'find' avulla viimeisimmäksi muokatut tiedostot /etc/-hakemistosta ja kotihakemistostasi. Selitä kaikki käyttämäsi parametrit ja format string 'man find' avulla.

a) Vastaus

Siirrytään virtuaalikoneella ensiksi /etc hakemistoon komennolla 'cd /etc'. Ja annetaan siellä komento 'find -printf "%T+ %p\n"|sort', mikä on komioitu suoraan teron [sivulta](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/). Alla näkyy tulos, josta en itse juurikaan ymmärrä mitään. 

![Näyttökuva 2023-11-24 kello 11 56 21](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/0b8ed5b9-5d05-4542-9fef-e1ccd1e09671)

Sitten siirrytään takaisin omaan kotihakemistoon komennolla 'cd' ja annetaan sama komento 'find -printf "%T+ %p\n"|sort'. Alla tulos.

![Näyttökuva 2023-11-24 kello 11 59 05](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/77b6bae3-97a1-45f6-a917-2ec19edd077c)

Alla vielä man-sivulta löydettyjä selityksiä parametreille.

![Näyttökuva 2023-11-24 kello 12 02 44](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/6f2c3d95-682e-4ab0-80b1-d5e04c481b9c)
![Näyttökuva 2023-11-24 kello 12 01 14](https://github.com/juliusjantti/palvelinten_hallinta_kurssi/assets/148885509/242b13ad-149f-4ccb-a640-d264ff573fda)

%T+ = tiedoston muokkaamisaika
%p = tiedostonimi
\n = uusi rivi
