# h2 Infraa koodina


## Tiivistelmä
### Hello Salt Infra-as-Code

- Oma tila (state) luodaan /srv/salt/hello/init.sls, joka varmistaa että tiedosto /tmp/hello -example on olemassa.
- Komennolla sudo salt-call --local state.apply hello tila ajetaan paikallisesti.
- Paikallisen ajon jälkeen tulevassa tulosteessa kerrotaan yksityiskohtaisesti, mitä tehtiin. (Karvinen, 3.4.2024)

### Salt overview
- Salt käyttää YAML-muotoa asetusten ja tilojen kuvaamiseen.
- YAML perustuu avain ja arvo -pareihin ja käyttää välilyöntejä, ei tabulaattoreita.
- YAML:ssä on kolme peruselementtiä, jotka ovat skalaari, lista ja sanakirja.
- YML:n rakenne määräytyy sisennyksillä. (Salt Project 2025)

### The Top File
- Top file määrittää, mitä tiloja ajetaan millekin koneelle.
- Sen sijainti on tilapuun juurella ja on nimetty top.sls.
- Yhdellä top.sls-tiedostolla voidaan hallita, mitkä tilat asennetaan ja ajetaan eri koneille samanaikaisesti. (Salt Project 2025)


## Infrakoodin kokeileminen paikallisesti

Aloitin hakemalla pakettipäivitykset komennolla sudo apt-get update. Sen jälkeen asensin Micro-editorin komennolla sudo apt-get -y install micro. Tämän jälkeen annoin komennon export EDITOR=micro, joka asettaa Micro-editorin oletuseditoriksi. Seuraavaksi loin kansion nimeltä hello polkuun /srv/salt komennolla sudo mkdir -p /srv/salt/hello, ja siirryin kansioon komennolla cd /srv/salt/hello.
<img width="559" height="97" alt="image" src="https://github.com/user-attachments/assets/01549349-bcea-4830-8781-e872af682a8e" />

