# H6 Salataampa

## a)

Ensimmäiseksi totesin, että sivut toimivat käynnistämällä palvelimen uudelleen ja kokeilemalla sivuja selaimessa. Sivujen vaikuttivat toimivan normaalisti, joten siirryin tehtävässä eteenpäin.

>sudo systemctl restart apache2

![sivut.png](sivut.png "Website")


### Testisertifikaatit

Aloitin asentamalla Legon, jolla on tarkoitus hakea sertificaatit salausta varten Let's Encrypt-palvelun kautta. Testasin Legoa ensin sen testiympäristössä, jonka osoitteen hain Let's Encryptin sivuilta ([letsencrypt.org](https://letsencrypt.org/fi/docs/staging-environment/)).

![acmetest.png](acmetest.png "Test Environment")
<br />
<br />
Loin /home/otus/Lego-kansion ja ajoin seuraavan komennon sertifikaatin hakemiseksi Let's Encryptin testipalvelimelta. Testaaminen kannattaa, koska Let's Encrypt ei arvosta epäonnistuineita yrityksiä oikeilta palvelimilta. Virheellisistä komennoista saattaa seurata odottelua bannin muodossa. Tarkistin komennon jälkeen, että uudesta kansioista löytyi sertifikaatin tiedostot.
 
>lego --server=https:<!-- -->//acme-staging-v02.api.letsencrypt.org/directory  
>--accept-tos --email=nimi<!-- -->@outlook.com  
>--domains=koira.me --domains=www<!-- -->.koira.me  
>--http --http.webroot='/home/otus/public_sites/sivusto' --path='/home/otus/lego'  
>--pem run

![acmeresult.png](acmeresult.png "Results")
![lego.png](lego.png "Lego")

### Oikeat sertifikaatit

Koska testi onnistui, muutin testissä käytetyn lego-kansion nimen ja loin uuden /home/otus/lego-kansion oikeita sertifikaatteja varten. Tarkistin kansion ja totesin sen olevan tyhjä ja valmis käyttöön.

![emptylego.png](emptylego.png "Empty folder")
<br />
<br />
Lähdin hakemaan oikeita sertifikaatteja sivustolleni /home/otus/lego-kansioon. Käytin samaa komentoa kuin aiemmin, mutta muutin sitä tunnilla läpi käytyjen ohjeiden mukaan. Poistin ajetusta komennosta viittauksen testiympäristön palvelimeen. Komennon jälkeen tarkistin taas, että tiedostot oli luotu oikein lego-kansioon.

>lego --accept-tos --email=email<!-- -->@outlook.com  
>--domains=koira.me --domains=www<!-- -->.koira.me  
>--http --http.webroot='/home/otus/public_sites/sivusto' --path='/home/otus/lego'  
>--pem run

![realresult.png](realresult.png "Results")
![legofolder.png](legofolder.png "Lego Folder")

### Apache2-asetukset

Lähden tekemään muutoksia palvelimen asetustiedostoon, /etc/apache2/sites-available/sivusto.conf, tunnilla tehtyjen muistiinpanojen ja tehtävänannon ohjeiden perusteella. Kopioin tiedostoon toisen virtualhostin ja muutin sen portin salatun liikenteen oletusporttiin 443. Sen jälkeen lisäsin tämän uuden virtualhostin alle rivit jotka mahdollistavat salauksen käytön (SSLEngine On) ja määrittelevät sertifikaattiin liittyvät hakemistopolut.

sudoedit /etc/apache2/sites-available/sivusto.conf

![sivuconf.png](sivuconf.png "Configuration")
<br />
<br />
Seuraavaksi aktivoin Apache2-palvelimen SSL ominaisuudet a2enmod-komennolla. Tämän jälkeen käynnistin palvelimen uudestaan ja ajoin asetusten testikomennon, joka antoi vastaukseksi lyhyesti ja ytimekkäästi 'Syntax OK'. Jäljellä oli enää palomuurin käsittely. Avasin palomuurista portin 443 ja tarkistin vielä palomuurin toiminnan ja säännöt.

>sudo a2enmod ssl  
>sudo systemctl apache2 restart  
>sudo apache2ctl configtest  
>sudo ufw allow 443/tcp  
>sudo ufw status

![ufwstatus.png](ufwstatus.png "UFW Status")

### Salauksen testaaminen

Kokeilin sivuja selaimessa ja petyin pahasti. Salaus ei näyttänyt toimivan toivotulla tavalla. Sekä koira<!-- -->.me, että www<!-- -->.koira.me kertoivat salauksen puuttuvan.

>koira<!-- -->.me  
>www<!-- -->.koira.me

![perusuns.png](perusuns.png "Unsecure")
![wwwuns.png](wwwuns.png "Unsecure")
<br />
<br />
Kokeilin kuitenkin varalta pakottaa selaimen hakemaan salattua versiota lisäämällä osoitteen alkuun https:/. Hieman yllättäen salaus näytti tämän perusteella toimivan, mutta sivut eivät jostain syystä halua ladata salattuja sivuja oletuksena. Koitin uudestaan kolmella eri laitteella, myös sellaisella jolla sivuja ei ollut aiemmin käytetty. Tuloksets olivat samanlaisia.

>https:<!-- -->//www<!-- -->.koira.me

![wwwsec.png](wwwsec.png "Secure")
<br />
<br />
Etsin Googlella apua siihen, miten saisin ohjattua kaikki porttiin 80 tulevat haut porttiin 443. Löysin hetken etsimisen jälkeen palvelimen .conf tiedostoon lisättävän Redirect ominaisuuden. Lisäsin sen salaamattoman (port 80) virtualhostin alle Apache2-dokumentaatiosta löydetyillä ohjeilla ([apache2.org](https://httpd.apache.org/docs/2.4/rewrite/remapping.html)). Tämän muutoksen jälkeen sivut vaikuttavat toimivan salattuina oletuksena.

![redirect.png](redirect.png "Redirect")
![letsenc.png](letsenc.png "Let's Encrypt")

## b)

### SSL Labs testi

Lähdin tarkastelemaan sivujani tehtävänannossa mainitulla SSL labsin työkalulla ([ssllabs.com](https://www.ssllabs.com/ssltest/)). Hetken odottelun jälkeen sain tulokseksi A-arvosanan.

![ssllabs.png](ssllabs.png "ssllabs")
![arating.png](arating.png "A-rating")

### Ongelmat

Testistä ei arvosanasta huolimatta kuitenkaan tullut täysiä pisteitä, joten tutkin tuloksia tarkemmin. Löysin niistä kolme epäkohtaa, jotka saattoivat laskea pisteitäni. Ensimmäisestä osiosta löytyi kohta DNS CAA, jota minulla ei ollut käytössä. Pikaisen googlauksen avulla löysin Let's Encryptin CAA ohjeet ([letencrypt.org](https://letsencrypt.org/fi/docs/caa/)). Ohjeiden perusteella Domainille luotu CAA-record varmistaa sen, että ainoastaan se taho, jolle recordissa on myönnetty lupa, voi myöntää domainille uusia sertifikaatteja. Kyseessä on yksi turvallisuuden osa palvelimen pyörittämisessä, mutta tässä vaiheessa on vaikea täysin hahmottaa, miten CAA-recordin puutetta voi käyttää koiruuksiin.

![caa.png](caa.png "DNS CAA")
<br />
<br />
Ohjeiden perusteella päädyin nimipalvelilmeni (Namecheap) asetuksiin. CAA-record lisättiin advanced DNS-välilehden takaa löytyviin Host Recordseihin, samalla tavalla kuin edellisten viikkojen tehtävissä. Lisäsin sinne ohjeista löydetyn esimerkin mukaisen CAA-recordin. DNS CAA-kohta SSL labsin raportissa näkyi nyt miellyttävän vihreänä. Toivottavasti tämä ei tule aiheuttamaan ongelmia myöhemmin, esimerkiksi sertifikaatin uusimisen kanssa.

![caarecord.png](caarecord.png "CAA-Record")
![caaok.png](caaok.png "DNS CAA")
<br />
<br />
Seuraavat kyseenalaiset tulokset löytyivät käytössä olevista salauksista. Ilmeisesti osa palvelimen tukemista salausmetodeista on vanhoja tai muuten vaan heikkoja.

![cipher.png](cipher.png "Ciphers")
<br />
<br />
Löysin Apachen dokumentaatiosta artikkelin ([apache.org](https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html)), joka käsitteli salausten määrittelyä palvelimen asetuksissa. Artikkelista sai sellaisen kuvan, että ne kannattanee tässä vaiheessa jättää oletusasekuksiinsa. Muutoksista voi olla enemmän haittaa kuin hyötyä. Kokeilin kuitenkin artikkelsita löytynyttä 'SSLCipherSuite HIGH:!aNULL:!MD5' riviä, jonka kuvaksen mukaisesti sallisi vain vahvat salausmetodit. Lisäsin rivin palvelimeni .conf tiedostoon muiden SSL-rivien alle ja käynnistin palvelimen uudestaan onnistuneesti. SSL Labsin raportti ei muuttunut ollenkaan.

Viimeinen huomiota herättäny kohta, oli epäonnistunut handshake. Kyseessä oli kuitenkin vain yksi epäonnistuminen monista, ja sekin tapahtui ikivanhan chromeversion kanssa. En ole tästä kohdasta erityisen huolissani.
![chrome.png](chrome.png "Hand Shake Failure")


















