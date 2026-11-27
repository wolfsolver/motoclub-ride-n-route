# Manuale Utente — MotoClubApp

Benvenuto nel manuale ufficiale di **MotoClubApp**, la piattaforma multi-tenant dedicata ai Moto Club, agli Ambassador del mototurismo e ai motociclisti (*Rider*).

Questo documento descrive tutte le funzionalità disponibili nell'applicazione e spiega passo dopo passo come utilizzarle in base al proprio ruolo.

---

## Indice

1. [Panoramica e Ruoli della Piattaforma](#1-panoramica-e-ruoli-della-piattaforma)
2. [Navigazione e Struttura dell'Interfaccia](#2-navigazione-e-struttura-dellinterfaccia)
3. [Installazione come App (PWA)](#3-installazione-come-app-pwa)
4. [Accesso, Registrazione e Sicurezza Account](#4-accesso-registrazione-e-sicurezza-account)
5. [Area Personale: Profilo, Notifiche Push e Garage Digitale](#5-area-personale-profilo-notifiche-push-e-garage-digitale)
6. [Home, Geolocalizzazione e Navigazione Mappe](#6-home-geolocalizzazione-e-navigazione-mappe)
7. [Itinerari e Repository GPX](#7-itinerari-e-repository-gpx)
8. [Eventi, Iscrizioni (RSVP) e Check-in](#8-eventi-iscrizioni-rsvp-e-check-in)
9. [Club, Cambio Contesto e Tessera Digitale](#9-club-cambio-contesto-e-tessera-digitale)
10. [Strumenti per Coordinatori del Club](#10-strumenti-per-coordinatori-del-club)
11. [Merchandising del Club](#11-merchandising-del-club)
12. [Ambassador, Bundle e Itinerari Premium](#12-ambassador-bundle-e-itinerari-premium)
13. [Console SuperAdmin (`/superadmin`)](#13-console-superadmin-superadmin)

---

## 1. Panoramica e Ruoli della Piattaforma

MotoClubApp centralizza in un'unica Progressive Web App (PWA) la gestione dei Moto Club, l'organizzazione dei motogiri, la condivisione di tracce GPX, il merchandising e la tessera digitale.

Le funzionalità visibili dipendono dal tuo ruolo nel contesto attivo:

| Ruolo | Descrizione | Cosa può fare |
| :--- | :--- | :--- |
| **Ospite** (*Guest*) | Visitatore non autenticato | Consulta in sola lettura i contenuti pubblici (club pubblici, eventi pubblici, itinerari pubblici, vetrina Ambassador, teaser) e verifica le tessere via QR (`/verify/:tokenId`). |
| **Rider Registrato** | Utente con account verificato | Gestisce Profilo e Garage Digitale, pubblica itinerari pubblici/privati, partecipa a eventi pubblici, segue Club (`Follower`) e Ambassador, richiede l'iscrizione a un Club o la creazione di un nuovo Club. |
| **Follower** | Utente che segue un Club | Riceve aggiornamenti del Club e visualizza anteprime (*teaser*) degli eventi riservati ai soci, senza accedere ai dettagli interni né agli RSVP riservati. |
| **Socio** (*Member*) | Membro ufficiale di un Club | Può passare alla **Modalità Club**, accedere a eventi `Solo Soci`, itinerari del Club, Tessera Digitale con QR di verifica e Catalogo Merchandising. |
| **Coordinatore** | Amministratore di un Club | Ha pieno controllo operativo sul proprio Club: approva/importa soci, gestisce rinnovi, crea eventi ufficiali, effettua il check-in ai ritrovi, gestisce ordini merchandising, invia avvisi broadcast e configura il profilo del Club. |
| **Ambassador** | Creator verificato di mototurismo | Può pubblicare itinerari **Premium**, gestire **Bundle** e autorizzare i propri Follower all'accesso completo alle tracce. |
| **SuperAdmin** | Amministratore globale | Gestisce la console `/superadmin`: attiva/sospende i Club, approva gli Ambassador e governa l'elenco ufficiale delle marche moto. |

> **Nota Multi-Club:** I ruoli di Socio e Coordinatore sono legati al singolo Club. Puoi essere *Coordinatore* nel Club A e semplice *Socio* nel Club B, passando rapidamente dall'uno all'altro.

---

## 2. Navigazione e Struttura dell'Interfaccia

L'interfaccia dell'app (`/app`) è organizzata in tre aree principali:

### Barra Superiore (TopBar)
* **Pulsante Sinistro (Contesto Operativo):** apre il menu laterale sinistro per cambiare contesto (*Free Rider* o uno dei tuoi *Club*) e accedere agli strumenti del Club o agli Ambassador.
* **Titolo Centrale:** indica il contesto attivo (*Free Rider*, *Ospite* oppure il nome del *Club* selezionato, con i colori tema del Club).
* **Pulsante Destro (Area Personale):** apre il menu laterale destro. Mostra:
  * un **badge numerico rosso** se hai notifiche non lette;
  * un **pallino giallo/ambra** se il tuo profilo o le notifiche push richiedono completamento.

### Barra Inferiore (4 Schede Principali)
1. **Home:** riepilogo personalizzato, avvisi di completamento profilo/push, prossimi eventi, itinerari in evidenza e classifiche Club/Ambassador.
2. **Itinerari:** repository delle tracce GPX e dei percorsi, suddiviso per ambito (`Club`, `Pubblici`, `Privati`, `I miei`).
3. **Eventi:** calendario delle uscite e dei raduni (`Club`, `Pubblici`, `Iscritti`, `I miei`).
4. **Club:** elenco e ricerca dei Moto Club attivi, richieste di adesione e creazione di nuovi Club.

### Menu Sinistro (`Contesto Operativo`)
* **Cambio Contesto:** seleziona **Usa come Free Rider** oppure uno dei Club a cui sei iscritto (`I Miei Club`).
* **Gestione / Altri Club:** apre la vista di scoperta e gestione dei Club.
* **Sezione Club Attivo** *(visibile solo in Modalità Club)*:
  * **La mia tessera**
  * **Merchandising**
* **Coordinamento Club** *(visibile solo ai Coordinatori in Modalità Club)*:
  * **Approvazione Richieste e Membri**
  * **Gestione Ordini Merchandising**
  * **Gestione Profilo Club**
  * **Avviso ai Soci del Club**
* **Community Ambassador** *(visibile a tutti, inclusi Ospiti)*:
  * **Ambassador** (Directory pubblica)
  * **Pannello Bundle & Follower** *(visibile solo agli Ambassador approvati)*

### Menu Destro (`Area Personale`)
* **Profilo Rider** (con eventuale badge `Da completare`)
* **Notifiche** (con contatore notifiche non lette)
* **Garage Digitale**
* **I miei ordini merchandising** (storico personale valido su tutti i Club)
* **Lingua** (`Italiano` / `English`)
* **Disconnetti** e **Build Info** in fondo al menu (`(c) 2026 - Build ...`)

---

## 3. Installazione come App (PWA)

MotoClubApp è una **Progressive Web App**: può essere installata sullo smartphone o sul computer senza passare dagli store tradizionali. L'installazione è fortemente consigliata e **obbligatoria su iPhone/iPad per ricevere le Notifiche Push**.

* **iPhone / iPad (Safari, iOS 16.4+):**
  1. Apri MotoClubApp in **Safari**.
  2. Tocca l'icona **Condividi** (quadrato con freccia verso l'alto).
  3. Seleziona **Aggiungi alla schermata Home** e conferma.
  4. Chiudi Safari e avvia l'app dall'icona creata nella schermata Home.
* **Android (Chrome / Edge):**
  * Apri il menu del browser (`⋮`) e tocca **Installa app** (oppure **Aggiungi a schermata Home**).
* **Desktop (Chrome / Edge):**
  * Clicca sull'icona di installazione nella barra degli indirizzi del browser per aprire MotoClubApp come applicazione desktop dedicata.

---

## 4. Accesso, Registrazione e Sicurezza Account

### Modalità Ospite vs Autenticazione
All'apertura dell'app, se non hai ancora effettuato l'accesso, puoi chiudere la finestra di benvenuto per esplorare l'app come **Ospite** in sola lettura, oppure accedere subito.

### Registrazione e Verifica Email
1. Apri **Accedi / Registrati** e seleziona la scheda di registrazione.
2. Inserisci **Email**, **Password** e conferma la password.
3. Dopo l'invio riceverai un'email con il link di conferma: cliccalo per verificare l'account e accedere alle funzionalità complete.

### Login e Password Dimenticata
* Nel modulo di accesso puoi usare l'icona **occhio** accanto al campo password per **mostrare o nascondere** la password digitata.
* Se non ricordi la password (o se sei stato **pre-inserito direttamente da un Club** e devi impostare la tua prima password), usa **Password dimenticata** per ricevere via email il link di ripristino.

---

## 5. Area Personale: Profilo, Notifiche Push e Garage Digitale

Apri il **Menu Destro → Profilo Rider** (oppure tocca il banner **Completa il tuo profilo** nella `Home`) per gestire tutte le tue informazioni personali.

### 5.1 Profilo Pubblico e Vetrina
* **Nome visualizzato & Avatar:** mostrati agli altri rider nei partecipanti agli eventi, negli itinerari e nelle recensioni.
* **Vetrina Pubblica:** Bio, Link Social, Sito Web e **Provincia Operativa** (usata per calcolare le distanze approssimative quando il GPS non è attivo).
* **Richiesta Qualifica Ambassador:** se crei contenuti mototuristici puoi inviare la richiesta di verifica Ambassador (stato *In attesa* fino alla valutazione del SuperAdmin).

### 5.2 Dati Privati & Sicurezza (PII)
Questi dati sono strettamente privati: sono visibili solo a te e, limitatamente alle esigenze di tesseramento e sicurezza nei raduni, ai **Coordinatori** dei Club a cui sei iscritto.

* **Dati Anagrafici Obbligatori per i Club:** Nome, Cognome, Codice Fiscale, Data e Luogo di nascita.
  > **Importante:** Finché questi dati non sono compilati, l'app ti impedisce di inviare richieste di iscrizione ai Club. Una volta diventato socio attivo o in attesa, i campi anagrafici vengono bloccati per garantire l'integrità del registro soci.
* **Sicurezza e Logistica:** Telefono, **Livello di esperienza** (`Rookie`, `Rider`, `Master`, `Wild`), **Contatto di Emergenza (ICE)** (nome e telefono), **Intolleranze / Allergie alimentari**.
* **Preferenze:**
  * **Club Predefinito:** scegli se avviare l'app in modalità *Free Rider* o direttamente in uno dei tuoi Club.
  * **Posizione Base (Home Location):** località di partenza predefinita usata come riferimento per il calcolo delle distanze se non usi il GPS.

### 5.3 Indicatori di Completezza (`Da completare`)
Se mancano campi del Profilo Pubblico, dei Dati Privati o se le **Notifiche Push** risultano disattivate/bloccate, l'app mostra:
* un pallino giallo sull'icona utente nella **TopBar**;
* il badge **`Da completare`** accanto a `Profilo Rider` nel Menu Destro;
* un riepilogo nella **Home** con pulsanti rapidi per raggiungere direttamente la sezione da completare.

### 5.4 Notifiche Push Web e Centro Notifiche
Nella sezione **Notifiche Push Web** del Profilo puoi:
1. Toccare **Attiva Notifiche Push** e concedere il permesso al browser (su iOS è necessario aver prima installato l'app nella schermata Home).
2. Scegliere quali categorie ricevere come notifica push sul dispositivo:
   * *Avvisi Urgenti del Club*
   * *Comunicazioni Ordinarie del Club*
   * *Messaggi Personali (Urgenti / Standard)*
   * *Promemoria Eventi*
   * *Stato Iscrizione & Tessera*
   * *Merchandising Disponibile*

Tutte le notifiche restano comunque sempre consultabili nel **Centro Notifiche** (**Menu Destro → Notifiche**), dove puoi filtrare tra *Tutte* e *Non lette*, segnarle come lette o aprire direttamente l'evento/sezione collegata. Le notifiche hanno una scadenza automatica configurata al momento dell'invio.

### 5.5 Garage Digitale
Accessibile da **Menu Destro → Garage Digitale**:
* Aggiungi una o più moto indicando **Marca** (scelta dall'elenco ufficiale o inserendo `"Altro"`), **Modello** e **Anno**.
* Puoi modificare o eliminare i veicoli in qualsiasi momento.
* Quando ti iscrivi a un evento, potrai selezionare con quale moto del tuo Garage parteciperai (scelta obbligatoria negli eventi `Solo Marca`).

---

## 6. Home, Geolocalizzazione e Navigazione Mappe

### Cosa trovi nella Home
* **Stato Completamento:** promemoria rapido per Profilo Pubblico, Dati Privati e Notifiche Push.
* **Prossimi Eventi & Itinerari Consigliati:** accesso rapido alle attività rilevanti per il contesto attivo.
* **Classifiche Community:** evidenza dei **Club più seguiti**, degli **Ambassador più seguiti** e del badge **Ambassador del Mese**.

### Gestione Posizione (GPS) e Distanze
Per rispettare la privacy e le policy dei browser (in particolare su iOS/Safari), l'app **non attiva richieste GPS ripetitive in background**:
* Tocca il pulsante **Usa la mia posizione** (o **Aggiorna GPS**) presente nelle viste di elenco per rilevare la posizione corrente su tua azione esplicita.
* Se non concedi il GPS (o se il permesso è negato), l'app calcola comunque le distanze approssimative usando in fallback la tua **Provincia Operativa** o la **Home Location** (o la sede del Club per i teaser dei Follower).
* Se il permesso risulta bloccato (`Posizione bloccata`), riabilitalo dalle impostazioni del browser o di iOS per tornare a usare il GPS.

### Apertura in App Mappe (`Apri in Mappe`)
Nelle schede di dettaglio di Eventi, Itinerari e Club, il pulsante **Apri in Mappe** apre automaticamente l'app di navigazione più adatta al tuo dispositivo:
* **iPhone / iPad (iOS/iPadOS):** apre **Apple Maps** tramite link universale (`maps.apple.com`).
* **Android:** apre il selettore app mappe nativo (`geo:`).
* **Desktop:** apre **Google Maps** nel browser.

---

## 7. Itinerari e Repository GPX

Nella scheda **Itinerari** puoi esplorare, scaricare e pubblicare percorsi motociclistici.

### Schede e Filtri
* **Club** *(in Modalità Club)*: itinerari condivisi dal tuo Club.
* **Pubblici:** catalogo globale accessibile a tutta la community.
* **Privati:** i tuoi percorsi personali visibili solo a te.
* **I miei:** tutti gli itinerari creati da te.

Ogni itinerario mostra un badge di difficoltà standardizzato:
* **Rookie (Turistico):** percorsi scorrevoli sotto i 150–200 km.
* **Rider (Dinamico):** medie distanze (200–350 km) e ritmo fluido.
* **Master (Iron Butt):** oltre 350–400 km, tornanti impegnativi o molte ore in sella.
* **Wild (Off-Road):** sterrati, polvere e ghiaia per Enduro e Scrambler.

### Creare o Modificare un Itinerario
1. Tocca il pulsante **Crea** (`+`) nella scheda Itinerari (se sei autenticato).
2. Compila **Titolo**, **Sommario**, **Descrizione** (supporta formattazione Markdown), **Punto di partenza** (con autocompilazione geografica), **Distanza (km)**, **Difficoltà** e **Visibilità** (`Privato`, `Club`, `Pubblico` o `Premium` per gli Ambassador).
3. Carica il file **`.gpx`**, una **Foto** o **Mappa di copertina**, e opzionalmente un **Link Esterno** (es. pagina originale del percorso su sito web o blog).

### Dettaglio Itinerario: Azioni Disponibili
* **Scarica GPX:** scarica in sicurezza il file `.gpx` per importarlo in OsmAnd+, Garmin, TomTom o altri navigatori (richiede account autenticato).
* **Apri in Mappe:** avvia la navigazione verso il punto di partenza.
* **Apri Sito Originale:** apre l'eventuale sito web esterno collegato all'itinerario.
* **Usa per il mio Club (Clonazione / Fork):** se sei Coordinatore di un Club, puoi clonare un itinerario pubblico all'interno del tuo Club per personalizzarlo mantenendo l'attribuzione all'autore originale.
* **Crea Evento da Itinerario:** genera direttamente un nuovo evento pre-collegato a questa traccia.
* **Valutazioni e Recensioni:** assegna un voto a stelle, indica la difficoltà percepita reale e lascia un commento dopo aver percorso la traccia.
* **Condividi:** copia o condividi il link diretto all'itinerario.

---

## 8. Eventi, Iscrizioni (RSVP) e Check-in

Nella scheda **Eventi** trovi le uscite ufficiali dei Club e gli eventi aperti.

### Livelli di Visibilità degli Eventi
* **Pubblico:** visibile a tutti (inclusi Ospiti e Free Rider).
* **Solo Soci (`Members_Only`):** completo solo per i Soci attivi del Club; i **Follower** vedono comunque un **Teaser** (titolo, data e distanza dalla sede del Club) per invogliarli a iscriversi.
* **Solo Marca (`Brand_Only`):** riservato a chi seleziona nel proprio Garage una moto compatibile con la marca richiesta.
* **Solo Coordinatori (`Coordinators_Only`):** eventi organizzativi visibili esclusivamente ai Coordinatori del Club.

### Iscriversi a un Evento (RSVP)
1. Apri il dettaglio dell'evento e tocca **Partecipa / Gestisci RSVP**.
2. Scegli lo stato: **Confermato**, **Forse** o **Ritirato**.
3. Seleziona la **Moto dal tuo Garage** (obbligatoria per eventi *Solo Marca*), indica se porti un **Passeggero**, se partecipi a **Pranzo** / **Pernottamento** (se previsti) e aggiungi eventuali note.
4. **Avviso Difficoltà:** se il livello dell'evento è superiore al livello di esperienza impostato nel tuo Profilo Privato, l'app ti mostrerà un avviso di prudenza prima di confermare.
5. **Lista d'Attesa (Waitlist):** se l'evento ha raggiunto il numero massimo di partecipanti, verrai inserito in lista d'attesa. Se un iscritto confermato si ritira, il sistema promuove automaticamente il primo in lista in ordine cronologico (FIFO).
6. **Aggiungi al Calendario:** dal dettaglio puoi esportare l'appuntamento nel calendario del tuo dispositivo.

### Gestione Evento e Check-in al Ritrovo (Coordinatori)
Chi organizza l'evento (o i Coordinatori per gli eventi ufficiali del Club) può:
* Aggiornare rapidamente lo stato dell'evento: **Bozza → Aperto → In Corso → Completato**.
* Quando l'evento è **Aperto**, consultare il **Riepilogo Logistico** (totale confermati, check-in effettuati, moto, passeggeri, pranzi, pernotti).
* Filtrare i partecipanti (*Confermati*, *Check-in mancante*, *Check-in effettuato*).
* Toccare **Check-in** all'arrivo di ogni rider al punto di ritrovo.
* Usare i pulsanti di **chiamata rapida** al partecipante (o al suo contatto ICE) se qualcuno è in ritardo al ritrovo.
* Segnare come **Consegnati** gli eventuali ordini merchandising del socio direttamente durante il check-in.

---

## 9. Club, Cambio Contesto e Tessera Digitale

### Scoprire, Seguire o Iscriversi a un Club
Nella scheda **Club** puoi sfogliare i Moto Club attivi, filtrarli e aprire la scheda di ciascuno:
* **Segui il Club (`Follower`):** se il Club accetta Follower, puoi seguirlo con un clic per ricevere notizie e vedere i teaser degli eventi riservati.
* **Richiedi Iscrizione (`Member`):** invia una richiesta ufficiale di adesione. Richiede che i tuoi **Dati Privati** (anagrafica e codice fiscale) siano compilati. Finché il Coordinatore non approva, lo stato resterà **In attesa** (puoi annullare la richiesta in qualsiasi momento).
* **Richiedi Nuovo Club:** dalla scheda `Club`, tocca **Richiedi Creazione Club** per proporre la registrazione di un nuovo Moto Club.
  * **Prerequisito:** devi aver prima compilato i **Dati Privati** anagrafici (Nome, Cognome, Codice Fiscale, Data e Luogo di nascita) nel Profilo Rider.
  * **Campi del modulo:**
    * **Nome Club** *(obbligatorio)*: denominazione ufficiale del Moto Club.
    * **Sottotitolo / Motto** *(opzionale)*: breve motto o sezione territoriale.
    * **Sede Fisica / Indirizzo del Club** *(opzionale, consigliato)*: indirizzo o città con autocompilazione geografica (latitudine/longitudine) usata per il calcolo delle distanze e la navigazione.
    * **Manifesto, Bio e Regolamento del Club** *(opzionale)*: descrizione di attività, regole e spirito del club.
    * **Colore di Riferimento del Club** *(opzionale, default `#eab308`)*: colore tema dell'interfaccia in Modalità Club.
    * **Stemma o Logo del Club** *(opzionale)*: immagine del logo del club.
    * **Club visibile nella directory pubblica** *(attivo di default)*: rende il club ricercabile pubblicamente.
    * **Consenti ai rider non iscritti di seguire il club** *(disattivo di default)*: abilita la Modalità Follower e i teaser di eventi/itinerari.
  * **Esito:** vieni registrato come **Coordinatore** in attesa di approvazione del **SuperAdmin**; dopo l'attivazione potrai impostare anche sito web, quota associativa e tolleranza rinnovi in `Gestione Profilo Club`.
* **Condivisione Club:** ogni Club dispone di un link diretto (`/app/clubs/:clubId`) e di un **QR Code** scansionabile per facilitare l'ingresso di nuovi soci.

### Passare tra Modalità Free Rider e Modalità Club
Apri il **Menu Sinistro (`Contesto Operativo`)**:
* Tocca **Usa come Free Rider** per navigare senza contesto di Club.
* Tocca il nome del tuo Club (o uno dei Club in `I Miei Club`) per attivare la **Modalità Club**, applicando il tema grafico del Club e sbloccando eventi, itinerari, tessera e merchandising interni.

### La Mia Tessera Digitale
In Modalità Club, apri **Menu Sinistro → La mia tessera**:
* Mostra nome socio, **N. Socio**, carica/mansione, anno di validità e stato effettivo (`Attivo`, `In tolleranza`, `Scaduto`, `In attesa`, `Sospeso`).
* Se sei **Attivo** o **In tolleranza**, viene generato un **QR Code temporaneo di verifica** valido **60 minuti** (rigenerabile con **Rigenera QR**).
* Chiunque scansioni il QR Code apre la pagina pubblica di verifica (`/verify/:tokenId`), che conferma in tempo reale la validità della tessera senza richiedere login e senza esporre dati sensibili.

---

## 10. Strumenti per Coordinatori del Club

In Modalità Club, i Coordinatori trovano la sezione **Coordinamento Club** nel **Menu Sinistro**.

### 10.1 Approvazione Richieste e Membri
* **Richieste in attesa:** approva o rifiuta le richieste di iscrizione; all'approvazione viene assegnato progressivamente il numero tessera.
* **Gestione Anagrafica e Rinnovi:** modifica ruolo/carica, aggiorna lo stato e registra la data di rinnovo annuale. Consulta in sola lettura i dati privati di sicurezza (telefono, ICE, allergie, codice fiscale) dei soci del tuo Club.
* **Inserimento Diretto Singolo (`Aggiungi Socio`):** inserisci direttamente un socio tramite email (e dati opzionali). Se l'utente è nuovo, riceverà un invito email per attivare l'account e impostare la password.
* **Importazione Massiva (`Importa Soci`):** scarica il modello `.xlsx` o `.csv`, oppure incolla i dati direttamente nella modale, verifica l'anteprima con validazione automatica degli errori e importa l'intero elenco soci in blocco.
* **Stato Verifica & Reinvio Invito:** filtra i soci non ancora verificati (`Non verificato`) e reinvia l'email di attivazione con un clic.
* **Esportazione CSV:** esporta l'elenco completo dei soci del Club in formato `.csv`.

### 10.2 Gestione Profilo Club
Configura nome, descrizione, logo, colore tema, sede, provincia operativa, sito web, **quota associativa annuale**, **data/periodo di tolleranza per i rinnovi** (grace cutoff) e l'opzione per accettare **Follower**.

### 10.3 Avviso ai Soci del Club (Broadcast)
Invia una comunicazione diretta a tutti i soci ufficiali **Attivi** e **In tolleranza** del Club (i Follower sono esclusi):
1. Scegli la priorità: **Avviso Normale** oppure **Avviso Urgente** (alta priorità push per cambi ritrovo, meteo o emergenze).
2. Inserisci **Titolo**, **Messaggio**, un eventuale **collegamento rapido a un Evento attivo** (o deep link `/app/...`) e la **Scadenza automatica** (7 giorni, 30 giorni o data personalizzata).

---

## 11. Merchandising del Club

* **Per i Soci (`Menu Sinistro → Merchandising`):** sfoglia il catalogo del Club attivo, scegli taglia o variante, compila eventuali campi personalizzabili (es. nickname su felpa/maglia) e invia la prenotazione. *(Non sono previsti pagamenti online in app: il saldo e il ritiro avvengono secondo le regole del Club).*
* **Storico Personale (`Menu Destro → I miei ordini merchandising`):** controlla in qualsiasi momento lo stato di tutti i tuoi ordini, anche tra Club diversi.
* **Per i Coordinatori (`Menu Sinistro → Gestione Ordini Merchandising`):** gestisci il catalogo articoli, monitora tutti gli ordini ricevuti, aggiorna gli stati (anche in modo massivo) ed esporta il riepilogo in formato **`.xlsx`**. Gli ordini pronti possono essere consegnati e marcati come *Consegnati* anche durante il check-in di un evento.

---

## 12. Ambassador, Bundle e Itinerari Premium

* **Directory Ambassador (`Menu Sinistro → Ambassador`):** esplora l'elenco degli Ambassador verificati e scopri l'**Ambassador del Mese**.
* **Vetrina Ambassador:** visualizza bio, link esterni, contatori Follower/Supporter, itinerari pubblici e l'anteprima degli itinerari **Premium** e dei **Bundle** disponibili. Tocca **Segui** per diventare Follower dell'Ambassador.
* **Itinerari Premium:** mostrano a tutti un *teaser* con le informazioni essenziali, mentre la traccia GPX completa e i dettagli tecnici sono riservati ai rider autorizzati dall'Ambassador (tramite un Bundle o autorizzazione diretta). Chi è autorizzato riceve il badge **Supporter** nelle proprie recensioni.
* **Pannello Bundle & Follower (`Menu Sinistro → Pannello Bundle & Follower`):** riservato agli Ambassador approvati per creare Bundle tematici di itinerari Premium e gestire le autorizzazioni permanenti dei propri Follower.

---

## 13. Console SuperAdmin (`/superadmin`)

Gli amministratori di piattaforma accedono separatamente all'indirizzo **`/superadmin`** utilizzando le credenziali SuperUser di PocketBase. La console offre:
* **Telemetria e Monitoraggio:** totali utenti, crescita ultimi 30 giorni/mensile, stato dei Club, degli itinerari e delle iscrizioni.
* **Code di Approvazione:** attivazione/sospensione dei nuovi **Club**, approvazione delle richieste **Ambassador** e assegnazione del flag **Ambassador del Mese**.
* **Vocabolario Marche:** gestione dell'elenco globale delle marche motociclistiche disponibili nel Garage Digitale.
