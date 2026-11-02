# h2 Nuuh


## x)
### Wireshark – Getting Started
- Wireshark on johtava verkkoliikenteen kaappaus- ja analysointityökalu
- Sillä on mahdollista tallentaa kaappauksia ja avata ne pcap-tiedostona

__Tilastot__
- Endpoints
- I/O Graphs
- Protocol hierarchy

__Suodattimet__ 
- dns
- tls
- http
- tcp.port
- ip.addr
- frame contains

### Network Interface Names on Linux
- Verkkoliittymä on lähes kuin verkkokortti, mutta ei välttämättä fyysinen
- Nimen numerot yksilöivät laitteen tai sen liitäntäpaikan, joten nimi pysyy samana uudelleenkäynnistyksissä
- Omien liittymien tarkistus komennoilla ``ip a`` ja ``ip route``




## a) Linux
Kali Linux jo valmiiksi asennettuna. 

<img width="566" height="136" alt="image" src="https://github.com/user-attachments/assets/cf3087cb-1007-4f52-9435-a577ce7411db" />



## b) Ei voi kalastaa

Kali Linuxissa voin katkaista internetyhteyden, painamalla hiiren oikealla näppäimellä ethernet kuvaketta ja valitsemalla checkmarking pois "Enable Networking", jolloin internetyhteys katkeaa.

<img width="230" height="194" alt="image" src="https://github.com/user-attachments/assets/399b4fd9-c2d2-496f-9dd5-cfa83737895c" />

Nyt internet ei toimi 

<img width="890" height="464" alt="image" src="https://github.com/user-attachments/assets/e8725dee-1dcb-42fa-9484-7388899e42e2" />

Netin saa takaisin päälle laittamalla valintamerkki takaisin ruutun. 



## c) Wireshark
Wireshark on jo valmiiksi asennettu Kali Linuxiin

Voimme valita verkkoliitännän joka on ylimpänä listassa ``eth0``. Ja painaa sinistä hainevä kuvaketta vesemmassa yläkulmassa aloittaaksemme kaappauksen.

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

Tämä oli hieman hankalempaa, joten käytin läpikävelyä apuna ja tein lisäksi himan omia testejä. 

Löysin JA3 sekä JA4 sormenjäljen, joita käytetään tunnistamaan ja profiloimaan verkkoliikennettä ilman, että salattu TLS-yhteys tarvitaan purkaa.

Ne löytyivät Hello Client TLS-paketissa. ``tls.handshake.type == 1``
<img width="1622" height="334" alt="image" src="https://github.com/user-attachments/assets/138b673a-8183-480c-adb2-5bf0bb67fd8b" />

<img width="1340" height="768" alt="image" src="https://github.com/user-attachments/assets/a9b6129b-6c04-4146-927c-d9e6175fa3c9" />


- __JA4: t13d1715h2_5b57614c22b0_7121afd63204__
- __JA3: a195b9c006fcb23ab9a2343b0871e362__

Nämä syötettyäni ja3.zone-sivulle JA4 ei antanut mitään mutta JA3 antoi Firefoxin ja Chromen

<img width="1041" height="156" alt="image" src="https://github.com/user-attachments/assets/0e881838-b3c0-41ed-8883-ab6d13d4e35c" />

Testasin vielä itse molemmilla selaimilla samaan osoitteeseen menemistä ja samojen pakettien kaappaamista. 

Firefox
<img width="1352" height="824" alt="image" src="https://github.com/user-attachments/assets/a55845bf-9787-4781-999d-5605fe122431" />

Chrome
<img width="1334" height="898" alt="image" src="https://github.com/user-attachments/assets/8288a50d-92e8-4502-85d4-34a74216701d" />

Oma Firefox testaus näyttää paljon enemmän samanlaiselta kuin Chrome ja JA4 alkuosiot ovat täysin samat. Tämä ei varmaan voi varmistaa käytettyä selainta mutta ainakin saatiin jotain. 


## i) Analyysi
Sieppasin 4 pakettia Firefox selaimen käynnistyessä.

__Paketti 1__ 0ms asiakkaalta palvelimelle 53 t salattua TLS-dataa (Seq=1, Len=53)
<img width="1559" height="665" alt="image" src="https://github.com/user-attachments/assets/f176c818-5744-43c5-84b3-6513b837eb59" />

__Paketti 2__ 1,35ms palvelimelta asiakkaalle Pelkkä ACK (Ack=54)
<img width="1561" height="513" alt="image" src="https://github.com/user-attachments/assets/426155b3-397e-43c1-a868-db221fb2e28d" />

 __Paketti 3__	47ms palvelimelta asiakkaalle 33 t salattua TLS-dataa (Seq=1, Ack=54)
<img width="1561" height="612" alt="image" src="https://github.com/user-attachments/assets/7bed8ec2-7e53-4c90-96ad-5b0ebf5f2906" />

__Paketti 4__	90ms asiakkaalta palvelimelle Pelkkä ACK (Seq=54, Ack=34)
<img width="1559" height="501" alt="image" src="https://github.com/user-attachments/assets/088d7c94-9394-4a1f-b0ef-65c44de95486" />


- __10.0.2.15__ on asiakas
- __178.63.128.66__ on julkinen palvelin
- Portti 443 on HTTPS
- Portti 52664 on asiakkaan satunnainen väliaikainen portti




## Lähteet
- __Verkkoon tunkeutuminen ja tiedustelu:__ https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/
- __Network Interface Names on Linux:__ https://terokarvinen.com/network-interface-linux/
- __Wireshark - Getting Started:__ https://terokarvinen.com/wireshark-getting-started/
- __Giang 2025: H1 Sniff:__ https://github.com/gianglex/Courses/blob/6e74794c2e27752698f9bff0455a927843d9f934/Verkkoon-Tunkeutuminen-ja-Tiedustelu/h1-sniff.md#f-mit%C3%A4-selainta-k%C3%A4ytt%C3%A4j%C3%A4-k%C3%A4ytt%C3%A4%C3%A4
- __JA3.ZONE:__ https://ja3.zone/
- __peakhour.io:__ https://www.peakhour.io/learning/fingerprinting/ja3-vs-ja4/

