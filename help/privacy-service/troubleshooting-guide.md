---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Privacy Service
description: Questo documento fornisce le risposte alle domande frequenti su Privacy Service, nonché informazioni sugli errori più comuni riscontrati nell’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# [!DNL Privacy Service] guida alla risoluzione dei problemi

Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutare le aziende a gestire le richieste dei clienti sulla privacy dei dati. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati privati o personali dei clienti, facilitando la conformità automatica alle normative aziendali e legali sulla privacy.

Questo documento fornisce le risposte alle domande più frequenti su [!DNL Privacy Service], nonché informazioni sugli errori comunemente riscontrati nell’API.

## Quando si eseguono richieste di accesso a dati personali nell’API, qual è la differenza tra un utente e un ID utente? {#user-ids}

Per eseguire un nuovo processo di privacy nell’API, il payload JSON della richiesta deve contenere `users` array che elenca informazioni specifiche per ogni utente a cui si applica la richiesta di accesso a dati personali. Ogni elemento in `users` array è un oggetto che rappresenta un particolare utente, identificato dal relativo `key` valore.

A sua volta, ogni oggetto utente (o `key`) contiene il proprio `userIDs` array. Questo array elenca valori ID specifici **per quello specifico utente**.

Considera l’esempio seguente `users` array:

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

L’array contiene due oggetti, che rappresentano i singoli utenti identificati dai rispettivi `key` (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; ha un solo ID elencato (il loro indirizzo e-mail), mentre &quot;utente12345&quot; ne ha due (il loro indirizzo e-mail e ECID).

Per ulteriori informazioni su come fornire informazioni sull’identità utente, consulta la guida su [dati di identità per le richieste di privacy](identity-data.md).


## Posso utilizzare [!DNL Privacy Service] per eliminare i dati inviati accidentalmente a [!DNL Platform]?

L’Adobe non supporta l’utilizzo di [!DNL Privacy Service] per cancellare i dati accidentalmente inviati a un prodotto. [!DNL Privacy Service] è progettato per aiutarti a rispettare gli obblighi relativi alle richieste di accesso o cancellazione delle persone interessate (o dei consumatori). Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito.

Le richieste di accesso a dati personali sono soggette a scadenza e vengono completate in base alla normativa sulla privacy applicabile. la presentazione di richieste che non sono richieste di accesso o di cancellazione dell’interessato/consumatore ha un impatto su tutti [!DNL Privacy Service] clienti e la possibilità di [!DNL Privacy Service] sostenere i calendari giuridici appropriati. È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio.

Contatta il team del tuo account di Adobe per coordinare e rimuovere eventuali problemi di PII o dati.

## Come posso ottenere informazioni sullo stato della mia richiesta di accesso a dati personali o del mio lavoro?

È possibile recuperare i dettagli di un particolare processo utilizzando [!DNL Privacy Service] API o interfaccia utente.

### Mediante l’API

Per recuperare lo stato di un particolare processo utilizzando [!DNL Privacy Service] API, invia una richiesta alla directory principale (`GET /`), utilizzando l’ID del processo nel percorso della richiesta. Per ulteriori dettagli, consulta la sezione su [verifica dello stato di un processo](api/privacy-jobs.md#check-the-status-of-a-job) nel [!DNL Privacy Service] Guida API di.

### Utilizzo dell’interfaccia utente

Tutte le richieste di lavoro attive sono elencate in **[!UICONTROL Richieste di lavoro]** widget sul [!DNL Privacy Service] Dashboard dell’interfaccia utente. Lo stato di ciascuna richiesta di processo viene visualizzato nella sezione **[!UICONTROL Stato]** colonna. Per ulteriori informazioni sulla visualizzazione delle richieste di lavoro nell’interfaccia utente, consulta la sezione [Guida utente di Privacy Service](ui/user-guide.md).

## Come posso scaricare i risultati dei miei processi sulla privacy completati?

Il [!DNL Privacy Service] API e interfaccia utente forniscono entrambi metodi per scaricare i risultati dei processi completati in formato ZIP.

### Mediante l’API

Effettua una richiesta alla radice (`GET /`) in [!DNL Privacy Service] API, utilizzando l’ID del processo di cui desideri scaricare i risultati nel percorso della richiesta. Se lo stato del processo è completo, l’API includerà una `downloadURL` nel corpo della risposta. Questo attributo contiene un URL che puoi incollare nella barra degli indirizzi del browser per scaricare il file ZIP.

Per ulteriori dettagli, consulta la sezione su [ricerca di un processo in base al relativo ID](api/privacy-jobs.md#check-the-status-of-a-job) nel [!DNL Privacy Service] Guida API di.

### Utilizzo dell’interfaccia utente

Il giorno [!DNL Privacy Service] nell&#39;interfaccia utente, trova il processo che desideri scaricare da **Richieste di lavoro** widget. Selezionare l&#39;ID del job per aprire la pagina Dettagli job. Da qui, seleziona **Scarica** nell’angolo in alto a destra per scaricare il file ZIP. Consulta la [Guida utente di Privacy Service](ui/user-guide.md) per passaggi più dettagliati.

## Messaggi di errore comuni

La tabella seguente illustra alcuni errori comuni in [!DNL Privacy Service], con descrizioni per aiutarli a risolvere i rispettivi problemi.

| Messaggio di errore | Descrizione |
| --- | --- |
| ID utente non trovati. | Alcuni degli ID utente forniti nella richiesta non sono stati trovati e sono stati ignorati. Assicurati di utilizzare gli spazi dei nomi e i valori ID corretti nel payload della richiesta. Vedi il documento su [fornitura di dati di identità](./identity-data.md) per una spiegazione più dettagliata. |
| Spazio dei nomi non valido | Uno spazio dei nomi identità fornito per un ID utente non è valido. Consulta la sezione su [spazi dei nomi di identità standard](./api/appendix.md#standard-namespaces) nel [!DNL Privacy Service] Appendice della guida API per un elenco degli spazi dei nomi accettati. Se utilizzi uno spazio dei nomi personalizzato, assicurati di impostare l’ID di `type` su &quot;custom&quot;. |
| Parzialmente completato | Il processo è stato completato correttamente, ma alcuni dati non erano applicabili per la richiesta specificata ed è stato saltato. |
| I dati non sono nel formato richiesto. | Uno o più valori di dati per l&#39;applicazione specificata non sono formattati correttamente. Per ulteriori informazioni, consulta i dettagli del processo. |
| Non è stato eseguito il provisioning per l’organizzazione IMS. | Questo messaggio viene visualizzato quando per la tua organizzazione non è stato eseguito il provisioning di [!DNL Privacy Service]. Per ulteriori informazioni, contatta l’amministratore. |
| Sono necessari l’accesso e le autorizzazioni. | Per utilizzare sono necessari l’accesso e le autorizzazioni [!DNL Privacy Service]. Contatta l’amministratore per ottenere l’accesso. |
| Si è verificato un problema durante il caricamento e l’archiviazione dei dati di accesso. | Quando si verifica questo errore, ricarica i dati di accesso e riprova. |
| Il carico di lavoro è stato superato per il limite di frequenza documenti corrente. | In questo caso, riduci il tasso di invio e riprova. |
