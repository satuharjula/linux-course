# h1 - Viisikko


## Tiivistelmä
### Karvinen 2025: Install Salt on Debian 13 Trixie:

Saltin asentaminen Debian 13:een vaatii APT-paketin arkiston, jonka kautta Saltin paketit voidaan hakea ja varmentaa. Arkisto sisältää PGP-avaimen, jolla varmennetaan pakettien allekirjoitukset, sekä sources.list-tiedoston, josta julkinen avain löytyy.

###	Karvinen 2023: Run Salt Command Locally

Saltia käytetään usean slave-koneen hallintaan. Salt-komentoja ajetaan paikallisesti, jolloin tulos nähdään heti. Tärkeimmät tilafunktiot ovat file, service, pkg, cmd ja user. 

###	Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

Slave-koneita voi hallita palomuurin tai NAT:in takaa, myös tuntemattomassa osoitteessa. Master-koneella, jolla slave-koneita hallitaan, tarvitsee olla julkinen palvelin sekä osoite. Eri slave-koneille lisätään eri id, jotta jokainen tunnistetaan yksilöllisesti. Lopuksi master-koneella hyväksytään slave-avain.

###	Karvinen 2006: Raportin kirjoittaminen

•	Toistettavuus 

    Kuka tahansa voi toistaa työn samassa ympäristössä samalla lopputuloksella.

•	Täsmällisyys

	Työvaiheet tulee kertoa tarkasti, millä komennolla ja milloin. 
	Onnistumiset ja epäonnistumiset tulee kirjata ylös.
    Raportin kirjoitus menneessä aikamuodossa.

•	Helppulukuisuus

    Väliotsikoiden käyttö
    Huolellinen kieli
    Halutessaan myös tiivistelmä raportin alkuun

•	Lähdeviitteet

•	Plagiointi, sepittäminen ja luvaton kuvien kopiointi ehdottomasti kielletty.

## Saltin asennus Debian 13:lle

Aloitin tehtävän asentamalla wget:in, jotta saan ladattua tarvittavat tiedostot. Latasin wget:in komennoilla sudo apt-get update ja sudo apt-get install wget. Seuraavaksi loin uuden kansion komennolla mkdir saltrepo/ ja siirryin siihen komennolla cd saltrepo/.

Seuraavaksi latasin PGP-julkisen avaimen komennolla wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public ja salt.sources-tiedoston komennolla wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources. 

Seuraavaksi kopioin julkisen avaimen komennolla sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp sekä salt.sources -tiedoston komennolla sudo cp salt.sources /etc/apt/sources.list.d/. Nämä siksi, että Saltin paketit voidaan hakea ja varmentaa automaattisesti.
Tämän jälkeen päivitin komennolla sudo apt-get update ja asensin Saltin komennolla sudo apt-get install salt-minion salt-master. Seuraavaksi tarkistin komennolla sudo salt-call --version, että asennus onnistui. 

<img width="608" height="73" alt="image" src="https://github.com/user-attachments/assets/7ec99b4f-dc8e-4a28-a55c-276724584c5d" />









