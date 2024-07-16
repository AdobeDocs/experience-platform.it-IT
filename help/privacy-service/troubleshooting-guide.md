---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Privacy Service
description: Questo documento fornisce le risposte alle domande frequenti su Privacy Service, nonché informazioni sugli errori più comuni riscontrati nell’API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---

# Guida alla risoluzione dei problemi di [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutare le aziende a gestire le richieste di privacy dei dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso ed eliminazione di dati privati o personali dei clienti, facilitando la conformità automatica alle normative aziendali e legali sulla privacy.

Questo documento fornisce le risposte alle domande frequenti su [!DNL Privacy Service], nonché informazioni sugli errori più comuni riscontrati nell&#39;API.

## Quando si eseguono richieste di accesso a dati personali nell’API, qual è la differenza tra un utente e un ID utente? {#user-ids}

Per poter eseguire un nuovo processo di privacy nell’API, il payload JSON della richiesta deve contenere un array `users` che elenca informazioni specifiche per ogni utente a cui si applica la richiesta di privacy. Ogni elemento nell&#39;array `users` è un oggetto che rappresenta un utente particolare, identificato dal relativo valore `key`.

A sua volta, ogni oggetto utente (o `key`) contiene il proprio array `userIDs`. Questa matrice elenca valori ID specifici **per un utente particolare**.

Considera il seguente array di esempio `users`:

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

L&#39;array contiene due oggetti, che rappresentano i singoli utenti identificati dai rispettivi valori `key` (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; ha un solo ID elencato (il loro indirizzo e-mail), mentre &quot;utente12345&quot; ne ha due (il loro indirizzo e-mail e ECID).

Per ulteriori informazioni su come fornire informazioni sull&#39;identità utente, consulta la guida su [dati di identità per le richieste di privacy](identity-data.md).


## Posso usare [!DNL Privacy Service] per pulire i dati accidentalmente inviati a [!DNL Platform]?

L&#39;Adobe non supporta l&#39;utilizzo di [!DNL Privacy Service] per la cancellazione dei dati inviati accidentalmente a un prodotto. [!DNL Privacy Service] è progettato per aiutarti a rispettare gli obblighi relativi alle richieste di accesso o cancellazione da parte dell&#39;interessato (o del consumatore). Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito.

Le richieste di accesso a dati personali sono soggette a scadenza e vengono completate in base alla normativa sulla privacy applicabile. l&#39;invio di richieste che non sono richieste di accesso o di cancellazione dell&#39;interessato/consumatore influisce su tutti i clienti [!DNL Privacy Service] e sulla capacità di [!DNL Privacy Service] di supportare le tempistiche legali appropriate. È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio.

Contatta il team del tuo account di Adobe per coordinare e rimuovere eventuali problemi di PII o dati.

## Come posso ottenere informazioni sullo stato della mia richiesta di accesso a dati personali o del mio lavoro?

È possibile recuperare i dettagli di un particolare processo utilizzando l&#39;API [!DNL Privacy Service] o l&#39;interfaccia utente.

### Mediante l’API

Per recuperare lo stato di un particolare processo utilizzando l&#39;API [!DNL Privacy Service], effettuare una richiesta all&#39;endpoint radice (`GET /`), utilizzando l&#39;ID del processo nel percorso della richiesta. Per ulteriori dettagli, vedere la sezione relativa alla verifica dello stato di un processo](api/privacy-jobs.md#check-the-status-of-a-job) nella guida dell&#39;API [!DNL Privacy Service].[

### Utilizzo dell’interfaccia utente

Tutte le richieste di processo attive sono elencate nel widget **[!UICONTROL Richieste di processo]** nel dashboard dell&#39;interfaccia utente [!DNL Privacy Service]. Lo stato di ogni richiesta di processo viene visualizzato nella colonna **[!UICONTROL Stato]**. Per ulteriori informazioni sulla visualizzazione delle richieste di processi nell&#39;interfaccia utente, consulta la [guida utente Privacy Service](ui/user-guide.md).

## Come posso scaricare i risultati dei miei processi sulla privacy completati?

L&#39;API [!DNL Privacy Service] e l&#39;interfaccia utente forniscono entrambi i metodi per scaricare i risultati dei processi completati in formato ZIP.

### Mediante l’API

