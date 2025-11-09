# h3 Soitto kotiin


## Tiivistelmä
### Two Machine Virtual Network With Debian 11 Bullseye and Vagrant

- Vagrantin tehtävä on automatisoida virtuaalikoneiden asennusja SSH-kirjautuminen kokonaan ilman graafista käyttöliittymää.
- Enää ei käytössä 11-bullseye, vaan debian/bookworm64. (Tero Karvinen 2021)

### Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

- Saltissa yksi master-palvelin voi hallita useaa minion-palvelinta. 
- Minionin asetustiedostoon määritellään masterin IP-osoite ja id. Master hyväksyy minionin avaimet, jonka jälkeen master voi ajaa komentoja kaikille minionin koneille. (Tero Karvinen 2018)

### Salt Vagrant - automatically provision one master and two slaves

- Saltissa infra määritellään tiloina tekstitiedostoissa.
- top.sls määrittää, mitä tiloja ajetaan millekin koneille. (Tero Karvinen 2023)


## Vagrantin asentaminen

Aloitin asentamalla Vagrantin. (Vagrant)
Asensin AMD64 (Versio: 2.4.9) koneelleni. Kun asennus oli valmis, käynnistin koneeni uudelleen.  Tämän jälkeen testasin komennolla vagrant --version, että Vagrant asentui Windows-isäntäkoneelleni. Tehtävässä tarvittavan VirtualBoxin olen jo aiemmin asentanut koneelleni.
 
<img width="503" height="105" alt="image" src="https://github.com/user-attachments/assets/9ec8d4e5-565a-4747-b4fb-7679f4908791" />

## Uusi Linux-virtuaalikone

Loin ensin kansion vagrant-test.
<img width="617" height="217" alt="image" src="https://github.com/user-attachments/assets/8c995c06-d3aa-4ba2-962b-b3dd89e7f241" />

Loin vagrant tiedoston komennolla vagrant init –minimal debian/bookworm64, jonka jälkeen käynnistin virtuaalikoneen komennolla vagrant up.
<img width="886" height="220" alt="image" src="https://github.com/user-attachments/assets/f10bada4-05b4-489d-9d60-ef6b4253a2dc" />

Kirjauduin koneeeseen ssh-yhteydellä.
<img width="995" height="231" alt="image" src="https://github.com/user-attachments/assets/606684c5-4a21-4099-9dfb-03ae7bce65d8" />

Varmistin, mikä Linux-versio VM:ssä pyörii. (Gcore 2023)
<img width="828" height="208" alt="image" src="https://github.com/user-attachments/assets/63b91f33-0833-4d0d-9934-12f0755cc7b8" />

Testasin vielä komennolla vagrant status, että virtuaalikone on ylhäällä.
<img width="974" height="256" alt="image" src="https://github.com/user-attachments/assets/4345a897-339f-4413-903a-0850b000bacd" />


## Kahden Linux-tietokoneen verkko Vagrantilla

Tehtävässä mukailtu (Tero Karvinen 2021) ohjeita, soveltaen Windowsille.

Tein uuden kansion nimeltä twohost komennolla mkdir twohost ja siirryinsiihen kansioon cd twohost. Seuraavaksi avasin Vagrantfile-tiedoston muokattavaksi komennolla notepad vagrantfile, ja liitin siihen tarvittavan skriptin.Tallennettuani tiedoston käynnistin molemmat virtuaalikoneet komennolla vagrant up t001 t002.









  
