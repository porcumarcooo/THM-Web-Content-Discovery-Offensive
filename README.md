# 🌐 Web Content Discovery & Enumeration Methodology

**Piattaforma:** TryHackMe  
**Stanza:** Content Discovery  
**Focus:** Web Enumeration, Directory Brute-Forcing, OSINT, Attacco alla Superficie Esposta  
**Strumenti Utilizzati:** Gobuster, ffuf, Dirb, Wappalyzer, cURL  

---

## 📝 Executive Summary
Questo repository documenta le metodologie offensive utilizzate per mappare la superficie di attacco "invisibile" di un'applicazione web. Durante un Penetration Test, identificare directory amministrative nascoste, file di backup esposti o vecchie versioni di API rappresenta spesso il vettore di ingresso principale per la compromissione totale del target.

---

## 🎯 Metodologia di Enumerazione (Kill Chain)

La scoperta dei contenuti web è stata strutturata in un approccio progressivo, passando dalla ricognizione passiva a quella attiva e rumorosa.

### 1. Ricognizione Passiva (OSINT)
Prima di inviare pacchetti direttamente al target, è fondamentale raccogliere informazioni senza far scattare gli allarmi dei firewall:
* **Google Dorks:** Ricerca di file indicizzati per errore (es. `site:target.com ext:pdf` o `intitle:"index of"`).
* **Wayback Machine:** Estrazione di vecchi endpoint o file JavaScript non più linkati nel sito attuale ma ancora presenti sul server.
* **GitHub Recon:** Ricerca di credenziali hardcoded o repository pubbliche sfuggite al controllo degli sviluppatori.

### 2. Ricognizione Manuale
Ispezione mirata dei file di configurazione standard:
* Analisi di `robots.txt` e `sitemap.xml` per scoprire le directory che l'amministratore ha esplicitamente chiesto ai motori di ricerca di ignorare.
* Analisi degli Header HTTP e del codice sorgente della pagina per estrarre commenti nascosti e versioni dei framework.

### 3. Enumerazione Attiva (Brute-Forcing)
L'utilizzo di dizionari mirati (es. `SecLists`) combinati con strumenti di automazione ad alta velocità per forzare la scoperta di percorsi nascosti.
* **Gobuster / ffuf:** Esecuzione di attacchi a dizionario contro gli URI del server web, filtrando le risposte per codice di stato (es. ignorando i 404 e analizzando i 200 OK o i 301 Redirect).
* **Fuzzing dei Parametri:** Ricerca di parametri GET/POST nascosti che potrebbero essere vulnerabili a LFI (Local File Inclusion) o SQL Injection.

---

## 🧠 Offensive Takeaways
1. **La "Security through Obscurity" fallisce sempre:** Se un pannello di amministrazione non è protetto da autenticazione forte, un attaccante armato di una buona wordlist lo troverà in pochi minuti.
2. **L'importanza dei dizionari:** L'efficacia dell'enumerazione attiva dipende interamente dalla qualità della wordlist utilizzata. Adattare il dizionario al target (es. usare wordlist specifiche per server IIS o per CMS WordPress) è cruciale per il successo dell'attacco.
