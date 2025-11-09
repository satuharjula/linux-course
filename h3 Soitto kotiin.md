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

<img width="897" height="370" alt="image" src="https://github.com/user-attachments/assets/8b7ab7f7-1b7e-47ae-b54a-0116ff0ebb7c" />

Ajoin komennon vagrant status, jolloin näin molempien koneiden olevan käynnissä ja asennuksen onnistuneen.

<img width="993" height="291" alt="image" src="https://github.com/user-attachments/assets/c965f16b-42ca-4a17-9057-2b7342d69626" />

Otin ssh -yhteyden t001 komennolla vagrant ssh t001, jonka jälkeen pingasin toista luomaani konetta t002 komennolla ping -c 1 192.168.88.102.

<img width="996" height="390" alt="image" src="https://github.com/user-attachments/assets/34f52d1b-3a4e-4cce-b33e-c6f740c65cb6" />

Poistuin ssh-yhteydestä t001 exit:llä, jonka jälkeen kokeilin vuorostaan pingata koneella t002 konetta t001. Sekin onnistui.

<img width="988" height="402" alt="image" src="https://github.com/user-attachments/assets/13fc2f54-9e88-4377-9b63-962637a6a84a" />

Kokeilin vielä yhteyttä Internetiin ja sekin onnistui. 

<img width="903" height="206" alt="image" src="https://github.com/user-attachments/assets/3b6a6f92-5dae-489f-b1c5-23ecd79c1bf1" />

## Salt-master asennus

Tehtävässä mukailtu (Tero Karvinen 2018) ohjeita.

Ajoin komennon vagrant up, jonka jälkeen muodostin ssh-yhteyden t001. Loin kansion keyrings komennolla mkdir -p /etc/apt/keyrings. Ajoin komennon sudo apt-get update, jonka jälkeen asensin curl:in komennolla sudo apt-get install curl.
Tämän jälkeen latasin ja lisäsin julkisen avaimen seuraavalla komennolla:

<img width="1004" height="68" alt="image" src="https://github.com/user-attachments/assets/be0238a7-a88b-4c10-80ae-8b725445989e" />

Lisäsin Saltin pakettivaraston APT:n lähdeluetteloon.

<img width="958" height="69" alt="image" src="https://github.com/user-attachments/assets/68f2ede0-5eff-4006-a77a-0e24ab1f8efc" /> (Salt project.io 2024)

Seuraavaksi ajoin komennon sudo apt-get update, jonka jälkeen asensin salt-masterin komennolla sudo apt-get -y install salt-master.

<img width="969" height="492" alt="image" src="https://github.com/user-attachments/assets/adc658df-ac3b-4166-aa6d-d1aa9c776c2b" />

Se onnistui. 

## Salt-minion asennus

Tehtävässä mukailtu (Tero Karvinen 2018) ohjeita.

Muodostin ssh-yheyden t002. Ajoin komennon sudo apt-get update, jonka jälkeen asensin curl:in komennolla sudo apt-get install curl.
Seuraavaksi loin kansion keyrings, komennolla mkdir -p /etc/apt/keyrings.
Sitten latasin ja lisäsin julkisen avaimen seuraavalla komennolla:

<img width="1004" height="48" alt="image" src="https://github.com/user-attachments/assets/75cdce5a-2fd7-4b84-99bf-8901746a7058" />

Lisäsin Saltin pakettivaraston APT:n lähdeluetteloon.

<img width="1004" height="128" alt="image" src="https://github.com/user-attachments/assets/16331741-7ec1-4419-af2b-5c3a9440d97a" /> (Salt project.io 2024)

Seuraavaksi ajoin komennon sudo apt-get update, jonka jälkeen asensin salt-minionin komennolla sudo apt-get -y install salt-minion.

<img width="969" height="778" alt="image" src="https://github.com/user-attachments/assets/7a7b584a-ead6-4758-b16b-2e84e3c82b08" />

Se onnistui. 

<img width="969" height="778" alt="image" src="https://github.com/user-attachments/assets/17445fb4-0c0c-4508-9f3d-8fe45d47d2c9" />

Seuraavaksi ajoin komennon sudoedit /etc/salt/minion, joka avasi minulle Saltin asetustiedoston. Muokkasin tiedostossa kohtaa #master: salt. Muutin sen näyttämään tältä:

<img width="1004" height="643" alt="image" src="https://github.com/user-attachments/assets/3eb3f141-ce87-4119-954f-c59227a6c917" />

Tallensin muutokset ja käynnistin minionin uudelleen komennolla sudo systemctl restart salt-minion. 
Tarkistin vielä minionin tilan seuraavasti:

<img width="1004" height="363" alt="image" src="https://github.com/user-attachments/assets/8f7a8ee5-fdc3-45fb-b835-d1c7b0563ba2" />

Seuraavaksi palasin masterille (t001) hyväksymään avaimen.

<img width="695" height="209" alt="image" src="https://github.com/user-attachments/assets/6a584467-7bca-41e2-8bde-ba949c56d8b0" />

Kokeilin seuraavaa komentoa ja sain vastauksen minionilta.

<img width="695" height="125" alt="image" src="https://github.com/user-attachments/assets/ae601539-6c60-454e-86ef-9159582609ec" />

## pkg ja service verkon yli

Asensin minionille paketit tree ja apache2 seuraavissa kuvissa näkyvillä komennoilla.

<img width="920" height="711" alt="image" src="https://github.com/user-attachments/assets/176d5263-ca96-449a-85bc-6828a08dbdcd" />
<img width="1004" height="36" alt="image" src="https://github.com/user-attachments/assets/d6455553-c95c-4b2c-affd-e56ac9eb4d58" />
<img width="538" height="219" alt="image" src="https://github.com/user-attachments/assets/c4144dee-69c1-4731-b2b9-f6e7e07e31a5" />

Seuraavassa kuvassa näkyvällä komennolla varmistin, että Apache on käynnissä ja käynnistyy bootissa.

<img width="1004" height="444" alt="image" src="https://github.com/user-attachments/assets/63682162-bfb4-45d1-98aa-9f5be9ee911f" />


## Lähteet

Karvinen, T. 28.3.2023. Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file.
Karvinen, T. 28.3.2018. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. 
Karvinen, T. 11.4.2021. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/.
Saltproject.io. 28.10.2024. Luettavissa: https://saltproject.io/blog/salt-project-package-repo-migration-and-guidance/. 
Vagrant. Install Vagrant. Luettavissa: https://developer.hashicorp.com/vagrant/docs/installation. 






































  
