# H2 Komentaja Pingviini

## Rauta & VirtualBox asetukset

OS:      Windows 11 Pro  
CPU:     Intel Core i7-9700k @ 3.6GHz, 8 Core  
Emolevy: Z390 AORUS ELITE-CF  
Muisti:  32GB DDR4-3200  
OS SSD:  250GB Samsung EVO 860, Vapaana 116GB  
VM SSD:  1TB Samsung EVO 860, Vapaana 280GB  
GPU:     Nvidia RTX 4070 12GB  
Näyttö:  MSI OPTIX MAG341CQ

VirtualBox asetukset:  
Oletusasetukset, muutamia poikkeuksia lukuunottamatta:  
OS: Debian 12.9.0  
Video Memory: 256MB  
Base Memory: 8192MB  
Harddisk: 60GB

## a)

Käytin Micron asentamiseen edelliseltä tunnilta tuttua komentoa. Asennus sujui ilman virheilmoituksia. Tämän jälkeen testasin ohjelmaa luomallta test.txt tiedoston onnistuneesti.

*sudo apt-get install micro*
*micro test.txt*

![MicroA.png](MicroA.png "MicroA")
<br />
<br />
## b)

Aloitin tehtävän etsimällä tarkoitukseen sopivia ohjelmia. En tiennyt etukäteen mitään hyviä vaihtoehtoja, joten kahlasin läpi useita Reddit-keskusteluita, tein Google-hakuja ja selasin Linux.fi:n wikiä. Useassa lähteessä oli mainittu TLDR-ohjelma, jonka tarkoitus on tiivistää manuaaleja (man) helpommin pureskeltavaan muotoon. Toiseksi ohjelmaksi valikoitui Midnight Commander (https://www.linux.fi/wiki/Midnight_Commander). Käytin MS-DOS aikoina sen esikuvana toiminutta Norton Commanderia, joten nostalgian yliannostus oli lähellä ohjelman avauduttua. Kolmas valitsemani ohjelma oli tunneillakin nähty Cowsay, joka vaikutti hauskalta. Kukapa ei lehmistä pitäisi.

Aloitin asennuksen etsimällä ohjelmien paketeille nimiä 'apt search' - komentoa hyödyntämällä. Kaikkien hakujen listauksissa oli ohjelmia, jotka eivät päällisin puolin liittyneet käytettyihin hakutermeihin mitenkään. Onneksi joukosta löytyivät myös haluamani paketit.

*apt-search tldr*, *apt-search cowsay*, *apt search midnight commander*

![tldr.png](tldr.png "tldr")
![cowsay.png](cowsay.png "cowsay")
![mc.png](mc.png "mc")
<br />
<br />
Komento kaikkien ohjelmien asentamiseen kerrallaan syntyi arvaamalla edellisen tunnin mkdir komentojen avulla. Jos kansioita voi luoda tietyllä tavalla usemman kerrallaan, niin miksei sama logiikka toimisi myös asennuksissa. Asennus alkoi ja loppui ilman virheilmoituksia. Tämän jälkeen testasin ohjelmia seuraavilla komennoilla:

*tldr cowsay*

![tldr2.png](tldr2.png "tldr2")
<br />
<br />
*cowsay -e @@ Iltaa...*

![cowsay2.png](cowsay2.png "cowsay2")
<br />
<br />
*mc*

![mc2.png](mc2.png "mc2")
<br />
<br />
## c)

**/**

Tiedostojärjestelmän ylin taso, eli juurihakemisto. Hakemiston alta löytyvät kaikki järjestelmän tiedostot ja hakemistot. Esimerkkinä hakemiston sisällöstä mainittakoon etc-hakemisto, jonka alta löytyy koko käyttöjärjestelmän laajuiisiin asetuksiin liittyviä tiedostoja.

*ls -p*

![juuri.png](juuri.png "juuri")
<br />
<br />
**/home/**

Tämän hakemiston sisältä löytyvät kaikkien käyttäjien kotihakemistot. Omasta virtuaalikoneestani löytyi vain yhden käyttäjän kansio.

*ls-p*

![home.png](home.png "home")
<br />
<br />
**/home/otus/**

Käyttäjän kotihakemisto. Tämä on ainoa hakemisto johon tavallinen käyttäjä voi tallentaa tietoa pysyvästi. Hakemisto sisältää alihakemistot esimerkiksi dokumenteille, kuville ja medialle. Kansiosta löytyy myös Desktop-hakemisto, joka sisältää käyttäjän työpöydän tiedostot.

*ls -p*  
*cd desktop*  
*echo test > test.txt*  
*ls*

![desktop.png](desktop.png "desktop")
<br />
<br />
**/etc/**

Tämä hakemisto sisältää käyttöjärjestelmän laajuiset asetukset selkokielisinä tekstitiedostoina. Hakemisto sisältää esimerkiksi asetukset aiemmin asentamalleni Midnight Commander-ohjelmalle. Siirryin ohjelman kansioon ja tutkin sen sisältöä. Valitsin tarkasteluun mc.keymap tiedoston, josta näytin viisi ensimmäistä riviä. Riveillä näkyy muutettavissa olevia näppäinasetuksia. Käytetty head-komento (ja myöhemmin käytetty tail-komento) löytyivät Google-haun AI-osasta (How to see first lines of a file in Linux command line?)

*cd mc*  
*ls*  
*head -n 5 mc.keymap*

![etc.png](etc.png "etc")
<br />
<br />
**/media/**

Tästä hakemistosta löytyvät ulkoiset tallennusmediat, kuten optiset asemat ja usb-tikut. Omassa järjestelmässäni löytyi vain yksi käyttäjän mukaan nimetty kansio, jonka tarkoituksena on luultavasti käytettyjen medioiden organisointi käyttäjien mukaan. Tämäkin hakemisto on tyhjä, koska virtuaalikoneeseeni ei ole liitetty mitään ylimääräistä.

*ls -p*

![media.png](media.png "media")
<br />
<br />
**/var/log/**

Tähän hakemistoon sisältyy käyttöjärjestelmän laajuisten lokien tiedostot. Hakemistoa tutkimalla löysin alihakemiston apt, joka sisältää history.log tiedoston. Kyseisestä tiedostosta löytyi aiemmin ajamiani apt-get komentoja.

*ls -p*  
*cd apt*  
*ls -p*  
*tail -n 5 history.log*

![log.png](log.png "log")
<br />
<br />
## d)

Koitin ensin grep-komentoa Micron manuaaliin putkea hyödyntämällä. Tarkoituksena oli löytää manuaalista quit-pikanappi ilman koko manuaalin selaamista. Kokeilu onnistui mainiosti.

*man micro|grep "quit"*

![mgrep.png](mgrep.png "mgrep")
<br />
<br />
Kokeilin seuraavaksi grep-komentoa kotihakemistosta käsin aiemmin mainittuun history.log tiedostoon ja sain tulokseksi pari riviä tekstiä, jotka sisälsivät 'cowsay' hakusanan. Valitsin riveistä oleellisimman, eli sen jossa oli listattu tehtävässä b) käytetty asennuskäsky ja tarkensin grep-komentoa lisäämällä sen hakuehtoon tarvittavat tiedot. Sen jälkeen hioin komentoa ottamalla mukaan '-C 3' valinnan, jonka piti käsittääkseni näyttää kolme riviä halutun rivin molemmilta puolilta. Tuloksena sain grep-komennon antamaan history.log tiedostosta kaikki rivit, jotka liittyivät haluttuun asennustapahtumaan.

*grep "cowsay" /var/log/apt/history.log*  
*grep -C 3 "apt-get install tldr cowsay mc" /var/log/apt/history.log*

![grepcow.png](grepcow.png "grepcow")
<br />
<br />

## e)

Alkuperäisenä tavoitteena oli käyttää yhden tiedoston (cow.txt) sisältöä (yksi rivi tekstiä) grep-kommenon ohjeistuksena toisen tiedoston (aiemmin käytetty history.log) tutkimiseen. Tämän jälkeen grep-komennon ulosanti siirtyisi lehmän suuhun cowsay-ohjelman kautta. Lopullisen tuotoksen oli tämän jälkeen tarkoitus korvata ensimmäisen tiedoston sisältö.

Löysin grepin ohjeista -f valinnan, joka vaikutti hyvältä.

*cat cow.txt|grep -f /var/log/apt/history.log*

Komento näytti vain cow.txt -tiedoston sisällön, joten se ei toiminut toivotulla tavalla. Seuraavaksi koitin yksinkertaistaa komentoa poistamalla putken kokonaan ja muokkaamalla grep-komentoa mielestäni loogisella tavalla.

*grep -f cow.txt /var/log/apt/history.log*

Tämä käsky toimi odotetulla tavalla ja näytti halutun rivin history.log -tiedostosta. Valitettavasti se tarkoitti myös sitä, että koko putki-idea oli tarpeeton. Halusin kuitenkin yrittää ratkaista ongelman alkuperäisen suunnitelman mukaisesti.

*cat cow.txt|grep -f - /var/log/apt/history.log*

Yhden vaivaisen - merkin takia käytin aivan liian kauan aikaa grepin ohjeiden parissa. Ongelma selvisi lopulta lähinnä kokeilemalla eri vaihtoehtoja. En ymmärrä täysin vieläkään, mitä - tarkalleen tekee komennossa.

*cat cow.txt|grep -f - /var/log/apt/history.log|cowsay*

Seuraava vaihe onnistui helposti, joten jäljelle jäi vain lehmän ulkoasun hiominen ja alkuperäisen tiedoston sisällön korvaaminen.

*cat cow.txt|grep -f - /var/log/apt/history.log|cowsay -e @@ -T U > cow.txt*

Cow.txt tiedoston korvaaminen lehmällä onnistui, mutta jostain syystä lehmän puhekupla tyhjeni toimenpiteen seurauksena. En keksinyt ongelmaan ratkaisua, joten tyydyin sisällön korvaamisen sijaan täydentämään sitä. Lopullisessa cow.txt tiedostossa on siis alkuperäinen sisältö ja cowsay:n tuottama lehmä, joka kertoo meille rivin history.log tiedostosta. Lopullinen komento on:

*cat cow.txt|grep -f - /var/log/apt/history.log|cowsay -e @@ -T U >> cow.txt*

![historycow.png](historycow.png "historycow")
<br />
<br />














