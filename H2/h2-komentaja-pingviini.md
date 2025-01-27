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

*cowsay -e @@ Iltaa...*

![cowsay2.png](cowsay2.png "cowsay2")

*mc*

![mc2.png](mc2.png "mc2")

## c)

**/**

Tiedostojärjestelmän ylin taso, eli juurihakemisto. Hakemiston alta löytyvät kaikki järjestelmän tiedostot ja hakemistot. Esimerkkinä hakemiston sisällöstä mainittakoon etc-hakemisto, jonka alta löytyy koko käyttöjärjestelmän laajuiisiin asetuksiin liittyviä tiedostoja.

![etc.png](etc.png "etc")
<br />
<br />
**/home/**

Tämän hakemiston sisältä löytyvät kaikkien käyttäjien kotihakemistot. Omasta virtuaalikoneestani löytyi vain yhden käyttäjän kansio.

![home.png](home.png "home")
<br />
<br />
**/home/otus/**

Käyttäjän kotihakemisto. Tämä on ainoa hakemisto johon tavallinen käyttäjä voi tallentaa tietoa pysyvästi. Hakemisto sisältää alihakemistot esimerkiksi dokumenteille, kuville ja medialle. Kansiosta löytyy myös Desktop-hakemisto, johon sisältää käyttäjän työpöydän tiedostot.

![desktop.png](desktop.png "desktop")
<br />
<br />
**/media/**

Tästä hakemistosta löytyvät ulkoiset tallennusmediat, kuten optiset asemat ja usb-tikut. Omassa järjestelmässäni löytyi vain yksi käyttäjän mukaan nimetty kansio, jonka tarkoituksena on luultavasti käytettyjen medioiden organisointi käyttäjien mukaan. Tämäkin hakemisto on tyhjä, koska virtuaalikoneeseeni ei ole liitetty mitään ylimääräistä.

![media.png](media.png "media")









