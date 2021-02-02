---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Guida alla risoluzione dei problemi Privacy Service
topic: troubleshooting
description: Questo documento contiene le risposte alle domande frequenti sui Privacy Service e informazioni sugli errori riscontrati più comunemente nell'API.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# [!DNL Privacy Service] guida alla risoluzione dei problemi

Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutare le aziende a gestire le richieste di privacy dei dati dei clienti. Con [!DNL Privacy Service] puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali, facilitando la conformità automatica alle normative aziendali e legali sulla privacy.

Questo documento contiene le risposte alle domande frequenti su [!DNL Privacy Service], nonché informazioni sugli errori più comuni riscontrati nell&#39;API.

## Quando si effettuano richieste di privacy nell&#39;API, qual è la differenza tra un utente e un ID utente? {#user-ids}

Per eseguire un nuovo processo di privacy nell&#39;API, il payload JSON della richiesta deve contenere un array `users` che elenca informazioni specifiche per ogni utente a cui si applica la richiesta di privacy. Ogni elemento nell&#39;array `users` è un oggetto che rappresenta un utente particolare, identificato dal relativo valore `key`.

A sua volta, ogni oggetto utente (o `key`) contiene la propria matrice `userIDs`. In questa matrice sono elencati i valori ID specifici **di un particolare utente**.

Considerare l&#39;esempio seguente `users` array:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

L&#39;array contiene due oggetti, che rappresentano i singoli utenti identificati dai rispettivi valori `key` (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; ha un solo ID elencato (il loro indirizzo e-mail), mentre &quot;user12345&quot; ne ha due (il loro indirizzo e-mail ed ECID).

Per ulteriori informazioni sulla fornitura di informazioni sull&#39;identità dell&#39;utente, consultare la guida relativa ai [dati di identità per le richieste di privacy](identity-data.md).


## È possibile utilizzare [!DNL Privacy Service] per pulire i dati inviati accidentalmente a [!DNL Platform]?

 Adobe non supporta l&#39;utilizzo di [!DNL Privacy Service] per cancellare i dati inviati accidentalmente a un prodotto. [!DNL Privacy Service] è progettato per aiutarti a soddisfare i tuoi obblighi per le richieste di accesso o di eliminazione dell&#39;oggetto dati (o del consumatore). Queste richieste sono sensibili al tempo e sono completate in relazione alla normativa sulla privacy applicabile. L&#39;invio di richieste che non sono oggetto di dati/richieste di accesso o eliminazione da parte del consumatore ha un impatto su tutti i clienti [!DNL Privacy Service] e sulla capacità di [!DNL Privacy Service] di supportare le scadenze legali appropriate.

Contatta il tuo account manager (CDM) per coordinare e fornire un livello di impegno per rimuovere eventuali problemi PII o di dati.

## Come posso ottenere informazioni sullo stato della mia richiesta di privacy o del mio lavoro?

Potete recuperare i dettagli su un particolare processo utilizzando l&#39;API [!DNL Privacy Service] o l&#39;interfaccia utente.

### Utilizzo dell&#39;API

Per recuperare lo stato di un particolare processo utilizzando l&#39;API [!DNL Privacy Service], effettuate una richiesta all&#39;endpoint principale (`GET /`), utilizzando l&#39;ID del processo nel percorso della richiesta. Per ulteriori dettagli, vedere la sezione relativa al controllo dello stato di un processo [nella [!DNL Privacy Service] guida per gli sviluppatori.](api/privacy-jobs.md#check-the-status-of-a-job)

### Utilizzo dell’interfaccia

Tutte le richieste di processo attive sono elencate nel widget **[!UICONTROL Job Requests]** nel dashboard dell&#39;interfaccia utente [!DNL Privacy Service]. Lo stato di ogni richiesta di processo viene visualizzato nella colonna **[!UICONTROL Status]**. Per ulteriori informazioni sulla visualizzazione delle richieste di lavoro nell&#39;interfaccia utente, consultate la guida utente [Privacy Service](ui/user-guide.md).

## Come si scaricano i risultati dei processi di privacy completati?

L&#39;API [!DNL Privacy Service] e l&#39;interfaccia utente forniscono entrambi metodi per scaricare i risultati dei processi completati in formato ZIP.

### Utilizzo dell&#39;API

Eseguite una richiesta all&#39;endpoint principale (`GET /`) nell&#39;API [!DNL Privacy Service], utilizzando l&#39;ID del processo di cui desiderate scaricare i risultati nel percorso della richiesta. Se lo stato del processo è completo, l&#39;API includerà un attributo `downloadURL` nel corpo della risposta. Questo attributo contiene un URL che potete incollare nella barra degli indirizzi del browser per scaricare il file ZIP.

Per ulteriori dettagli, vedere la sezione relativa alla ricerca di un processo in base all&#39;ID](api/privacy-jobs.md#check-the-status-of-a-job) nella [!DNL Privacy Service] guida per gli sviluppatori.[

### Utilizzo dell’interfaccia

Nel dashboard [!DNL Privacy Service] dell&#39;interfaccia utente, trova il processo che desideri scaricare dal widget **Richieste di lavoro**. Selezionate l’ID del processo per aprire la pagina Dettagli processo. Da qui, selezionare **Scarica** nell&#39;angolo in alto a destra per scaricare il file ZIP. Per ulteriori informazioni, vedere la guida utente [Privacy Service](ui/user-guide.md).

## Messaggi di errore comuni

Nella tabella seguente sono riportati alcuni errori comuni in [!DNL Privacy Service], con descrizioni utili per risolvere i rispettivi problemi.

| Messaggio di errore | Descrizione |
| --- | --- |
| ID utente non trovati. | Non è stato possibile trovare alcuni ID utente forniti nella richiesta e sono stati ignorati. Assicurati di utilizzare i nomi e i valori ID corretti nel payload della richiesta. Per una spiegazione più dettagliata, vedere il documento relativo alla [fornitura di dati di identità](./identity-data.md). |
| Spazio dei nomi non valido | Spazio dei nomi di identità fornito per un ID utente non valido. Per un elenco dei namespace accettati, vedere la sezione relativa agli [spazi dei nomi identità standard](./api/appendix.md#standard-namespaces) nell&#39;appendice della guida per gli sviluppatori [!DNL Privacy Service]. Se utilizzi uno spazio dei nomi personalizzato, accertati di impostare la proprietà `type` dell&#39;ID su &quot;custom&quot;. |
| Completato parzialmente | Il processo è stato completato correttamente, ma alcuni dati non erano applicabili per la richiesta specificata ed è stato ignorato. |
| I dati non sono nel formato richiesto. | Uno o più valori di dati per l&#39;applicazione specificata non sono stati formattati correttamente. Per ulteriori informazioni, consultate i dettagli del processo. |
| Il provisioning dell&#39;organizzazione IMS non è stato effettuato. | Questo messaggio si verifica quando non è stato eseguito il provisioning dell&#39;organizzazione IMS per [!DNL Privacy Service]. Per ulteriori informazioni, contattare l’amministratore. |
| Sono necessari accesso e autorizzazioni. | Per utilizzare [!DNL Privacy Service] sono necessari accesso e autorizzazioni. Contattate l’amministratore per ottenere l’accesso. |
| Si è verificato un problema durante il caricamento e l&#39;archiviazione dei dati di accesso. | Quando si verifica questo errore, caricate nuovamente i dati di accesso e riprovate. |
| Il carico di lavoro è stato superato per il limite di frequenza del documento corrente. | Quando si verifica questo errore, ridurre la frequenza di invio e riprovare. |