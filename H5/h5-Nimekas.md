# H5 Nimekäs

## a)

### GitHub Education

Päätin hyödyntää tehtävässä GitHub education-pakettia, jonka kautta on mahdollista saada NameCheapin .me-domain vuodeksi käyttöön ilmaisesksi. Etupaketin aktivointi onnistui hyvin, mutta laitoin alkuasetuksissa vahingossa nimen osoittamaan GitHub Pages-sivuille. Tämä aiheutti lievää sekaannusta myöhemmin. Koska tuleva domain on tarkoitettu lähinnä koulutehtäviä varten, en valinnut nimeksi mitään henkilökohtaista tai ammattimaista. Yllätyksekseni koira.me oli vapaana, joten koirien ystävänä päädyin siihen.

**getu

### Nimipalvelin

Lähdin seuraamaan tunneilla tekemiäni muistiinpanoja ja löysin NameCheapin sivuilta Account-painikkeen alta listan käytössäni olevista domaineista (Domain list).

**nimi

Seuraavaksi siirryin uuden nimeni Manage-napin kautta asetusvalikkoon. Asetusten Domain-välilehdellä tajusin, että kaikki palveluun syöttämäni tiedot ovat periaatteessa julkisia. Lähtökohtaisesti kuka tahansa pääsee käsiksi nimipalvelimelle annettuihin henkilötietoihin, kuten nimi, osoite ja puhelinnumero. Kyseessä on nimien hallinnointiin liittyvä vaatimus. Tiedot löytyvät esimerkiksi whois-komennolla Linuxin komentokehotteesta.

>&emsp;whois haaga-helia.fi

**whois

Joillain nimipalvelimilla on kuitenkin käytössä tiedot piilottava ominaisuus. NameCheapilla löytyy asetuksista WithHeldForPrivacy, joka on onneksi oletuksena päällä. Suojauksen seurauksena whois-komento ei enää tarjoa hyödyllistä tietoa domainin omistajasta.

>&emsp;whois koira.me

**whois2

Seuraavaksi siirryin asetusten Advanced DNS-välilehdelle. Ensimmäiseksi huomioni kiinnittyi tunneilla nähdystä esimerkistä poikkeaviin recordeihin. Näissä oli kyse aiemmin tekemästäni valinnasta GitHub-sivuihin liittyen. Käytännössä uusi nimeni, koira.me, ohjautui nyt oletuksena tiliini linkitettyihin GitHub-sivuihin. Lisäsin uudet A-recordit osoittamaan palvelimelleni ja poistin kaikki muut. Samalla poistin myös GitHubin-sivujen asetuksista Custom Domain-maininnan.

**record
**custom

Testasin sivuja sekä koira.com, että www.koira.com osoitteilla onnistuneesti.

## b)

