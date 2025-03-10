### a)

Aloitin tehtävän luomalla kolme tiedosoa, joissa hyödynsin Bash, Python ja Java kieliä. Bash ja Python olivat yksinkertaisia, ja toimivat suoraan tiedoston luonnin jälkeen ajamalla ne bash- ja python3-komennoilla. Java vaati pienen välivaiheen, jossa lähdekoodi (.java) käännetään JVM-ympäristöön sopivaan muotoon luokka-tiedostoksi (.class). Tiedostoilla on tässä vaiheessa vain rajallisesti käyttöoikeuksia, mutta tämän tehtävän kannalta sillä ei ole merkitystä, koska esimerkiksi ajo-oikeuksia (x) ei tarvita.

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

### b) Edellisten viikkotehtävien lähteiden päivittämistä ja yleistä siistimistä. Ei raportoitavaa.

### c)
