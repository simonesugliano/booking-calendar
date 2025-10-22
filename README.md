
# Booking Calendar Automation  
**Aggiornamento automatico del calendario Booking su GitHub Pages tramite GitHub Actions**

---

## Il problema  
Il cliente desiderava mostrare sul proprio sito web **solo le date effettivamente disponibili** siu Booking.com, evitando doppie prenotazioni  
Il widget ufficiale di Booking no era adatto perché:
- incitava a prenotare direttamente su Booking (commissioniper il cliente);
- non permetteva di integrare facilmente la logica delle disponibilità personalizzate;
- richiedeva aggiornamenti manuali o sincronizzazioni omplesse.

Era quindi necessario **un sistema automatico** che potesse:
1. scaricare il file `.ics` di Booking (il calendario delle prenotazioni);
2. elaborarlo e pubblicarlo in un formato leggibile dal sito,;
3. funzionare in modo autonomo e senza server dedicati.

---

## Analisi delle possibili soluzioni  

### 1. Server Node.js con Express + node-ical  
costruire un piccolo backend Node.js che scaricasse e analizzasse l’ICS, restituendo al sito i dati in formato JSON.  
**Vantaggi:** massima flessibilità e pasing in tempo reale.  
**Svantaggi:** necessità di un hosting con Node.js attivo, manutenzione del server e gestione CORS.  

### 2. Script lato client (JavaScript nel sito)  
scaricare direttamente il file ICS via `fetch()` dal browser.  
**Problema:** Booking.com non consente richieste cross-origin (CORS blocked).  

### 3. Automazione su GitHub Actions + GitHub Pages   
Soluzione adottata, dopo analisi si pro e contro generali, perchè è una soluzione completamente *serverless* e sostenibile:
- GitHub Actions scarica automaticamente il file `.ics` da Booking ogni 6 ore.  
- Lo salva nel repository e lo pubblica tramite GitHub Pages.  
- Il sito può quindi leggere il file pubblico aggiornato senza limiti né CORS.

Questa soluzione non richiede nessun server, nessuna manutenzione, ed è completamente trasparente per il cliente.

---

## Come funziona tecnicamente  

1. **Repository GitHub** → contiene il file `booking.ics` e il workflow `.github/workflows/update-ical.yml`.  
2. **GitHub Actions** → esegue uno script `curl` ogni 6 ore per scaricare il file ICS da Booking.  
3. **Commit automatico** → se il file cambia, viene automaticamente versionato e pubblicato.  
4. **GitHub Pages** → serve pubblicamente il file all’indirizzo:  
5. **Il sito del cliente** → legge questo file per mostrare un calendario sincronizzato e sempre aggiornato.

---

## Sicurezza e sostenibilità  

- Nessun dato sensibile viene memorizzato o elaborato.  
- Tutto è gestito su GitHub, infrastruttura sicura e scalabile.  
- Il file `.ics` è pubblico ma non contiene informazioni personali, solo date di prenotazione.  
- L’automazione è completamente grtuita e priva di manutenzione.

---

## Risltato  

Un sistema **completamente automatico**, affidabile e “serverless”, capace di:
- sincronizzare Bookng con il sito web in modo invisibile;
- evitare doppi inserimenti o errori umani;
- ridurre costi e tempi di gestione.

---

## Tecnologie utilizzate  
- **GitHub Actions**  
- **GitHub Pages**  
- **cURL & Bash scripting**  
- **ICS (iCalendarstandard)**  

---

## Stato del progetto  
Test completato con simulazione ICS e notifiche automatiche.  
In attesa del link ICS reale del cliente per l’attivazione definitiva.  

---

---

## Dati sensibili (privata)

L’URL del calendario Booking reale è gestito tramite **GitHub Secrets.**
In questo modo il workflow può aggiornare i dati automaticamente
senza esporre informazioni sensibli nel codice publico.

---

## Riflessioni personali e competenze apprese  

Questo progetto nasce da un’esigenza reale: semplificare la gestione delle disponibilità di n agriturismo,  
mantenendo l’autonomia del cliente e riducendo al minimo la manutenzione tenica.

Durante la realizzazione ho approfondito diversi aspetti pratici e concettuali:

- **Automazione con GitHub Actions:** pianificazione di jobcron, gestione del flusso di commit e deploy automatico.  
- **Integrazione serverless:** comprensione di come GitHub Pages possa fungere da hosting “backendless” per dati inamici.  
- **Gestione file ICS (iCalendar):** standard di sincronizzazione usato da Booking e altri gestionali.  
- **Problem olving tecnico:** analisi di più approcci (backend Node.js, fetch lato client, API proxy) e scelta della soluzione più sostenibile.  
- **Sicurezza e scalabilità:** costruire un sistema che funziona 24/7 senza costi di server, mantenendo pieno controllo dei dati.

Il risultato è un flusso di lavoro completamente automatico e trasparente,  
che combina semplicità, sicurezza e affidabilità: un perfetto esempio di come una buona architettura possa risolvere un problema reale in modo elegante ed efficiente.

---

