# H4 Maailma kuulee

## a)

Aloitin virtuaalipalvelimen vuokraamisen ilmottautumalla GitHub Educationiin (GitHub Student Developer Pack). Vaikka hakemus hyväksyttiin heti, jouduin odottamaan luvattuja etuja noin neljä päivää. Onneksi tajusin hake niitä hyvissä ajoin. Tarjolla olevista eduista valitsin Digital Oceanin (https://www.digitalocean.com/), jolle oli tarjolla 200$ edestä krediittejä vuoden ajaksi.

**kuva

Tilin luomisen yhteydessä lisäsin vaaditut luottokortin tiedot ja aktivoin GitHub Educationin edun. Sivuston Billing-osiosta löysin luvatut 200$ saldona ja merkinnän Education-paketin käytöstä.

**kuva

Löysin uusien palvelinten luomisen Create-napin takaa sivun oikeasta yläkulmasta. Palvelimista käytetty Droplet-nimi aiheutti aluksi lievää epävarmuutta, mutta niiden asetussivua tutkimalla totesin ne käyttööni sopiviksi. Aloitin asetusten läpikäymisen palvelimen maantieteellisestä sijainnista. Tarjolla olevista vaihtoehdoista vain kaksi Amsterdam, Frankfurt) oli EU-alueella. Näillä on tuskin suurta käytännön eroa, joten valitsin Frankfurtin.

**kuva.

Käyttöjärjestelmäksi tajrolla oli samoja vaihtoehtoja, kuin tunnilla esitellyssä palvelussa. Valitsin käyttöön tutun ja turvallisen Debianin (12 x64). Valitsin pavelimelle halvimman mahdollisen CPU-tyypin (Basic, shared CPU). Huomasin, että halvimmassa palvelimessa oli vain 512MB muistia, joten päädyin ottamaan seuraavaksi halvimman vaihtoehdon, jossa muistia oli 1GB. Hintaa valinnalle tuli 6$. Ei ole riskiä siitä, että GitHubin tarjoama 200$ ylittyy seuraavan vuoden aikana.

**kuva

Seuraavaksi tarjolla oli lisää levytilaa ja automaattista varmuuskopiointia pienellä lisämaksulla. Ohitin ne ja siirryin valitsemaan Authentication Metodia. Tunneilla suositeltiin käyttämään SSH-avaimia, joten seuraavaksi siirryin virtuaalikoneeni puolelle asentamaan tarvittavia ohjelmia. Vastoin tunnilla nähtyä esimerkkiä, minulla oli openSSH-client jo valmiiksi asennettuna, joten siirryin luomaan SSH-avaimia.

> sudo keygen

**kuva

Avaimet luotuani laitoin julkisen avaimen (id_rsa.pub) uuden palvelimen asetuksiin ja annoin sille nimeksi Key1. Lisäasetuksista otin käyttöön IPv6-verkon. Vaihdoin Hostnamen itselleni selkeämpään muotoon ja loin palvelimen Create Droplet-napista oletuksena olleeseen first-project -projektiin. Palvelimen luontiin kului noin minuutti, jonka jälkeen se löytyi first-projectin alta IP-osoitteen kanssa.

**kuva
**kuva
**kuva

## b)

