# Tehtävä h1
x)
- GitHub sivun luominen oli helppoa kun seurasi annettuja ohjeita, tunnilla tehty ensimmäinen tehtävä osoitti onnistumisen.
- Salt:ia käytetään kontrolloidessa suuria määriä tietokoneita.
- Salt-komentoja voi myös ajaa lokaalisti yhdellä tietokoneella, ja tällä tavoin harjoitella niiden käyttämistä turvallisesti.
- Lopuksi latasin debian-live-12.2.0-amd64-xfce.iso tiedoston ja asensin sen VirtualBox virtuaalitietokoneelle ohjeiden mukaisesti.

a)
Salt minion asentaminen onnistui. Asentamisessa käytin komentoa mikä oli tehtävänannon mukana. Se oli hiukan hankala kirjoittaa terminaaliin mutta kaikki onnistui loppujenlopuksi. Salt versio "salt-call" komennolla oli 3006.3 (sulfur)

b) 
Ensimmäisenä komentona pkg.installed: komento piti huolen että paketti asennettiin tai poistettiin vain kerran. Ensimmäisellä kerralla vastaus tuli että jotain asennettiin tai poistettiin. Seuraavilla kerroilla ilmoitus vain "All specific packages are already installed", eli muutoksia ei tullut.
file.managed komennolla sama homma. Jos tiedostoa ei ollut, se luotiin ja jos tiedosto oli, vastauksena tuli että "tiedosto on jo olemassa, ei muutoksia". Tekstin lisäyskomennolla tiedostoon, ilmoitus tuli että tiedosto päivitettiin ja mitä tekstiä lisättiin. Tämän jälkeen komennon uudelleenajamisen jälkeen ilmoitus että "is in the correct state". file.absent komennon kanssa sama juttu, jos tiedosto oli olemassa se poistettiin, ja jos ei ollut olemassa niin ilmoitus että ei ole olemassa.
service.running komennolla laitetaan käyntiin jokin demoni. Jos se ei ole päällä kyseinen demoni käynnistetään, ja jos se on päällä mitään ei tapahdu. Sama toimii käänteisesti service.dead komennolla.
user.present/user.absent, voidaan luoda tai poistaa käyttäjä. Jos käyttäjä on olemassa, mitään ei tapahdu kun sitä yritetään luoda uudelleen. Ja jos käyttäjää ei ole, mitään ei tapahdu jos käyttäjää yritetään poistaa (user not present).
Ja vielä kerran sama komennolla cmd.run. Kone ajaa komennon, vain jos muutoksien teko on tarvittavaa. 

c) 
Idempotentti komento siis tarkoittaa komentoa jonka voi ajaa usean kerran, mutta joka tapahtuu vain yhden kerran. Esimerkkinä uuden käyttäjän luominen. Ensimmäisellä kerralla kone luo käyttäjän, mutta toisella kerralla kone näkee että käyttäjä on jo olemassa, ja täten jättää uuden käyttäjän tekemättä. Tulee ilmoitus että käyttäjä on jo olemassa. 

d)
'sudo salt-call --local grains.item osfinger virtual' komennon jälkeen sain poimituksi vain seuraavat tiedot: "osfinger:Debian-12" ja "virtual: VirtualBox".
kolme poimintaa saltin grains.items tekniikalla:

biosrelesedate: 12/01/2006
oscodename: bookworm
cpu_model: Intel(R) Core(TM) i5-8279U CPU @ 2.40GHz






  

## Lähteet
Tehtäväsivu: https://terokarvinen.com/2023/configuration-management-2023-autumn/

Kuinka asentaa debian: https://terokarvinen.com/2021/install-debian-on-virtualbox/

Debian versiot: https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/

Salt komennot: https://terokarvinen.com/2021/salt-run-command-locally/

Apua pakettien lataamiseen ja poistamiseen: https://www.debian.org/doc/manuals/debian-faq/pkgtools.en.html


