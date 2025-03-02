# H6 Salataampa

## a)

Ensimmäiseksi totesin, että sivut toimivat normaalisti käynnistämällä palvelimen uudelleen ja kokeilemalla sivuja selaimessa.

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
![le.png](le.png "Lego Folder")

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

>koira.me  
>www.koira.me

![perusuns.png](perusuns.png "Unsecure")
![wwwuns.png](wwwuns.png "Unsecure")
<br />
<br />
Kokeilin kuitenkin varalta pakottaa selaimen hakemaan salattua versiota lisäämällä osoitteen alkuun https:/. Hieman yllättäen salaus näytti tämän perusteella toimivan, mutta sivut eivät jostain syystä halua ladata salattuja sivuja oletuksena. Koitin uudestaan kolmella eri laitteella, myös sellaisella jolla sivuja ei ollut aiemmin käytetty. Tuloksets olivat samanlaisia.

>https://koira.me  
>https://www.koira.me

![perussec.png](perussec.png "Secure")
![wwwsec.png](wwwsec.png "Secure")
<br />
<br />
Etsin Googlella apua siihen, miten saisin ohjattua kaikki porttiin 80 tulevat haut porttiin 443. Löysin hetken etsimisen jälkeen palvelimen .conf tiedostoon lisättävän Redirect ominaisuuden. Lisäsin sen salaamattoman (port 80) virtualhostin alle Apache2-dokumentaatiosta löydetyillä ohjeilla ([apache2.org](https://httpd.apache.org/docs/2.4/rewrite/remapping.html)). Tämän muutoksen jälkeen sivut vaikuttavat toimivan salattuina oletuksena.

![redirect.png](redirect.png "Redirect")
![Redirect.png](Redirect.png "Redirect")
![letsenc.png](letsenc.png "Let's Encrypt")









