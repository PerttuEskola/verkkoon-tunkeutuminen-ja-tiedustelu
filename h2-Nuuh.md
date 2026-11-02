# h2 Nuuh


## x)




## a) Linux
Kali Linux jo valmiiksi asennettuna. 

<img width="566" height="136" alt="image" src="https://github.com/user-attachments/assets/cf3087cb-1007-4f52-9435-a577ce7411db" />



## b) Ei voi kalastaa

Kali Linuxissa voin katkaista internetyhteyden, painamalla hiire oikealla internet kuvaketta ja valitsemalla checkmarking pois "Enable Networking", jolloin internetyhteys katkeaa.

<img width="230" height="194" alt="image" src="https://github.com/user-attachments/assets/399b4fd9-c2d2-496f-9dd5-cfa83737895c" />

Nyt internet ei toimi 

<img width="890" height="464" alt="image" src="https://github.com/user-attachments/assets/e8725dee-1dcb-42fa-9484-7388899e42e2" />

Netin saa takaisin päälle laittamalla valintamerkki takaisin ruutun. 



## c) Wireshark
Wireshark on jo valmiiksi asennettu Kali Linuxiin

Voimme valita verkkoliitännän joka on ylimpänä listassa ``eth0``. Ja painaa sinisen hain evän kuvaketta vesemmassa yläkulmassa aloittaaksemme kaappauksen.

<img width="982" height="720" alt="image" src="https://github.com/user-attachments/assets/45673134-9b62-4d48-9e7f-4c203026cad1" />


Käynnistämme selaimen ja nyt näemme paketteja. 

<img width="1764" height="784" alt="image" src="https://github.com/user-attachments/assets/5bd70b3b-91ab-43be-9d37-619bdf94ae3d" />


## d) Oikeesti TCP/IP
Etsitään jokin DNS paketti jotta näemme kaikki tasot.

<img width="1287" height="129" alt="image" src="https://github.com/user-attachments/assets/a795d5b5-0c8e-479c-b04c-8253b116f219" />

- (keltainen) __Linkkikerros__ - Tarjoaa sovelluksille rajapinnan verkkopalvelujen käyttöön
- (sininen) __Internet-kerros__ - Huolehtii sovellusten välisestä luotettavasta tai nopeasta tiedonsiirrosta ja virheiden hallinnasta
- (vihreä) __Kuljetuskerros__ - Vastaa datapakettien osoittamisesta ja reitittämisestä verkkojen välillä
- (punainen) __Sovelluskerros__ -  Käsittelee fyysistä tiedonsiirtoa ja MAC-osoitteita




## e) Mitäs tuli surffattua

Kaappauksessa on käyty ainakin google.com ja terokarvinen.com sivulla. Kaapaus kestää noin 7.5 sekunttia. Siinä on lähetetty 283 pakettia. Kaikki kulkee ethernetin läpi. 

<img width="1146" height="126" alt="image" src="https://github.com/user-attachments/assets/1cf3dba9-9a7d-4bf8-9a97-7eb31420c4e7" />

## g) Minkä merkkinen verkkokortti käyttäjällä on?

MAC-osoite ``52:54:00:2f:e1:e5`` antoi tuloksen __Locally Administered Address__. Kyseessä voi olla esimerkikis virtuaalikoneen verkkokortti.

<img width="1155" height="538" alt="image" src="https://github.com/user-attachments/assets/1edf7fb1-0a8e-4355-92ed-145f77305b89" />

## h) Millä weppipalvelimella käyttäjä on surffaillut?




