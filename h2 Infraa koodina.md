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

Aloitin hakemalla pakettipäivitykset komennolla sudo apt-get update. Sen jälkeen asensin Micro-editorin komennolla sudo apt-get -y install micro. Tämän jälkeen annoin komennon export EDITOR=micro, joka asettaa Micro-editorin oletuseditoriksi. Seuraavaksi loin kansion nimeltä hello polkuun /srv/salt/ komennolla sudo mkdir -p /srv/salt/hello, ja siirryin kansioon komennolla cd /srv/salt/hello.
<img width="559" height="97" alt="image" src="https://github.com/user-attachments/assets/01549349-bcea-4830-8781-e872af682a8e" />
Seuraavaksi ajoin komennon sudoedit init.sls, joka avasi Micro-editorin, jonka juuri asensin. Lisäsin editoriin seuraavat asiat: 
<img width="408" height="314" alt="image" src="https://github.com/user-attachments/assets/65cd75ec-87b9-48bc-a290-c5775b2f7c01" />
Ajoin komennon sudo salt-call --local state.apply hello, joka tulosti kuvan mukaisen yhteenvedon:
<img width="637" height="369" alt="image" src="https://github.com/user-attachments/assets/c881354f-0780-474e-b717-2ce62e2c5b22" />
Tuloste kertoi, että tiedosto /tmp/hellosatu on luotu onnistuneesti, koska siinä lukee file /tmp/hellosatu created. Varmistin vielä komennolla ls /tmp/hellosatu, että tiedosto on oikeasti olemassa. Kun saman komennon ajaa uudelleen, changed (1) poistuu, koska mitään ei tarvitse enää muuttaa. Tämä osoittaa, että Salt toimii oikein ja tila on idempotentti.
<img width="547" height="39" alt="image" src="https://github.com/user-attachments/assets/8c050f5e-aa57-41b9-ae31-908b29dff572" />
<img width="547" height="39" alt="image" src="https://github.com/user-attachments/assets/9aabf67f-8d4b-4837-a263-0953e7e1612f" />
Siirryin vielä takaisin hellosatu -tiedostoon ja lisäsin sisällön ”Hei maailma!”.
<img width="616" height="357" alt="image" src="https://github.com/user-attachments/assets/03b1c48d-da57-47e2-a3a3-4b420df5aa6e" />
<img width="624" height="55" alt="image" src="https://github.com/user-attachments/assets/31c89533-ec4b-43d1-b8bc-cbbb1918041d" />
Tarkistin vielä komennolla cat /tmp/hellosatu, että tiedosto oli olemassa ja siinä näkyi haluttu sisältö.










