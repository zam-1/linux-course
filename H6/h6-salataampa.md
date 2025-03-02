# H6 Salataampa

## a)

Ensimmäiseksi totesin, että sivut toimivat normaalisti käynnistämällä palvelimen uudelleen ja kokeilemalla sivuja selaimessa.

>sudo systemctl restart apache2

*sivut


Hain testiympäristön Let's Encryptin sivuilta ([letsencrypt.org](https://letsencrypt.org/fi/docs/staging-environment/)).

**acmetest

Loin /home/otus/Lego-kansion ja ajoin seuraavan komennon sertifikaatin hakemiseksi Let's Encryptin testipalvelimelta. Tarkistin komennon jälkeen, että uudesta kansioista löytyi sertifikaatin tiedostot.
 
>lego --server=https:<!-- -->//acme-staging-v02.api.letsencrypt.org/directory  
>--accept-tos --email=nimi<!-- -->@outlook.com  
>--domains=koira.me --domains=www<!-- -->.koira.me  
>--http --http.webroot='/home/otus/public_sites/sivusto' --path='/home/otus/lego'  
>--pem run

**acmeresult

Muutin testissä käytetyn lego-kansion nimen ja loin uuden /home/otus/lego-kansion. Tarkistin kansion ja totesin sen olevan tyhjä.

**emptylego

Koska testi toimi moitteetta, lähdin hakemaan oikeita sertifikaatteja sivustolleni /home/otus/lego-kansioon. Käytin samaa komentoa kuin aiemmin, mutta muutin sitä tunnilla läpi käytyjen ohjeiden mukaan. Poistin ajetusta komennosta viittauksen testiympäristön palvelimeen. Komennon jälkeen tarkistin taas, että tiedostot oli luoti lego-kansioon.

>lego --accept-tos --email=email@outlook.com  
>--domains=koira.me --domains=www.koira.me  
>--http --http.webroot='/home/otus/public_sites/sivusto' --path='/home/otus/lego'  
>--pem run

**realresult
**lego