Effettuare una richiesta all&#39;endpoint radice (`GET /`) nell&#39;API [!DNL Privacy Service], utilizzando l&#39;ID del processo di cui si desidera scaricare i risultati nel percorso della richiesta. Se lo stato del processo è completo, l&#39;API includerà un attributo `downloadURL` nel corpo della risposta. Questo attributo contiene un URL che puoi incollare nella barra degli indirizzi del browser per scaricare il file ZIP.

Per ulteriori dettagli, vedere la sezione relativa alla ricerca di un processo in base al relativo ID](api/privacy-jobs.md#check-the-status-of-a-job) nella guida dell&#39;API [!DNL Privacy Service].[

### Utilizzo dell’interfaccia utente

Nel dashboard dell&#39;interfaccia utente [!DNL Privacy Service] trovare il processo che si desidera scaricare dal widget **Richieste di processo**. Selezionare l&#39;ID del job per aprire la pagina Dettagli job. Da qui, seleziona **Scarica** nell&#39;angolo in alto a destra per scaricare il file ZIP. Per i passaggi più dettagliati, consulta la [guida utente di Privacy Service](ui/user-guide.md).

## Messaggi di errore comuni {#common-error-messages}

Nella tabella seguente vengono descritti alcuni errori comuni in [!DNL Privacy Service], con descrizioni che consentono di risolvere i rispettivi problemi.

| Messaggio di errore | Descrizione |
| --- | --- |
| Non sono stati trovati gli ID utente. | Alcuni degli ID utente forniti nella richiesta non sono stati trovati e sono stati ignorati. Assicurati di utilizzare gli spazi dei nomi e i valori ID corretti nel payload della richiesta. Per una spiegazione più dettagliata, consulta il documento su [fornitura dei dati di identità](./identity-data.md). |
| Spazio dei nomi non valido | Uno spazio dei nomi identità fornito per un ID utente non è valido. Per un elenco degli spazi dei nomi accettati, consulta la sezione sugli [spazi dei nomi di identità standard](./api/appendix.md#standard-namespaces) nell&#39;appendice della guida API [!DNL Privacy Service]. Se utilizzi uno spazio dei nomi personalizzato, assicurati di impostare la proprietà `type` dell&#39;ID su &quot;custom&quot;. |
| Parzialmente completato | Il processo è stato completato correttamente, ma alcuni dati non erano applicabili per la richiesta specificata ed è stato saltato. |
| I dati non sono nel formato richiesto. | Uno o più valori di dati per l&#39;applicazione specificata non sono formattati correttamente. Per ulteriori informazioni, consulta i dettagli del processo. |
| Non è stato eseguito il provisioning per l’organizzazione IMS. | Questo messaggio si verifica quando non è stato eseguito il provisioning dell&#39;organizzazione per [!DNL Privacy Service]. Per ulteriori informazioni, contatta l’amministratore. |
| Sono necessari l’accesso e le autorizzazioni. | Per utilizzare [!DNL Privacy Service] sono necessari l&#39;accesso e le autorizzazioni. Contatta l’amministratore per ottenere l’accesso. |
| Si è verificato un problema durante l’upload e l’archiviazione dei dati di accesso. | Quando si verifica questo errore, ricarica i dati di accesso e riprova. |
| Il carico di lavoro è stato superato per il limite di frequenza documenti corrente. | In questo caso, riduci il tasso di invio e riprova. |
| Troppe richieste<br>(errori HTTP 429) | Se i modelli di invio superano il limite monitorato di processi consentiti per l’interessato, verrà visualizzato un errore HTTP 429 in risposta al traffico continuo dall’organizzazione. Privacy Service è destinato al trattamento delle richieste di privacy delle persone interessate. Non deve essere utilizzato per la pulizia dei dati. Se ricevi errori HTTP 429, i limiti di limitazione e di richiesta vengono implementati per proteggere gli Adobi da abusi che potrebbero mettere a rischio il lavoro di conformità legittimo.<br>Metodi alternativi per ridurre al minimo i dati sono forniti da [l&#39;impostazione delle pianificazioni di scadenza dei set di dati](../hygiene/ui/dataset-expiration.md) e l&#39;utilizzo della [funzionalità di eliminazione record](../hygiene/ui/record-delete.md). Per ulteriori informazioni su come applicare queste funzionalità, consulta la relativa documentazione. |