Minulla oli jo IP-osoitteen takaa löytyvä Name Based Virtual Host palvelimella edellisen viikon tehtävien seurauksena. Edellisessä tehtävässä toteutettu nimipalvelimen ohjaaminen palvelimeni IP-osoitteeseen johti siis tässä tehtävässä toivoittuun lopputulokseen, eli koira.me takaa löytyviin ja tavallisena käyttäjänä muokattavissa oleviin sivuihin. Kertauksena voidaan sanoa, että loin /home/otus/public_sites/sivusto kansion, lisäsin sinne sivujen vaatimat tiedostot, tein uuden .conf tiedoston hostia varten /etc/apache2/sites-available-kansioon, aktivoin uuden tiedoston /etc/apache2/sites-enabled-kansioon ja disabloin apache2:n oletussivut. Tämän jälkeen käynnistin Apache2 uudelleen. Tarkemmat tiedot löytyvät edellisen viikon raportista kohdasta d) (https://github.com/zam-1/linux-course/blob/main/H4/h4-Maailma-kuulee.md).

**conf

## c)

### Sivujen teko

Minulla oli jo toimiva sivu, joten päädyin vain muokkaamaan sitä uuden nimen koira-teeman mukaan. Lisäsin sivuille muutamia koiran kuvia erillisille sivuille (index.html, koira1.html jne.). Linkitys tapahtuu thumbnail-tyylisistä kuvista pääkuvan alta. Aloitin sivujen tekemisen VS coden avulla poistamalla vanhasta index.html tiedostosta kaiken turhan. Tämän jälkeen lisäsin siihen pääkuvan ja sen alle loput kuvat pienemmässä koossa. Kuin sain tämän vaiheen toimimaan (div elementtien asemointi on tuskaa...), lisäsin pienempiin kuviin linkit alasivuille. Alasivut tein kopioimalla index.html:n ja tekemällä tarvittavat muutokset uusiin tiedostoihin. Lopputulos oli tyydyttävä, vaikka en saanutkaan pikkukuvia riviin kännykkänäkymässä. Annoin alta löytyvän koodin validaattorille, joka ei löytänyt virheitä.

*koodit

### Sivut palvelimelle

Seuraavaksi lähdin siirtämään sivujen tiedostoja palvelimelle. Tein tämän hyödyntäen edellisten viikkojen tehtävissä käyttämääni Shared Folders-ominaisuutta VirtualBoxin asetuksissa. Jaettavaksi määritelty kansio ilmestyy /media/sf_sivut/-hakemistoon.

**shared

Kopioin hakemiston käyttäjäni kotihakemiston Documents-kansioon helpompaa käsittelyä varten ja muutin sen ja sen sisältämien tiedostojen käyttöoikeudet haluamaani muotoon.

sudo cp -r sf_sivut /home/otus/Documents
cd /home/otus/Documents
sudo chown otus:otus sf_sivut
cd sf_sivut
sudo chown otus:otus *
sudo chmod 644 *

**oikeudet

Nyt minulla oli tallessa paikallisesti käyttäjän muokattavissa olevat tiedostot ja olin valmis siirtämään ne palvelimelle. Käytin taas aiemmista tehtävistä tuttua scp-komentoa. Nyt palvelimeltani löytyi kaikki tarvittavat tiedostot oikeasta paikasta /home/otus/public_sites/sivusto/-hakemistosta. Tiedostot ovat otus-käyttäjän muokattavissa.

scp -r * otus@IP-osoite:/home/otus/public_sites/sivusto

**siirto
**kansio

Seuraavaksi testasin sivut onnistuneesti koira.me ja www.koira.me osoitteilla sekä työpöydällä ja puhelinnäkymässä.

**sivuok

## d)

Aloitin alidomainien tutkimisen googlehaulla ja löysin NameCheapin omat ohjeet alidomainien luomiselle (https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/). Loin ensin pieni-alidomainin A-recordilla tehtävässä a) kuvatulla tavalla ja sen jälkeen CNAME-recordilla iso-alidomainin. Tähän alidomainiin ei kelvannut isännäksi IP-osoite, joten käytin sen tilalla domainnimeä. Apua löytyi internetistä (https://dnsmadeeasy.com/post/cname-records-explained), josta selvisi ettei CNAME:n pitää aina osoittaa toiseen domainiin, ei IP-osoitteeseen.

**alidomain

Vapaaehtoisessa osiossa lähdin tekemään omaa Name Based Virtual Hostia iso.koira.me alidomainille. Päättelin aluksi, että minun pitää luoda uusi nimipalvelin (iso.koira.me) aiempien oppien mukaisesti ja muuttaa alkuperäisen sivun .conf tiedostoa tottelemaan koira.me:n lisäksi myös pieni- ja www-alidomaineja. Aloitin luomalla uudelle hostille kansion vanhan sivuston rinnalle. Uuteen kansioon tein yksinkertaisen index.html tiedoston, jonka tehtävän oli näyttää vain yksi kuva. Kuvan kopioin alkuperäisen sivuston tiedostoista.

**kansiokuva
**kansiokuva

Tämän jälkeen kopioin /etc/apache2/sites-available/-kansioon uuden isosivusto.conf tiedoston vanhasta sivusto.conf-tiedostosta. Tein uuteen tiedostoon muutokset, jotka viittaavat uuteen iso.koira.me-alidomainiin. Oleellisia kohtia olivat ServerName ja hakemistot.

**isokconf

Seuraavaksi muutin alkuperäisen sivusto.conf-tiedoston osoittamaan koira.me:n lisäksi myös muihin alidomaineihin. ServerNamen muutosten lisäksi otin käyttöön myös ServerAlias ominaisuuden, jonka alle listasin tarvittavat alidomainit.

**sivuconf

Asetusten muuttamisen jälkeen jäljellä oli enää uuden hostin aktivointi ja Apache2:n resetointi.

sudo a2ensite isosivusto.conf
sudo systemctl restart apache2

Kaiken tämän jälkeen, minulla oli pääsivu, joka totteli nimiä koira.me, www.koira.me ja pieni.koira.me. Sen lisäksi minulla oli toinen Name Based Virtual Host, joka totteli ainoastaan nimeä iso.koira.me.

**









