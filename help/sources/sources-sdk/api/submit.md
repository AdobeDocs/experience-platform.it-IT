---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Invia la tua origine (Beta)
topic-legacy: overview
description: Il seguente documento fornisce passaggi su come testare e verificare una nuova origine utilizzando l’API del servizio di flusso e integrare una nuova origine tramite l’SDK di Origini.
hide: true
hidefromtoc: true
source-git-commit: 274784a5b82d12497f7437fdeaf665dd64224c2d
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Invia la tua fonte (Beta)

>[!IMPORTANT]
>
>L&#39;SDK di Origini è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità descritta in questa documentazione è soggetta a modifiche.

Il passaggio finale per integrare la nuova origine in Adobe Experience Platform utilizzando [!DNL Sources SDK] per verificare la fonte. Una volta completata la procedura, puoi inviare la nuova origine contattando il rappresentante di Adobe.

Il seguente documento fornisce passaggi su come verificare ed eseguire il debug dell&#39;origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

* Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).
* Per informazioni su come generare le credenziali per le API di Platform, consulta l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md).
* Per informazioni su come impostare [!DNL Postman] per le API di Platform, consulta l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../landing/postman.md).
* Per facilitare il processo di test e debug, scarica il [[!DNL Sources SDK] raccolta e ambiente di verifica qui](../assets/sdk-verification.zip) e segui i passaggi descritti di seguito.

## Verificare la sorgente

Per testare la sorgente, è necessario eseguire la [[!DNL Sources SDK] raccolta e ambiente di verifica](../assets/sdk-verification.zip) su [!DNL Postman] fornendo le variabili di ambiente appropriate relative all’origine.

Per avviare il test, devi prima impostare la raccolta e l’ambiente su [!DNL Postman]. Quindi, specifica l&#39;ID della specifica di connessione da verificare. Questo ID deve essere lo stesso generato con [!DNL Sources SDK].

### Specifica `authSpecName`

Dopo aver immesso l’ID della specifica di connessione, devi quindi specificare la `authSpecName` che si sta utilizzando per la connessione di base. A seconda della scelta, potrebbe essere `OAuth 2 Refresh Code` o  `Basic Authentication`. Una volta specificato il `authSpecName`, devi quindi includere le credenziali richieste nell’ambiente. Ad esempio, se specifichi `authSpecName` come `OAuth 2 Refresh Code`, devi quindi fornire le credenziali richieste per OAuth 2, che sono `host` e `accessToken`.

### Specifica `sourceSpec`

Aggiungendo i parametri di autenticazione, è necessario aggiungere le proprietà richieste dalla specifica di origine. Puoi trovare le proprietà richieste in `sourceSpec.spec.properties`. Nel caso di [!DNL MailChimp Members] di seguito, l’unica proprietà richiesta è `listId`, ossia `listId` ed è il valore ID corrispondente al tuo [!DNL Postman] ambiente.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Una volta forniti i parametri di autenticazione e specifica di origine, puoi iniziare a popolare le altre variabili di ambiente, vedi la tabella seguente per riferimento:

>[!NOTE]
>
>Tutte le variabili di esempio riportate di seguito sono valori segnaposto che è necessario aggiornare, ad eccezione di `flowSpecificationId` e `targetConnectionSpecId`, che sono valori fissi.

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `x-api-key` | Identificatore univoco utilizzato per autenticare le chiamate alle API di Experience Platform. Guarda l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Un&#39;entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Guarda l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../landing/postman.md) per istruzioni su come recuperare `x-gw-ims-org-id` informazioni. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Token di autorizzazione necessario per completare le chiamate alle API di Experience Platform. Guarda l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Versione univoca corrispondente allo schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | La `meta:altId` che viene restituito accanto al  `schemaId` durante la creazione di un nuovo schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | I set di mapping possono essere utilizzati per definire il modo in cui i dati di uno schema di origine vengono mappati su quello di uno schema di destinazione. Per i passaggi dettagliati su come creare una mappatura, consulta l’esercitazione su [creazione di un set di mappature utilizzando l’API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | L&#39;ID univoco che corrisponde al set di mappatura. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | ID della specifica di connessione corrispondente alla tua origine. Questo è l&#39;ID generato dopo [creazione di una nuova specifica di connessione](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | ID della specifica di flusso di `RestStorageToAEP`. **Questo è un valore fisso**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | L’ID di connessione di destinazione del data lake in cui arrivano i dati acquisiti. **Questo è un valore fisso**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervallo di tempo designato da seguire per il controllo del completamento di un’esecuzione di flusso. | `40` |
| `startTime` | L’ora di inizio designata per il flusso di dati. L&#39;ora di inizio deve essere formattata in tempo unix. | `1597784298` |

Dopo aver fornito tutte le variabili di ambiente, puoi iniziare a eseguire la raccolta utilizzando [!DNL Postman] interfaccia. In [!DNL Postman] , seleziona i puntini di sospensione (**...**) accanto [!DNL Sources SSSs Verification Collection] quindi seleziona **Esegui raccolta**.

![corridore](../assets/runner.png)

La [!DNL Runner] viene visualizzata un’interfaccia che ti consente di configurare l’ordine di esecuzione del flusso di dati. Seleziona **Esegui raccolta di verifica SSS** per eseguire la raccolta.

>[!NOTE]
>
>È possibile disabilitare **Elimina flusso** dalla lista di controllo per l’esecuzione se preferisci utilizzare il dashboard di monitoraggio delle sorgenti nell’interfaccia utente di Platform. Tuttavia, una volta terminato il test, è necessario assicurarsi che i flussi di test vengano eliminati.

![raccolta](../assets/run-collection.png)

## Invia l&#39;origine

Una volta che la sorgente è in grado di completare l’intero flusso di lavoro, puoi contattare il tuo rappresentante di Adobe e inviare la tua sorgente per l’integrazione.