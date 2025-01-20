# H1 Oma Linux

Alkusanoina mainittakoon, että en ennen tätä tehtävää tiennyt Linuxin käytöstä juuri mitään, mutta olen sen kuitenkin asentanut useamman kerran vuosien varrella. Sama pätee muihinkin käyttöjärjestelmiin MS-DOS ajoista lähtien. En siis odottanut tämän tehtävän osalta suurempia ongelmia. Hankaluudet alkavat luultavasti vasta seuraavien tehtävien parissa.

## VirtualBox

Aloitin VirtualBoxin asentamisen hakemalla asennuspaketin VirtuaBoxin sivuilta (https://www.virtualbox.org/wiki/Downloads) tehtävän ohjeiden mukaisesti. Valitsin tarjolla olevista vaihtoehdoista Windows Hosts-version. Asennus sujui ilman ongelmia. Olin asentanut edellisen periodin Python kurssilla liittyviä sidonnaisuuksia, joten VirtualBoxin asennuksella ei ollut niistä huomauttamista. Valitsin VirtualBoxin aloitusnäkymästä oikealta 'Expert mode' vaihtoehdon ja aloitin uuden virtuaalikoneen luomisen 'New' napista.

Eteeni auenneissa virtuaalikoneen asetuksissa oli joitain eroja tehtävän ohjeiden kuvitukseen verrattuna. Käyttöjärjestelmävalikon alla oli 'Edition' kohta, jota en voinut muuttaa. Ohitin sen huoletta, koska se ei vaikuttanut tehtävän kannalta oleelliselta. Rautavalikossa oli poikkeuksena CPU asetus prosessoreiden määrälle. Jätin sen oletusarvoonsa yhteen. Kovalevyn asetuksissa suurimpana erona oli 'Dynamically allocated' vaihtoehdon puuttuminen. Koska vastaavalla paikalla oli asetus 'Pre-allocate Full Size', oletin dynaamisen allokoinnin olevan nykyään oletuksena. Tarkastettuni asetusten yhteenvedon, loin virtuaalikoneen, joka ilmestyi näkyviin vasempaan laitaan. Lähdin asettamaan .iso tiedostoa optiseen asemaan, mutta yllätyksekseni huomasin, että asia oli jo oletuksena kunnossa.

Käynnistin virtuaalikoneen tuplaklikkaamalla ja muutaman sekuntin sisällä eteeni aukesi Debianin boottivalikko.









