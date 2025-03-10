# a)

Aloitin tehtävän luomalla kolme tiedosoa, joissa hyödynsin Bash, Python ja Java kieliä. Bash ja Python olivat yksinkertaisia, ja toimivat suoraan tiedoston luonnin jälkeen ajamalla ne bash- ja python3-komennoilla. Java vaati pienen välivaiheen, jossa lähdekoodi (.java) käännetään JVM-ympäristöön sopivaan muotoon luokka-tiedostoksi (.class). Tiedostoilla on tässä vaiheessa vain rajallisesti käyttöoikeuksia, joten lisäsin kaikille käyttäjille ajo-oikeudet.

>micro HelloBash

```
echo Hello, Basher!
```

>micro HelloPython

```
print("Hello, Python!")
```

>micro HelloJava.java

```
public class HelloJava {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

![codes.png](codes.png "Code")

>bash HelloBash  
>python3 HelloPython  
>javac HelloJava.java  
>java HelloJava

![crun.png](crun.png "Running Code")

>ls -l

![cfiles.png](cfiles.png "File permissions")

### b) 

Edellisten viikkotehtävien lähteiden päivittämistä ja yleistä siistimistä. Ei raportoitavaa.

### c)

Aloitin luomalla kevyen Python-komennon, jossa pyydetään lehmää (cowsay) kertomaan kellonaika. Loin tarvittavan tiedoston käyttäjäni kotihakemistoon ja asetin sille ajo(x) oikeudet kaikille käyttäjille. Kun ohjelma toimi odotetusti, lisäsin tiedoston alkuun Pythonin komentotulkin rivillä '#!/usr/bin/python3'. Tämän jälkeen kopioin tidoston kaikille käyttäjille tarkotettujen komentojen /usr/local/bin/-hakemistoon. Tämän jälkeen testasin komentoa tyhjässä kansiossa. Tehtävä meni hyvin tunnilla saatujen ohjeiden avulla, ja selvisin ilman vastoinkäymisiä.

>micro cowtime

```
#!/usr/bin/python3

import subprocess
from datetime import datetime

valinta = input("Haluatko lehmän kertovan kellonajan (y/n)?: ")

if valinta == "y":
	aika = datetime.now()
	kello = aika.strftime("%H.%M")
	komento = ['cowsay', kello]
	subprocess.run(komento)
else:
	print("Ok...")
```

>chmod ugo+x cowtime

![cowp.png](cowp.png "File permissions")

>cp -n cowtime /usr/local/bin  
>cowtime (tyhjässä hakemistossa)

![cowtime.png](cowtime.png "Running Cow")

# d)

### a) Taustatiedot

Taustatiedot eivät ole tässä vaiheessa oleellisia.

### b) Tiivistelmä

Tehtävässä tehdään ilmeisesti virtuaalikoneeseen index.md tiedosto raportointia varten /home/user/report/-hakemistoon. Luon tiedoston, vaikka raportointi tapahtuu GitHubin avulla.

>mkdir /home/otus/report  
>cd /home/otus/report  
>touch index.md

![index.png](index.png "index.md")


### c) Ei kolmea sekoseiskaa

Asetan index.md tiedostolle käyttöoikeudet, jotka antavat käyttäjälle täydet oikeudet ja poistavat oikeudet muilta.

>chmod 700 index.md

tai

>chmod u+x index.md  
>chmod go-r index.md

![perm.png](perm.png "Permissions")

### d) 'howdy'

Tässä vaiheessa on hyvä asentaa micro-tekstieditori. Laitan sen samalla myös oletuseditoriksi tähän sessioon.

>sudo apt-get -y install micro  
>export EDITOR=micro



