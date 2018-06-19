# Konfigurator

Konfigurator je orodje, ki lajša naročnikom konguracijo lastnosti izbranih produktov. Je del Iskrine spletne strani in je dostopen v zavihku Configurator.

# Uporaba

  - Vsebino datoteke Konfigurator.html se naloži v CMS Bananadmin, na mesto, ki je rezervirano za konfigurator. CMS spremeni dele vsebine konfiguratorja na nepredviden način. Zato copy&paste neposredno iz 'source code' konfiguratorja, ki že deluje na strani ne bo deloval. Vselej je treba v CMS kopirati originalno Konfigurator.html  
  - Konfigurator je z stranjo, na kateri deluje povezan z "object literal" context. 
  -- Lastnost `url` je povezana z glavnim naslovom spletne strani. Ta nima id atributa ima pa zaenkrat edinstven class: 'productItemTittle'.
-- Lastnost `language` je povezana z HTML elemntom lang
-- Lastnost `dataPath` predstavlja pot do datotek s podatki. Konfigurator za delovanje potrebuje vsaj datoteke ProduktneSkupine.txt, InternetneSkupine.txt in Napisi.txt ter datoteke, ki vključujejo tiste produkte, ki naj jih bo konfigurator zmožen prikazati.  
```
    var context = {
        url: document.getElementsByClassName("productItemTittle")[0].innerHTML,
        language: document.documentElement.lang,
        dataPath: 'https://' + location.hostname + '/f/konfigurator/',
    }
```
- Skripta je z obrazcem za pošiljanje povezana preko html elementa z id-jem 'orderCode'. Ta prebere value tega elementa in ga shrani kot sporočilo obrazca za pošiljanje.
```
document.getElementById("orderCode").value = orderMessage;
```
### Uporaba kode na strani, ki bo prikazovala vse produkte
V datoteki Napisi.txt je kategorija mainPage v različnih jezikih. Ko se konfigurator zažene na spletni strani najprej prebere jezik strani na kateri biva, nato pa preveri, kakšen je naslov strani. Če bo konfiguratorjev `url` (torej naslov strani) enak temu stringu v kategoriji mainPage v ustreznem jeziku, takrat bo konfigurator prikazal vse produkte.
Če bi se torej gradila spletna stran, na kateri bi bilo moč pokazati vse produkte, se vsebino mape Konfigurator.txt enako naseli na stran, in se v datoteki Napisi.txt ustrezno spremeni kategorijo mainPage.
### Testiranje strani na lokalnem Express strežniku
$ git clone https://github.com/zetiko8/KonfiguratorIs.git
$ cd is-config
$ npm install
$ nodemon bin/www

# Dependencies
- [Vue](https://vuejs.org/), knjižnica za databinding.
- jQuerry