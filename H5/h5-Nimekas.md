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

Minulla oli jo IP-osoitteen takaa löytyvä Name Based Virtual Host palvelimella edellisen viikon tehtävien seurauksena. Edellisessä tehtävässä toteutettu nimipalvelimen ohjaaminen palvelimeni IP-osoitteeseen johti siis tässä tehtävässä toivoittuun lopputulokseen, eli koira.me takaa löytyviin ja tavallisena käyttäjänä muokattavissa oleviin sivuihin. Kertauksena voidaan sanoa, että loin /home/otus/public_sites/sivusto kansion, lisäsin sinne sivujen vaatimat tiedostot, tein uuden .conf tiedoston hostia varten /etc/apache2/sites-available-kansioon, aktivoin uuden tiedoston /etc/apache2/sites-enabled-kansioon ja disabloin apache2:n oletussivut. Tarkemmat tiedot löytyvät edellisen viikon raportista kohdasta d) (https://github.com/zam-1/linux-course/blob/main/H4/h4-Maailma-kuulee.md).

**conf

## c)

### Sivut

Minulla oli jo toimiva sivu, joten päädyin vain muokkaamaan sitä nimen koira-teeman mukaan. Lisäsin sivuille muutamia koiran kuvia erillisille sivuille (index.html, koira1.html jne.). Linkitys tapahtuu thumbnail-tyylisistä kuvista pääkuvan alta. Aloitin sivujen tekemisen VS coden avulla poistamalla vanhasta index.html tiedostosta kaiken turhan. Tämän jälkeen lisäsin siihen pääkuvan ja sen alle loput kuvat pienemmässä koossa. Kuin sain tämän vaiheen toimimaan (div elementtien asemointi on tuskaa...), lisäsin pienempiin kuviin linkit alasivuille. Alasivut tein kopioimalla index.html ja tekemällä siihen tarvittavat muutokset. Lopputulos oli tyydyttävä, vaikka en saanutkaan pikkukuvia riviin kännykkänäkymässä. Annoin alta löytyvän koodin validaattorille, joka ei löytänyt virheitä.

*koodit



