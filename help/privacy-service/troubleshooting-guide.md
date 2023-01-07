---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Privacy Service
description: Questo documento fornisce le risposte alle domande frequenti su Privacy Service e informazioni sugli errori più comuni nell’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# [!DNL Privacy Service] guida alla risoluzione dei problemi

Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutare le aziende a gestire le richieste di privacy dei dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati di clienti privati o personali, facilitando la conformità automatica alle normative aziendali e legali sulla privacy.

Questo documento fornisce le risposte alle domande frequenti sulle [!DNL Privacy Service], nonché informazioni sugli errori più comuni riscontrati nell’API.

## Quando esegui le richieste di privacy nell’API, qual è la differenza tra un utente e un ID utente? {#user-ids}

Per eseguire un nuovo lavoro sulla privacy nell’API, il payload JSON della richiesta deve contenere un `users` array in cui sono elencate informazioni specifiche per ogni utente a cui si applica la richiesta di privacy. Ogni elemento nel `users` array è un oggetto che rappresenta un utente specifico, identificato dal relativo `key` valore.

A sua volta, ogni oggetto utente (o `key`) contiene il proprio `userIDs` array. Questa matrice elenca valori ID specifici **per quel particolare utente**.

Prendi in considerazione l’esempio seguente `users` array:

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

La matrice contiene due oggetti, che rappresentano i singoli utenti identificati dai rispettivi `key` valori (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; ha un solo ID elencato (il loro indirizzo e-mail), mentre &quot;user12345&quot; ne ha due (il loro indirizzo e-mail ed ECID).

Per ulteriori informazioni sulla fornitura di informazioni sull’identità dell’utente, consulta la guida su [dati di identità per le richieste di privacy](identity-data.md).


## Posso usare [!DNL Privacy Service] per pulire i dati che sono stati accidentalmente inviati a [!DNL Platform]?

Adobe non supporta l&#39;utilizzo di [!DNL Privacy Service] per la cancellazione dei dati accidentalmente inviati a un prodotto. [!DNL Privacy Service] è progettato per aiutarti a rispettare gli obblighi relativi alle richieste di accesso o cancellazione della persona interessata (o del consumatore). Queste richieste sono soggette a scadenza e sono completate in relazione alla normativa sulla privacy applicabile. L’invio di richieste che non sono richieste di accesso o di cancellazione dell’interessato/consumatore ha effetto su tutte le [!DNL Privacy Service] e la capacità [!DNL Privacy Service] sostenere le scadenze giuridiche appropriate.

Contatta il tuo account manager (CDM) per coordinarti e sforzarti di rimuovere eventuali PII o problemi di dati.

## Come posso ottenere informazioni sullo stato della mia richiesta di privacy o del mio lavoro?

Puoi recuperare i dettagli su un particolare processo utilizzando la [!DNL Privacy Service] API o interfaccia utente.

### Mediante l’API

Per recuperare lo stato di un particolare processo utilizzando [!DNL Privacy Service] API, effettua una richiesta alla radice (`GET /`), utilizzando l’ID del processo nel percorso della richiesta. Per ulteriori dettagli, consulta la sezione su [controllo dello stato di un processo](api/privacy-jobs.md#check-the-status-of-a-job) in [!DNL Privacy Service] Guida all’API.

### Utilizzo dell’interfaccia

Tutte le richieste di lavoro attive sono elencate nella **[!UICONTROL Richieste di lavoro]** widget sul [!DNL Privacy Service] Dashboard dell&#39;interfaccia utente. Lo stato di ogni richiesta di lavoro viene visualizzato nella sezione **[!UICONTROL Stato]** colonna. Per ulteriori informazioni sulla visualizzazione delle richieste di lavoro nell’interfaccia utente, consulta la [Guida utente di Privacy Service](ui/user-guide.md).

## Come faccio a scaricare i risultati dei miei lavori sulla privacy completati?

La [!DNL Privacy Service] API e interfaccia utente forniscono entrambi i metodi per scaricare i risultati dei processi completati in formato ZIP.

### Mediante l’API

Invia una richiesta alla radice (`GET /`) nel [!DNL Privacy Service] API, utilizzando l’ID del processo di cui desideri scaricare i risultati nel percorso della richiesta. Se lo stato del processo è completo, l’API includerà un `downloadURL` nel corpo della risposta. Questo attributo contiene un URL che puoi incollare nella barra degli indirizzi del tuo browser per scaricare il file ZIP.

Per ulteriori dettagli, consulta la sezione su [ricerca di un processo in base al relativo ID](api/privacy-jobs.md#check-the-status-of-a-job) in [!DNL Privacy Service] Guida all’API.

### Utilizzo dell’interfaccia

Sulla [!DNL Privacy Service] Dashboard dell&#39;interfaccia utente, trova il processo da scaricare dal **Richieste di lavoro** widget. Seleziona l’ID del processo per aprire la pagina Dettagli processo . Da qui, seleziona **Scarica** nell’angolo in alto a destra per scaricare il file ZIP. Consulta la sezione [Guida utente di Privacy Service](ui/user-guide.md) per passaggi più dettagliati.

## Messaggi di errore comuni

La tabella seguente illustra alcuni errori comuni in [!DNL Privacy Service], con descrizioni che aiutano a risolvere i rispettivi problemi.

| Messaggio di errore | Descrizione |
| --- | --- |
| ID utente non trovati. | Impossibile trovare alcuni degli ID utente forniti nella richiesta e sono stati ignorati. Verifica di usare i namespace e i valori ID corretti nel payload della richiesta. Visualizza il documento in [fornitura di dati di identità](./identity-data.md) per una spiegazione più dettagliata. |
| Spazio dei nomi non valido | Spazio dei nomi di identità specificato per un ID utente non valido. Vedi la sezione su [spazi dei nomi delle identità standard](./api/appendix.md#standard-namespaces) in [!DNL Privacy Service] Appendice della guida API per un elenco di namespace accettati. Se utilizzi uno spazio dei nomi personalizzato, assicurati di impostare l’ID come `type` su &quot;custom&quot;. |
| Completato parzialmente | Il processo è stato completato correttamente, ma alcuni dati non erano applicabili per la richiesta specificata ed è stato ignorato. |
| I dati non sono nel formato richiesto. | Formattazione errata di uno o più valori di dati per l&#39;applicazione specificata. Per ulteriori informazioni, consulta i dettagli del processo . |
| Il provisioning dell&#39;organizzazione IMS non è stato eseguito. | Questo messaggio si verifica quando non è stato eseguito il provisioning dell’organizzazione IMS per [!DNL Privacy Service]. Per ulteriori informazioni, contatta l’amministratore. |
| Sono necessari accesso e autorizzazioni. | Per poter utilizzare [!DNL Privacy Service]. Contatta il tuo amministratore per accedere. |
| Si è verificato un problema durante il caricamento e l&#39;archiviazione dei dati di accesso. | Quando si verifica questo errore, ricarica i dati di accesso e riprova. |
| Il carico di lavoro è stato superato per il limite di tasso documento corrente. | Quando si verifica questo errore, ridurre il tasso di invio e riprovare. |
