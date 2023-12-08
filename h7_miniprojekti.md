# h7 Miniprojekti

Miniprojektin tarkoituksena luoda konfiguraatio linux tietokoneelle.

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

Sitten tuhotaan vanhat virtuaalikoneet ja luodaan tilalle uudet "puhtaat" koneet. Käytetään komentoa 'vagrant destroy'.


