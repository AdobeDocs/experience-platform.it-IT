---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Domande frequenti sul servizio Privacy
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 64cb2de507921fcb4aaade67132024a3fc0d3dee

---


# Domande frequenti sul servizio Privacy

Questo documento contiene le risposte alle domande frequenti sul servizio per la privacy di Adobe Experience Platform.

Il servizio Privacy fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutare le aziende a gestire le richieste di privacy dei dati dei clienti. Con il servizio Privacy puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali, facilitando la conformità automatica alle normative aziendali e legali sulla privacy.

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


## Posso usare il servizio Privacy per pulire i dati inviati accidentalmente a Platform?

Adobe non supporta l&#39;utilizzo del servizio Privacy per cancellare i dati inviati accidentalmente a un prodotto. Il Servizio Privacy è progettato per aiutarti a soddisfare i tuoi obblighi in materia di richieste di accesso o di eliminazione di soggetti o consumatori. Queste richieste sono sensibili al tempo e sono completate in relazione alla normativa sulla privacy applicabile. L&#39;invio di richieste che non siano oggetto/consumatore di dati o che non siano richieste di cancellazione ha effetto su tutti i clienti del servizio Privacy e sulla capacità del servizio Privacy di supportare le relative tempistiche legali.

Contatta il tuo account manager (CDM) per coordinare e fornire un livello di impegno per rimuovere eventuali problemi PII o di dati.

## Come posso ottenere informazioni sullo stato della mia richiesta di privacy o del mio lavoro?

Potete recuperare i dettagli su un particolare processo utilizzando l&#39;API del servizio Privacy o l&#39;interfaccia utente.

### Utilizzo dell&#39;API

Per recuperare lo stato di un particolare processo utilizzando l’API del servizio Privacy, effettuate una richiesta all’endpoint principale (`GET /`), utilizzando l’ID del processo nel percorso della richiesta. Per ulteriori dettagli, vedere la sezione relativa al [controllo dello stato di un processo](api/privacy-jobs.md#check-the-status-of-a-job) nella guida per gli sviluppatori del servizio per la privacy.

### Utilizzo dell’interfaccia

Tutte le richieste di processo attive sono elencate nel widget Richieste **di** processo nel dashboard dell’interfaccia utente del servizio per la privacy. Lo stato di ciascuna richiesta di processo viene visualizzato nella colonna **Stato** . Per ulteriori informazioni sulla visualizzazione delle richieste di lavoro nell’interfaccia utente, consultate la guida [utente del servizio](ui/user-guide.md)per la privacy.

## Come si scaricano i risultati dei processi di privacy completati?

L’API del servizio Privacy e l’interfaccia utente forniscono entrambi metodi per scaricare i risultati dei processi completati in formato ZIP.

### Utilizzo dell&#39;API

Eseguite una richiesta all&#39;endpoint principale (`GET /`) nell&#39;API del servizio Privacy, utilizzando l&#39;ID del processo di cui desiderate scaricare i risultati nel percorso della richiesta. Se lo stato del processo è completo, l&#39;API includerà un `downloadURL` attributo nel corpo della risposta. Questo attributo contiene un URL che potete incollare nella barra degli indirizzi del browser per scaricare il file ZIP.

Per ulteriori dettagli, consultate la sezione sulla [ricerca di un lavoro in base all&#39;ID](api/privacy-jobs.md#check-the-status-of-a-job) nella guida per gli sviluppatori del servizio per la privacy.

### Utilizzo dell’interfaccia

Nel dashboard dell’interfaccia utente del servizio per la privacy, trova il processo che desideri scaricare dal widget Richieste **di** lavoro. Fate clic sull’ID del processo per aprire la pagina Dettagli __ processo. Da qui, fate clic su **Scarica** nell&#39;angolo in alto a destra per scaricare il file ZIP. Per ulteriori informazioni, consulta la guida [utente del servizio](ui/user-guide.md) Privacy.