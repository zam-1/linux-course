# H6 Salataampa

## a)

Hain testiympäristön Let's Encryptin sivuilta ([letsencrypt.org](https://letsencrypt.org/fi/docs/staging-environment/)).

**acmetest

Loin Lego-hakemiston käyttäjän kotikansioon ja ajoin seuraavan komennon sertifikaatin hakemiseksi Let's Encryptin testiserveriltä.

>mkdir /home/otus/lego  
>lego --server=https:<!-- -->//acme-staging-v02.api.letsencrypt.org/directory --accept-tos --email=nimi<!-- -->@outlook.com --domains=koira<!-- -->.me --domains=www.koira.me --http --http.webroot='/home/otus/public_sites/sivusto' --path='/home/otus/lego' --pem run

**acmeresult




