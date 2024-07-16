---
keywords: Experience Platform;home;argomenti popolari;origini;inserimento;risoluzione dei problemi;risoluzione dei problemi origini;sorgenti faq;faq;source connectors;source connectors;source connectors faqs;source connectors; risoluzione dei problemi;
solution: Experience Platform
title: Risoluzione dei problemi relativi alle origini
description: Questo documento fornisce le risposte alle domande più frequenti sulle origini in Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: 583eb70235174825dd542b95463784638bdef235
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi relativi alle origini

Questo documento fornisce le risposte alle domande più frequenti sulle origini in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi [!DNL Platform], inclusi quelli incontrati in tutte le API [!DNL Platform], fare riferimento alla [guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sulle origini.

### È necessario apportare modifiche alle impostazioni di sicurezza della rete per abilitare le origini?

Inserire nell&#39;elenco Consentiti Per abilitare le sorgenti, potrebbe essere necessario alcuni indirizzi IP. Per ulteriori informazioni, consulta la documentazione sul connettore di origine specifico.

### Quali tipi di autenticazione sono supportati dalle origini?

Le origini possono essere autenticate utilizzando stringhe di connessione, nomi utente e password oppure token e chiavi di accesso. Dettagli specifici sui tipi di autenticazione supportati sono disponibili nella documentazione del connettore di origine specificato.

### Perché tutte le esecuzioni recenti del flusso non riescono?

Se si nota che tutte le esecuzioni recenti del flusso non riescono, è possibile che le credenziali siano state modificate o che siano scadute. Per risolvere il problema, prova ad aggiornare la connessione con le credenziali più recenti.

### Quali tipi di file sono supportati?

Attualmente i tipi di file supportati sono file delimitati, JSON e Parquet.

### Quali sono i vincoli per i nomi e le dimensioni dei file?

Di seguito è riportato un elenco di vincoli che è necessario tenere conto dei file nelle origini.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).
- Il numero massimo di file per batch è 1500, con una dimensione batch massima di 100 GB.
- Il numero massimo di proprietà o campi per riga è 10.000.
- Il numero massimo di batch inviabili per utente al minuto è 2000.

### Quali tipi di dati sono supportati?

I tipi di dati supportati includono numeri interi, stringhe, booleani, oggetti datetime, array e oggetti.

### Quali formati di data e ora sono supportati?

Origini supporta un’ampia varietà di formati datetime durante l’acquisizione dei dati. Ulteriori informazioni sui formati datetime supportati sono disponibili nella sezione date della [guida alla gestione del formato dati](../data-prep/data-handling.md#dates) nella documentazione della preparazione dati.

### Come si formattano gli array in file CSV, JSON e Parquet?

I file JSON e Parquet supportano gli array in modo nativo. Per le strutture piatte, come i CSV, gli array non sono supportati. Tuttavia, le stringhe con valori multipli possono essere suddivise in un array utilizzando funzioni di preparazione dei dati come esplora e unisci. Ulteriori informazioni su queste funzioni di preparazione dati sono disponibili nella [guida delle funzioni di preparazione dati](../data-prep/functions.md#string)

### Quali origini supportano l’acquisizione parziale?

Tutte le origini dell’acquisizione batch supportano l’acquisizione parziale. Tuttavia, le origini di acquisizione in streaming non supportano l’acquisizione parziale.

### Quando dovrei usare l’acquisizione parziale?

L&#39;acquisizione parziale deve essere utilizzata se **non** ha vincoli, ad esempio l&#39;acquisizione dell&#39;intero file in Platform. In alternativa, utilizza l’acquisizione parziale se non ti dispiace acquisire dati che potrebbero contenere errori al suo interno.

### Qual è la soglia tipica per gli errori di acquisizione parziale?

Non esiste una &quot;soglia di errore tipica&quot; per l’acquisizione parziale. Al contrario, questo valore può variare da un caso d’uso all’altro. Per impostazione predefinita, la soglia di errore è impostata al 5%.

### Quanto tempo ci vuole per aggiornare lo stato di esecuzione di un flusso dopo la creazione di un nuovo flusso di dati?

Le esecuzioni del flusso non vengono generate istantaneamente e l&#39;aggiornamento può richiedere da due a tre minuti dopo l&#39;indicazione `startTime`. Il controllo dello stato di un&#39;esecuzione del flusso, immediatamente dopo la creazione di un nuovo flusso di dati, non restituisce informazioni sull&#39;esecuzione del flusso `lastRunDetails`, in quanto non si è ancora verificata. Si consiglia di generare il flusso di dati per alcuni minuti prima di controllare lo stato dell’esecuzione del flusso.