---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Domande frequenti su Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# [!DNL Privacy Service] guida alla risoluzione dei problemi

 Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutare le aziende a gestire le richieste di privacy dei dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali, facilitando la conformità automatica alle normative aziendali e legali sulla privacy.

Questo documento contiene le risposte alle domande frequenti su [!DNL Privacy Service]di , nonché informazioni sugli errori più comuni riscontrati nell&#39;API.

## Quando si effettuano richieste di privacy nell&#39;API, qual è la differenza tra un utente e un ID utente? {#user-ids}

Per eseguire un nuovo processo di privacy nell&#39;API, il payload JSON della richiesta deve contenere un `users` array che elenca informazioni specifiche per ogni utente a cui si applica la richiesta di privacy. Ciascun elemento dell&#39; `users` array è un oggetto che rappresenta un utente particolare, identificato dal relativo `key` valore.

A sua volta, ogni oggetto utente (o `key`) contiene un proprio `userIDs` array. Questa matrice elenca i valori ID specifici **per quel particolare utente**.

Consider the following example `users` array:

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

L&#39;array contiene due oggetti, che rappresentano i singoli utenti identificati dai rispettivi `key` valori (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; ha un solo ID elencato (il loro indirizzo e-mail), mentre &quot;user12345&quot; ne ha due (il loro indirizzo e-mail ed ECID).

Per ulteriori informazioni sulla fornitura di informazioni sull&#39;identità dell&#39;utente, consultate la guida sui dati di [identità per le richieste](identity-data.md)di privacy.


## Posso usare [!DNL Privacy Service] per pulire i dati a cui sono stati accidentalmente inviati [!DNL Platform]?

Adobe non supporta l&#39;utilizzo [!DNL Privacy Service] per cancellare i dati inviati accidentalmente a un prodotto. [!DNL Privacy Service] è progettato per aiutarti a soddisfare i tuoi obblighi per le richieste di accesso o di eliminazione dell&#39;oggetto dati (o del consumatore). Queste richieste sono sensibili al tempo e sono completate in relazione alla normativa sulla privacy applicabile. L&#39;invio di richieste che non sono oggetto/consumatore di accesso o di eliminazione di richieste ha un impatto su tutti [!DNL Privacy Service] i clienti e sulla capacità di [!DNL Privacy Service] supportare le scadenze legali appropriate.

Contatta il tuo account manager (CDM) per coordinare e fornire un livello di impegno per rimuovere eventuali problemi PII o di dati.

## Come posso ottenere informazioni sullo stato della mia richiesta di privacy o del mio lavoro?

Potete recuperare i dettagli su un particolare processo utilizzando l&#39; [!DNL Privacy Service] API o l&#39;interfaccia utente.

### Utilizzo dell&#39;API

Per recuperare lo stato di un particolare processo utilizzando l&#39; [!DNL Privacy Service] API, effettuate una richiesta all&#39;endpoint principale (`GET /`), utilizzando l&#39;ID del processo nel percorso della richiesta. Per ulteriori dettagli, consultate la sezione relativa alla [verifica dello stato di un processo](api/privacy-jobs.md#check-the-status-of-a-job) nella guida per [!DNL Privacy Service] gli sviluppatori.

### Utilizzo dell’interfaccia

Tutte le richieste di processo attive sono elencate nel **[!UICONTROL Job Requests]** widget nel dashboard dell’ [!DNL Privacy Service] interfaccia utente. Lo stato di ciascuna richiesta di processo viene visualizzato sotto la **[!UICONTROL Status]** colonna. Per ulteriori informazioni sulla visualizzazione delle richieste di lavoro nell’interfaccia utente, consultate la guida [utente di](ui/user-guide.md)Privacy Service.

## Come si scaricano i risultati dei processi di privacy completati?

L&#39; [!DNL Privacy Service] API e l&#39;interfaccia utente forniscono entrambi metodi per scaricare i risultati dei processi completati in formato ZIP.

### Utilizzo dell&#39;API

Eseguite una richiesta all&#39;endpoint principale (`GET /`) nell&#39; [!DNL Privacy Service] API, utilizzando l&#39;ID del processo di cui desiderate scaricare i risultati nel percorso della richiesta. Se lo stato del processo è completo, l&#39;API includerà un `downloadURL` attributo nel corpo della risposta. Questo attributo contiene un URL che potete incollare nella barra degli indirizzi del browser per scaricare il file ZIP.

Per ulteriori dettagli, consultate la sezione sulla [ricerca di un processo in base all’ID](api/privacy-jobs.md#check-the-status-of-a-job) nella guida per [!DNL Privacy Service] gli sviluppatori.

### Utilizzo dell’interfaccia

Nel dashboard [!DNL Privacy Service] dell’interfaccia utente, individuate il processo da scaricare dal widget Richieste **di** processo. Fate clic sull’ID del processo per aprire la pagina Dettagli __ processo. Da qui, fate clic su **Scarica** nell&#39;angolo in alto a destra per scaricare il file ZIP. Per ulteriori informazioni, consultate la guida [utente di](ui/user-guide.md) Privacy Service.

## Messaggi di errore comuni

Nella tabella seguente sono riportati alcuni errori comuni relativi a [!DNL Privacy Service], con descrizioni utili per risolvere i rispettivi problemi.

| Messaggio di errore | Descrizione |
| --- | --- |
| ID utente non trovati. | Non è stato possibile trovare alcuni ID utente forniti nella richiesta e sono stati ignorati. Assicurati di utilizzare i nomi e i valori ID corretti nel payload della richiesta. Per una spiegazione più dettagliata, vedere il documento [che fornisce i dati](./identity-data.md) di identità. |
| Spazio dei nomi non valido | Spazio dei nomi di identità fornito per un ID utente non valido. Per un elenco dei namespace accettati, vedete la sezione relativa agli spazi dei nomi delle identità [standard](./api/appendix.md#standard-namespaces) nell&#39;appendice della guida [!DNL Privacy Service] per gli sviluppatori. Se utilizzi uno spazio dei nomi personalizzato, accertati di impostare la `type` proprietà ID su &quot;custom&quot;. |
| Completato parzialmente | Il processo è stato completato correttamente, ma alcuni dati non erano applicabili per la richiesta specificata ed è stato ignorato. |
| I dati non sono nel formato richiesto. | Uno o più valori di dati per l&#39;applicazione specificata non sono stati formattati correttamente. Per ulteriori informazioni, consultate i dettagli del processo. |
| Il provisioning dell&#39;organizzazione IMS non è stato effettuato. | Questo messaggio si verifica quando non è stato effettuato il provisioning per l&#39;organizzazione IMS [!DNL Privacy Service]. Per ulteriori informazioni, contattare l’amministratore. |
| Sono necessari accesso e autorizzazioni. | Per poter utilizzare sono necessari accesso e autorizzazioni [!DNL Privacy Service]. Contattate l’amministratore per ottenere l’accesso. |
| Si è verificato un problema durante il caricamento e l&#39;archiviazione dei dati di accesso. | Quando si verifica questo errore, caricate nuovamente i dati di accesso e riprovate. |
| Il carico di lavoro è stato superato per il limite di frequenza del documento corrente. | Quando si verifica questo errore, ridurre la frequenza di invio e riprovare. |