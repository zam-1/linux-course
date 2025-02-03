# H3 Hello Web Server

## a)

Asensin Apache-weppipalvelimen tuntien aikana. Asennus onnistui hyvin tunnilla saatujen ohjeiden ja tehtävänannossakin mainittujen ohjeiden avulla (https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/). Weppipalvelin ei vaatinut erillistä käynnistämistä, vaan toimi automaattisesti heti asennuksen jälkeen.

&emsp;*sudo systemctl status apache2*  
&emsp;*curl localhost*

![status.png](status.png "status")
![curltesti.png](curltesti.png "curltesti")
<br />
<br />
## b)

Tein tehtäviä hieman eri järjestyksessä, joten tässä tehtävässä on jo käytössä c) tehtävässä toteutettu oletussivun vaihto. Aloin tutkimaan /var/log/apache2/access.log -tiedostoa. Hieman yllättäen se sisälsi vain vanhoja merkintöjä tuntien aikana tehdyistä kokeiluista. Tarkistin varalta myös other_vhosts_access.log -tiedoston ja löysin tuoreet lokimerkinnät yllättäen sen sisältä. Ensimmäinen reaktioni oli tarkistaa Apache2 asennuksen oletussivu, tarkemmin ottaen sen asetustiedosto, 000-default.conf, sites-available -kansiossa. Oletusasetuksista löytyikin kaiksi lokeihin liittyvää kohtaa, jotka lisäsin omaan hattu.example.com.conf -tiedostoon.

![confchange.png](confchange.png "confchange")

Muutoksen jälkeen Access.log -tiedostoon tuli selaimella tehdyn yhteydenoton seurauksena kaksi uutta merkintää.

&emsp;*sudo tail -5 /var/log/apache2/access.log*

![access.png](access.png "access")

Ensimmäinen lokirivi kertoo onnistuneesta (200) yrityksestä hakea tietoa sivuille määritellystä juuresta. Apache2 antaa käsittääkseni oletuksena juuresta löytyvän index.html tiedoston. Seuraava rivi kertoo epäonnistuneesta yrityksestä (404, file not found). Haettu favicon.ico on käsittääkseni oletushaku, jonka selaimet tekevät löytääkseen osoiteriville ikonin (https://appwrk.com/resolving-favicon-ico-404-errors). Kyseessä ei ole siis apache2:n asetuksiin liittyvä ongelma.

Löysin avukseni ohjeet (https://httpd.apache.org/docs/2.4/logs.html), joilla tulkitsin lokitiedostoa seuraavasti:

* IP-osoite alussa yksilöi sivuihin yhteydeyden ottaneen laitteen.
* Ensimmäinen '-' kertoo ettei kohdassa haettavaa tietoa löydy. Tieto olisi liittynyt yhteyden omistajan määrittelyyn Ident-protokollan (https://en.wikipedia.org/wiki/Ident_protocol) avulla. Tieto ei lähteiden perusteella vaikuta luotettavalta tai nykyaikaiselta.
* Seuraava '-' kertoo taas tiedosta, jota ei ole tarjolla. Tässä kohdassa olisi yhteyden ottaneen käyttäjän userid, jolla pyritään tunnistamaan käyttäjä ja tämän oikeus päästä käsiksi haluttuun tietoon.
* Tiedossa on seuraavaksi yhteydenoton aika, päivämäärä ja aikavyöhyke.
* "-merkkien sisältä löytyy tieto siitä, mitä metodia yhteyteen käytetään. Tässä tapauksessa kyseessä on GET (Hakee tietoa, esim. .html ja kuvatiedostoja). Tästä osiosta löytyy myös se mitä haetaan (/ ei tässä tapauksessa ole ymmärtääkseni järjestelmän juuri, vaan apachen asetuksissa mainittu hakemistojuuri /home/otus/public_sites.hattu.example.com/) ja hakuun käytetty protokolla (HTTP/1.1).
* Tämän jälkeen seuraa kaksi numeroa, joista ensimmäinen kertoo yhteydenoton statuksen. 2-alkuiset numerot kertovat onnistuneesta yhteydenotosta, 3-alkuiset uudelleenohjauksesta, 4-alkuiset virheestä yhteydenottajan päässä ja 5-alkuiset virheestä palvelimen puolella. Toinen numero kertoo lähetetyn datan tavumäärän.
* Seuraava "-merkkien välissä olevan tieto kertoo luultavasti sen mistä yhteys on linkitetty.
* Loppuosio kertoo kokonaisuudessaan yhteydenottoon liittyvistä ohjelmista ja käyttöjärjestelmistä. Omissa lokimerkinnöissäni nämä kertoivat minun käyttäneen Firefoxia Debian-kääyttöjärjestelmässä.







