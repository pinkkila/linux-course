# Maalisuora

Tehtävät ovat Tero Karvisen opintojaksolta [Linux Palvelimet 2025 alkukevät](https://terokarvinen.com/linux-palvelimet/)

#### Laite jolla tehtävät tehdään:

- Apple MacBook Pro M2 Max
- macOS Sequoia 15.3.1
- Parallels ARM Virtual Machine
- Debian GNU/Linux 12.6

---


### a) Kirjoita ja aja "Hei maailma" kolmella kielellä.

#### Java

Päätin aloittaa Javalla ja halusin tarkistaa, mitä JKD vaihtoehtoja olisi. En muistanut millä komennolla etsiä mahdollisia paketteja joten googlailin ja löysin [debian-wikistä](https://wiki.debian.org/PackageManagement/Searching) seuraavan komennon:

```
apt-cache search packagename
```

Ja sain tulokseksi:

![img.png](img.png)


Ihmettelin hiukan, että eikö vaihtoehtoina ole mitään uudempaa kuin 17 ja ajattelin johtuuko se Debianin hitaasta päivitystahdista. Halusin nähdä mitä tapahtuu, jos laittaa uudemman version joten ajoin komennon versiolla 21, mutta pakettia ei (tietenkään) löytynyt. Katoin [Oraclen sivuilta](https://www.oracle.com/java/technologies/downloads/) ja sieltä tietysti voisi ladata uusimmat versiot JDK:sta mutta kätevyyden vuoksi asentaa package managerilla JKD 17.

```
sudo apt-get install openjdk-17-jdk
```

Seuraavaksi loin käyttäjän kotihakemiston Documents hakemistoon hello_worlds hakemiston:

![img_2.png](img_2.png)

Ja seuraavaksi tein Hello.java tiedoston:

![img_3.png](img_3.png)

Seuraavaksi käänsin ohjelman ja ajoin sen: 

```
javac Hello.java
```

```
java Hello
```

![img_1.png](img_1.png)


#### Python

Pythonin suhteen itselläni on nolla osaaminen, joten tarkistin [tästä videosta](https://www.youtube.com/watch?v=3cVAHD4mi30), että miten tämä nyt menikään. 

![img_5.png](img_5.png)

![img_4.png](img_4.png)


#### C

C:tä en ole kirjoittanut koskaan, mutta tiedän hiukan C:n historiasta ja sen merkityksestä ohjelmointiin ja ohjelmointikieliin, joten tämä on jännittävää.

Tutkein asiaa hieman ja Tero Karvisen [sivujen](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/) ja [tämän](https://www.youtube.com/watch?v=U3aXWizDbQ4) Fireship videon perusteella tein seuraavaa.

Ensin katsoin mitä seuraava komento antaa (gcc Karvisen sivuilta ja joka Fireshipin videon mukaan on olettavasti GNU C Compiler):

```
apt-cache search gcc
```

Vaihtoehtoja tuli vaikka kuinka paljon:

![img_6.png](img_6.png)

Googlailtuani ja [tämän mukaan](https://packages.debian.org/search?keywords=gcc) (kuva alla) oletteisin, että komento gcc ilman versioita asentaa paketin, jossa on itselleni sopiva kääntäjä

![img_8.png](img_8.png)

Seuraavaksi laitoin komennon 

```
sudo apt-get install gcc
```

Ja tämän jälkeen kävi ilmi, että minulla oli C-kääntäjä valmiiksi asennettuna:

![img_7.png](img_7.png)

Seuraavaksi mukailin Fireshipin videota ja Karvisen sivua ja tein hello.c nimisen tiedoston, johon kirjoitin seuraavaa:

![img_10.png](img_10.png)

ja seuraavaksi käänsin ja ajoin. 

![img_9.png](img_9.png)


### c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.

Aloitin tekemällä scriptin käyttäjän kotihakemistoon, niin kuin muistaakseni Tero neuvoi tekemään tunnilla. 

![img_12.png](img_12.png)

Seuraavaksi siirsin scriptin hakemistoon usr/local/bin ja muokkasin Teron [ohjeilla](https://terokarvinen.com/2007/12/04/shell-scripting-4/) scriptiä:

![img_11.png](img_11.png)

Komento toimii myös parallels-käyttäjällä.

![img_13.png](img_13.png)

### d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.

Asensin tehtävää varten uuden virtuaalikoneen. Tein tämän samalla tavalla kuin tehtävässä [h1](https://github.com/pinkkila/linux-course/blob/main/tehtava-h1.md).

Päätin tehdä [tästä labrasta](https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/) seuraavat tehtävät:

#### labraharjoitus d) 'howdy'

- Tee kaikkien käyttäjien käyttöön komento 'howdy'
- Tulosta haluamaasi ajankohtaista tietoa, esim päivämäärä, koneen osoite tms
- Pelkkä "hei maailma" ei riitä
- Komennon tulee toimia kaikilla käyttäjillä työhakemistosta riippumatta 

Tein seuraavan scriptin:

```
#!/bin/bash

user=$(whoami)

today=$(date +"%Y-%m-%d")

echo "Hi, $user!"
echo "Today's date is: $today"

```

Päivämäärän suhteen otin hieman mallia Teron viime tunnin esimerkistä ja selvitin geeksforgeeks [oheilla](https://www.geeksforgeeks.org/bash-script-define-bash-variables-and-its-types/) miten muuttujiin laitettua komentoja. 

Scripti toimi:

![img_14.png](img_14.png)

Seuraavaksi siirsin scriptin /usr/local/bin hakemistoon ja muutin nimen pelkäksi howdy:ksi.

![img_15.png](img_15.png)


#### labraharjoitus e) Etusivu uusiksi

- Asenna Apache-weppipalvelin
- Tee yrityksellemme "AI Kakone" kotisivu
- Kotisivu tulee näkyä koneesi IP-osoitteella suoraan etusivulla
- Sivua pitää päästä muokkaamaan normaalin käyttäjän oikeuksin (ilman sudoa). Liitä raporttiisi listaus tarvittavien tiedostojen ja kansioiden oikeuksista.


#### labraharjoitus g) Salattua hallintaa

- Asenna ssh-palvelin
- Tee uusi käyttäjä omalla nimelläsi, esim. minä tekisin "Tero Karvinen test", login name: "terote01"
- Automatisoi ssh-kirjautuminen julkisen avaimen menetelmällä, niin että et tarvitse salasanoja, kun kirjaudut sisään. Voit käyttää kirjautumiseen localhost-osoitetta


Ja [tästä labrasta](https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/) seuraavat tehtävät

#### labraharjoitus h) Käyttäjät. Käyttäjämme tarvitsevat käyttäjät Linuxiin. Tee uudet käyttäjät seuraaville: John Doe, Erik Vähäkäähkä, Akhmad Amun, Päivä Ångström, Maija-Liisa Vähäaho-Virtaoja. Listaa käyttäien salasanat raporttiin report/index.md .


#### labraharjoitus i) Etänä. Kaikki käyttäjämme haluavat käyttää modernisti etänä SSH:lla. Asenna tarvittavat palvelut. Automatisoi oman käyttäjäsi kirjautuminen julkisella avaimella.


#### labraharjoitus j) Tee käyttäjille mahdollisuus tehdä kotisivuja. Tee käyttäjille esimerkkikotisivut. (Voit kirjautua kyseisten käyttäjien tunnuksilla, koska he eivät ole vielä voineet tallentaa henkilökohtaisia tietojaan kotihakemistoonsa).



---

## Lähteet

Tero Karvinen. Linux Palvelimet 2025 alkukevät: https://terokarvinen.com/linux-palvelimet/

Debian Wiki. PackageManagementSearching: https://wiki.debian.org/PackageManagement/Searching

Oracle. Java Downloads: https://www.oracle.com/java/technologies/downloads/

YouTube: Cobb Coding. How to Write Hello World in Python: https://www.youtube.com/watch?v=3cVAHD4mi30

Tero Karvinen. Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

YouTube: Fireship. C in 100 Seconds: https://www.youtube.com/watch?v=U3aXWizDbQ4

Debian packages: https://packages.debian.org/search?keywords=gcc

Tero Karvinen. Shell Scripting: https://terokarvinen.com/2007/12/04/shell-scripting-4/

Tero Karvinen.Final Lab for Linux Palvelimet 2024 Spring: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/
 
Tero Karvinen. Final Lab for Linux Palvelimet 2024 Autumn: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/

GeeksForGeeks. Bash Script – Define Bash Variables and its types: https://www.geeksforgeeks.org/bash-script-define-bash-variables-and-its-types/



