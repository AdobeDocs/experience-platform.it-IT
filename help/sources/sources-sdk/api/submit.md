---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Invia la tua origine
description: Il documento seguente illustra come verificare e testare una nuova origine utilizzando l’API del servizio Flusso e integrare una nuova origine tramite Origini self-service (SDK batch).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Invia l&#39;origine

Il passaggio finale per integrare la nuova origine in Adobe Experience Platform utilizzando Self-Serve Sources (SDK batch) consiste nel testare l’origine per la verifica. In caso di esito positivo, puoi inviare la nuova sorgente contattando il rappresentante dell’Adobe.

Il documento seguente illustra i passaggi per testare ed eseguire il debug dell’origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

* Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).
* Per informazioni su come generare le credenziali per le API di Platform, consulta l’esercitazione su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md).
* Per informazioni su come impostare [!DNL Postman] per le API di Platform, consulta l’esercitazione su [configurazione della console per sviluppatori e [!DNL Postman]](../../../landing/postman.md).
* Per facilitare il processo di test e debug, scarica il file [Raccolta e ambiente di verifica delle origini self-service qui](../assets/sdk-verification.zip) e segui i passaggi descritti di seguito.

## Verifica l’origine

Per verificare l&#39;origine, è necessario eseguire il comando [Raccolta e ambiente di verifica delle origini self-service](../assets/sdk-verification.zip) il [!DNL Postman] fornendo al tempo stesso le variabili di ambiente appropriate relative alla tua origine.

Per avviare il test, devi prima impostare la raccolta e l’ambiente su [!DNL Postman]. Specificare quindi l&#39;ID della specifica di connessione che si desidera verificare.

### Specifica `authSpecName`

Dopo aver inserito l&#39;ID della specifica di connessione, è necessario specificare `authSpecName` che utilizzi per la connessione di base. A seconda della scelta, potrebbe essere `OAuth 2 Refresh Code` o  `Basic Authentication`. Dopo aver specificato `authSpecName`, è quindi necessario includere le credenziali richieste nell’ambiente. Ad esempio, se specifichi `authSpecName` as `OAuth 2 Refresh Code`, è necessario fornire le credenziali richieste per OAuth 2, che sono `host` e `accessToken`.

### Specifica `sourceSpec`

Aggiungendo i parametri della specifica di autenticazione, devi aggiungere le proprietà richieste dalla specifica di origine. Puoi trovare le proprietà richieste in `sourceSpec.spec.properties`. Nel caso di [!DNL MailChimp Members] nell’esempio seguente, l’unica proprietà richiesta è `listId`, che significa `listId` e il valore ID corrispondente al tuo [!DNL Postman] ambiente.

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

Una volta forniti i parametri di autenticazione e di specifica dell’origine, puoi iniziare a popolare le altre variabili di ambiente, per riferimento consulta la tabella seguente:

>[!NOTE]
>
>Tutte le variabili di esempio riportate di seguito sono valori segnaposto da aggiornare, ad eccezione di `flowSpecificationId` e `targetConnectionSpecId`, che sono valori fissi.

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `x-api-key` | Identificatore univoco utilizzato per autenticare le chiamate alle API Experience Platform. Guarda il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Guarda il tutorial su [configurazione della console per sviluppatori e [!DNL Postman]](../../../landing/postman.md) per istruzioni su come recuperare `x-gw-ims-org-id` informazioni. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Il token di autorizzazione necessario per completare le chiamate alle API Experience Platform. Guarda il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite l’API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Versione univoca corrispondente allo schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | Il `meta:altId` che viene restituito insieme al  `schemaId` durante la creazione di un nuovo schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite l’API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | I set di mappatura possono essere utilizzati per definire il modo in cui i dati in uno schema di origine vengono mappati a quelli di uno schema di destinazione. Per i passaggi dettagliati su come creare una mappatura, consulta l’esercitazione su [creazione di un set di mappatura tramite l’API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | L’ID univoco che corrisponde al set di mappatura. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | ID della specifica di connessione corrispondente alla sorgente. Questo è l’ID che hai generato dopo [creazione di una nuova specifica di connessione](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | ID della specifica di flusso di `RestStorageToAEP`. **Valore fisso**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | ID della connessione di destinazione del data lake in cui arrivano i dati acquisiti. **Valore fisso**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | L’intervallo di tempo designato da seguire durante il controllo del completamento di un’esecuzione del flusso. | `40` |
| `startTime` | Ora di inizio designata per il flusso di dati. L&#39;ora di inizio deve essere formattata come ora unix. | `1597784298` |

Dopo aver fornito tutte le variabili di ambiente, puoi iniziare a eseguire la raccolta utilizzando [!DNL Postman] di rete. In [!DNL Postman] , selezionare i puntini di sospensione (**...**) accanto a [!DNL Sources SSSs Verification Collection] e quindi seleziona **Esegui raccolta**.

![corridore](../assets/runner.png)

Il [!DNL Runner] viene visualizzata l’interfaccia, che consente di configurare l’ordine di esecuzione del flusso di dati. Seleziona **Esegui raccolta di verifica SSS** per eseguire la raccolta.

>[!NOTE]
>
>Puoi disattivare **Elimina flusso** dall’elenco di controllo dell’ordine di esecuzione, se preferisci utilizzare il dashboard di monitoraggio delle origini nell’interfaccia utente di Platform. Tuttavia, una volta terminato il test, devi assicurarti che i flussi di test vengano eliminati.

![run-collection](../assets/run-collection.png)

## Invia l&#39;origine

Una volta che la tua sorgente è in grado di completare l’intero flusso di lavoro, puoi procedere a contattare il rappresentante del tuo Adobe e inviare la sorgente per l’integrazione.
