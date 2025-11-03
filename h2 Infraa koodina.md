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


## Top-file: kaikkien tilojen ajaminen yhdellä komennolla

Aloitin ajamalla komennon sudoedit /srv/salt/top.sls, jolloin editori avautui ja lisäsin sinne seuraavat kohdat:
<img width="584" height="315" alt="image" src="https://github.com/user-attachments/assets/56c3ac45-34a5-411b-a0b2-13c622549754" />

Tämän jälkeen tallensin ja suljin editorin. Testasin ensin yhden tilan ajamalla sudo salt-call --local state.apply hello, joka toimi.
<img width="632" height="309" alt="image" src="https://github.com/user-attachments/assets/5de65ecf-1ee7-4f6b-817a-5cacec375e35" />

Seuraavaksi ajoin kaikki topissa listatut tilat komennolla sudo salt-call --local state.apply, ja tuloste vahvisti että tila on kunnossa (“File /tmp/hellosatu is in the correct state”).
<img width="627" height="298" alt="image" src="https://github.com/user-attachments/assets/bf5c8c64-cefa-4a76-b0b4-815e3dff75dd" />


## Viisi esimerkki-tilafunktiota

Aloitin luomalla kansiot jokaiselle viidelle tilafunktiolle komennolla sudo mkdir -p /srv/salt/{hellopkg,hellofile,helloservice,hellouser,hellocmd}.

### pkg-tilafunktio:

Siirryin hellopkg-hakemistoon komennolla cd /srv/salt/hellopkg, jonka jälkeen ajoin komennon sudoedit init.sls, joka siirsi minut editoriin.
<img width="491" height="208" alt="image" src="https://github.com/user-attachments/assets/576d5e78-623a-49cb-adcf-c2d123da68ec" />

Seuraavaksi ajoin komennon sudo salt-call --local state.apply hellopkg
<img width="635" height="326" alt="image" src="https://github.com/user-attachments/assets/be810d9d-2b47-427d-b04c-d15e98710153" />

### file-tilafunktio:

Siirryin hellofile-hakemistoon komennolla cd /srv/salt/hellofile, jonka jälkeen ajoin komennon sudoedit init.sls, jotta pääsen editoriin.
<img width="602" height="165" alt="image" src="https://github.com/user-attachments/assets/4d28eaa3-75b1-4fdb-a0e8-0553ae1ef95a" />

Seuraavaksi ajoin komennon sudo salt-call --local state.apply hellofile
<img width="636" height="336" alt="image" src="https://github.com/user-attachments/assets/4153401c-b4c6-41ed-9970-b45626491923" />

Lisäsin tiedostoon vielä sisältöä, eli menin uudestaan editoriin komennolla sudoedit init.sls.
<img width="315" height="158" alt="image" src="https://github.com/user-attachments/assets/f1eb4172-1122-4d58-a4e7-ab0194225376" />

Ajoin uudestaan komennon sudo salt-call –local state.apply hellofile.
<img width="638" height="352" alt="image" src="https://github.com/user-attachments/assets/c857ea60-25e0-4fe0-8e52-5af94c35dee0" />

Tuloste vahvisti onnistumisen rivillä File /tmp/hello.file.txt updated, eli Salt havaitsi muutoksen ja toteutti sen.

### service-tilafunktio: 

Siirryin helloservice-hakemistoon komennolla cd /srv/salt/helloservice ja siitä editoriin komennolla sudoedit init.sls.
<img width="563" height="133" alt="image" src="https://github.com/user-attachments/assets/61027f4f-d95b-4d06-9f87-1f7db3a6478c" />

Tämän jälkeen asensin OpenSSH-palvelimen komennoilla sudo apt update ja sudo apt install -y openssh-server. 
Seuraavaksi ajoin komennon sudo salt-call –local state.apply helloservice.
<img width="449" height="238" alt="image" src="https://github.com/user-attachments/assets/339b7e27-3cc2-4de7-96c1-20c8ecdc9d23" />

### user-tilafunktio:

Siirryin hakemistoon komennolla cd  /srv/salt/hellouser, jonka jälkeen editoriin komennolla sudoedit init.sls.
<img width="289" height="167" alt="image" src="https://github.com/user-attachments/assets/ecadfc7a-bbdc-41ee-a25c-2f07ff612888" />

Seuraavaksi ajoin komennon sudo salt-call –local state.apply hellouser.
<img width="485" height="403" alt="image" src="https://github.com/user-attachments/assets/b234bc4e-a8ff-4a9d-ab7e-cd7d0dd40d58" />

###  CMDDDDD


## Kahden tilafunktion SLS

Aloitin luomalla uuden kansion komennolla sudo mkdir -p /srv/salt/apache ja siirryin tähän kansioon komennolla cd /srv/salt/apache. Seuraavaksi siirryin editoriin komennolla sudoedit init.sls.
<img width="302" height="197" alt="image" src="https://github.com/user-attachments/assets/9d2d4c4c-3b2c-4b29-860b-3a66a447c8bc" />

Ajoin komennon  sudo salt-call –local state.apply apache.
<img width="626" height="521" alt="image" src="https://github.com/user-attachments/assets/9441b2ee-cc6e-4e49-9a5c-e512d3494182" />
<img width="634" height="796" alt="image" src="https://github.com/user-attachments/assets/aca7201b-d8e7-4e5e-a480-5acf49eebbee" />

Testasin vielä useamman kerran komennolla sudo salt-call --local state.apply apache, että sls-tiedostoni on idempotenssi. 
<img width="634" height="403" alt="image" src="https://github.com/user-attachments/assets/297b4e96-ac4c-48df-9ccd-ba744fecb563" />

Testasin vielä, että Apache on käynnissä ja käynnistyy myös automaattisesti. Käytin komentoa  systemctl is-active apache2 && systemctl is-enabled apache2. Komennolla curl -I http://localhost/ | head -n1 testasin, että apache vastaa http-pyyntöihin. (Red Hat Documentation 2025)
<img width="614" height="63" alt="image" src="https://github.com/user-attachments/assets/d58c004d-a5f5-4a38-b8b2-f942920c1a83" />














(Salt project 2025)








Lähteet:
Salt project 2025. Salt.states.pkg. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg.html.


