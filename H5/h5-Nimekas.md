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

### Alidomainit

Aloitin alidomainien tutkimisen googlehaulla ja löysin NameCheapin omat ohjeet alidomainien luomiselle (https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/). Loin ensin pieni-alidomainin A-recordilla tehtävässä a) kuvatulla tavalla ja sen jälkeen CNAME-recordilla iso-alidomainin. Tähän alidomainiin ei kelvannut isännäksi IP-osoite, joten käytin sen tilalla domainnimeä. Apua löytyi internetistä (https://dnsmadeeasy.com/post/cname-records-explained), josta selvisi ettei CNAME:n pitää aina osoittaa toiseen domainiin, ei IP-osoitteeseen.

**alidomain

### Uusi Name Based Virtual Host

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

**isokuva

## e)

## Host

host iso.koira.me

Host komento omaan alidomainiini kertoo sen olevan alias päädomainille koira.me. Hausta selviää myös nimen takana vaikuttava IP-osoite, joka on sama kuin käytössä olevalla palvelimella. En ole muuttanut nimipalvelimeni sähköpostiasetuksia, mutta niiden oletusarvot ja host-komennon ulosanti vastaavat toisiaan. Asetuksissa määritelty sillisalaatti kertoo luultavasti oleelliset tiedot käytössä olevasta edelleenlähetyspalvelusta.

**hostme

host bta3062.com

Kyseessä on Battletech-pelin modin sivusto. Tarjolla olevista lyhyistä tiedoista selviää domainin takana olevan palvelimen IP-osoite ja postin edelleenlähettämiseen liittyvät tiedot. Pieni projektisivusto tulee ilmeisesti toimeen pienemmällä postinkäsittelykapasiteetilla kuin suuri nimipalvelin.

**hostbta

host hs.fi

Helsingien sanomien palvelimesta irtoaa muista poiketen useita osoitteita. IPv4-osotteita on peräti 4. Sen lisäksi hs.fi hyödyntää myös useampaa IPv6-osotteita. Postin käsittelyssä luotetaan Microsoftin tarjontaan, Outlook:ia hyödyntäen.

**hosths

### Dig

Dig-komentoa ei löytynyt oletuksena omalta palvelimeltani, joten jouduin ensin selvittämään, miten sen saa asennettua. Asia selvisi Googlen avulla nopeasti (https://www.cloudns.net/blog/linux-dig-command-install-use/).

sudo apt-get -y update
sudo apt-get -y install dnsutils

Seuraavaksi lähdin kokeilemaan komentoa omaan palvelimeeni.

dig koira.me

**digme

* Internetistä löydettyjen tietojen (https://phoenixnap.com/kb/linux-dig-command-examples) avulla, lähdin tulkitsemaan Dig-komennon ulosantia. Ensimmäinen rivi kertoo haussa käytetyn ohjelmaversion ja haun kohteen.
* Header-osiosta selviää tietoa tehdystä hausta. Se kertoo haun tyypin (query) ja miten se meni (NOERROR, onnistunut haku). Se sisältää myös haun attribuutteja, jotka kertovat tässä tapauksessa siitä, että kyseessä oli vastaus (qr) ja sen, että haku halusi (rd) tietoa rekursiivisesti. (ra) kertoo sen, että palvelimen on mahdollista toteuttaa rekursiivinen haku. Loppuosa kertoo vastauksen sisällöstä.
* OPT PSEUDOSECTION-kertoo EDNS (Extension system for DNS) version, haun lisäasetuksia (joita tässä haussa ei ole) ja käytetyn portin. ENDS mahdollistaa suuremmat tiedostokoot vastauksissa ja perus-DNS laajemman työkalupakin.
* QUESTION ja ANSWER SECTION kertovat yhdessä sen mitä haetaan, ja mitä hakuun vastataan. Tässä tapauksessa haetaan tietoa koira.me-domainin A-record (A) tietoja internetissä (IN). Vastauksessa haettu tieto löytyy palvelimen IP-osoitteen muodossa.
* Loppuosa kertoo DNS-palvelimesta, josta tietoa kysyttiin. Tiedot ovat hakuun kulunut aika, palvelimen osoite, haun ajankohta ja vastauksen koko.

dig bta3062.com

**digbta

Tässä haussa ei ole juurikaan eroa edelliseen. Osoitteissa ja porteissa on luonnollisesti eroja, mutta vastaus on sisällöltään muuten sama.

dig hs.fi

**dighs

HS.fi:n tiedot eroavat lähinnä IP-osotteiden määrässä. Käytössä on jo HOST-komennosta tutut neljä osoitetta. Dig ei ilmeisesti oletuksena näytä IPv6-osotteita.

### Kaivetaan syvemmälle

Ensimmäiseksi lähden perehtymään siihen, mitä eri tietoja Dig-komennolla saa kaivettua esiin. Löysin avuksi sivut (https://www.cyberciti.biz/faq/linux-unix-dig-command-examples-usage-syntax/) internetissä, joilla listataan haettavia tyyppejä. Koitin muutamia haettavia tyyppejä, kuten AAAA (IPv6), NS (NameServer-nimi) ja MX (Email-palvelimien host-nimet).

dig hs.fi AAAA
dig hs.fi NS
dig hs.fi MX

**dighs6
**dighsns
**dighsmx

Mielenkiintoisin huomio ylläolevista tiedoista on se, että hs.fi käyttää Amazonin nimipalvelimia (esim. ns-1461.awsdns-54.org). Tarjolla on muitakin haettavia tyyppejä, mutta laitan niistä enää vain esimerkin CNAME-recordista, jota oma domainini iso.koira.me edustaa. Hausta selviää lähinnä juuridomain, eli koira.me.

dig iso.koira.me CNAME

*digiso

























