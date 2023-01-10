---
keywords: Experience Platform;home;argomenti comuni;origini;acquisizione;risoluzione dei problemi;origini risoluzione dei problemi;domande frequenti;origini;FAQ;connettori sorgente;connettori sorgente;domande frequenti sui connettori sorgente;risoluzione dei problemi dei connettori sorgente;
solution: Experience Platform
title: Risoluzione dei problemi di Origini
description: Questo documento fornisce le risposte alle domande più frequenti sulle origini su Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di Origini

Questo documento fornisce le risposte alle domande più frequenti sulle origini su Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altre [!DNL Platform] servizi, compresi quelli incontrati in tutti [!DNL Platform] API, fai riferimento alla [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande frequenti

Di seguito è riportato un elenco delle risposte alle domande più frequenti sulle fonti.

### È necessario apportare modifiche alle impostazioni di sicurezza della rete per abilitare le fonti?

Per abilitare le origini potrebbe essere necessario inserire nell&#39;elenco Consentiti alcuni indirizzi IP. Per ulteriori informazioni, consulta la documentazione sul connettore di origine specifico.

### Quali tipi di autenticazione sono supportati dalle origini?

Le origini possono essere autenticate utilizzando stringhe di connessione, nomi utente e password o token di accesso e chiavi. Ulteriori dettagli sui tipi di autenticazione supportati sono disponibili nella documentazione del connettore di origine specificato.

### Perché tutte le mie esecuzioni recenti non riescono?

Se noti che tutte le esecuzioni recenti del flusso non riescono, le tue credenziali potrebbero essere cambiate o scadute. Per risolvere il problema, prova ad aggiornare la connessione con le credenziali più recenti.

### Quali tipi di file sono supportati?

Attualmente i tipi di file supportati sono file delimitati, JSON e Parquet.

### Quali sono i vincoli relativi ai nomi e alle dimensioni dei file?

Di seguito è riportato un elenco di vincoli da tenere in considerazione per i file nelle origini.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. Punti di codice come `\uE000`, anche se valido nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti alcuni caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1 vedi [RFC 2616, sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (..) e due caratteri punto (.).
- Il numero massimo di file per batch è 1500, con una dimensione batch massima pari a 100 GB.
- Il numero massimo di proprietà o campi per riga è 10.000.
- Il numero massimo di batch che possono essere inviati per utente, al minuto è 138.

### Quali tipi di dati sono supportati?

I tipi di dati supportati includono numeri interi, stringhe, booleani, oggetti datetime, array e oggetti.

### Quali formati di data e ora sono supportati?

Origini supporta un&#39;ampia varietà di formati di datetime durante l&#39;acquisizione dei dati. Ulteriori informazioni sui formati datetime supportati sono disponibili nella sezione date del [guida alla gestione del formato dati](../data-prep/data-handling.md#dates) nella documentazione Data Prep .

### Come si formattano gli array in file CSV, JSON e Parquet?

I file JSON e Parquet supportano gli array in modo nativo. Per le strutture piatte, come i CSV, gli array non sono supportati. Tuttavia, le stringhe con più valori possono essere suddivise in un array utilizzando funzioni di preparazione dei dati come esplodi e join. Ulteriori informazioni su queste funzioni di preparazione dei dati sono disponibili nella sezione [guida alle funzioni di preparazione dei dati](../data-prep/functions.md#string)

### Quali origini supportano l’acquisizione parziale?

Tutte le origini di acquisizione batch supportano l’acquisizione parziale. Tuttavia, le origini di acquisizione in streaming non supportano l’acquisizione parziale.

### Quando dovrei usare l’acquisizione parziale?

L’acquisizione parziale deve essere utilizzata se **not** presenta vincoli, ad esempio l’acquisizione dell’intero file in Platform. In alternativa, è necessario utilizzare l’acquisizione parziale se non si desidera acquisire dati che potrebbero contenere errori al suo interno.

### Qual è la tipica soglia di errore di acquisizione parziale?

Non esiste una &quot;soglia di errore tipica&quot; per l’acquisizione parziale. Al contrario, questo valore può variare da caso d’uso a caso d’uso. Per impostazione predefinita, la soglia di errore è impostata su 5%.

### Quanto tempo è necessario per l’aggiornamento dello stato di un’esecuzione di flusso dopo la creazione di un nuovo flusso di dati?

Le esecuzioni del flusso non vengono generate istantaneamente e possono richiedere circa due o tre minuti per l’aggiornamento dopo che è stato designato `startTime`. Il controllo dello stato di un&#39;esecuzione di flusso, subito dopo la creazione di un nuovo flusso di dati, non restituisce informazioni sul `lastRunDetails` come non è ancora successo. Si consiglia di consentire la generazione del flusso di dati per alcuni minuti prima di controllare lo stato dell’esecuzione del flusso.