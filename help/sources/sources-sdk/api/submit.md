---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Invia il tuo Source
description: Il documento seguente illustra come verificare e testare una nuova origine utilizzando l’API del servizio Flusso e integrare una nuova origine tramite Origini self-service (SDK batch).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Invia l&#39;origine

Il passaggio finale per integrare la nuova origine in Adobe Experience Platform utilizzando Self-Serve Sources (SDK batch) consiste nel testare l’origine per la verifica. In caso di esito positivo, puoi inviare la nuova sorgente contattando il rappresentante dell’Adobe.

Nel documento seguente vengono descritti i passaggi necessari per verificare ed eseguire il debug dell&#39;origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

* Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).
* Per informazioni su come generare le credenziali per le API di Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md).
* Per informazioni sulla configurazione di [!DNL Postman] per le API di Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md).
* Per facilitare il processo di test e debug, scarica la raccolta di verifica delle [origini self-service e l&#39;ambiente qui](../assets/sdk-verification.zip) e segui i passaggi descritti di seguito.

## Verifica l’origine

Per verificare l&#39;origine, è necessario eseguire la raccolta di verifica delle [origini self-service e l&#39;ambiente](../assets/sdk-verification.zip) in [!DNL Postman] fornendo le variabili di ambiente appropriate relative all&#39;origine.

Per avviare il test, è necessario prima impostare la raccolta e l&#39;ambiente in [!DNL Postman]. Specificare quindi l&#39;ID della specifica di connessione che si desidera verificare.

### Specifica `authSpecName`

Dopo aver immesso l&#39;ID della specifica di connessione, è necessario specificare `authSpecName` utilizzato per la connessione di base. A seconda della scelta, potrebbe essere `OAuth 2 Refresh Code` o `Basic Authentication`. Dopo aver specificato `authSpecName`, è necessario includere le credenziali richieste nell&#39;ambiente. Ad esempio, se si specifica `authSpecName` come `OAuth 2 Refresh Code`, è necessario fornire le credenziali richieste per OAuth 2, che sono `host` e `accessToken`.

### Specifica `sourceSpec`

Aggiungendo i parametri della specifica di autenticazione, devi aggiungere le proprietà richieste dalla specifica di origine. È possibile trovare le proprietà richieste in `sourceSpec.spec.properties`. Nel caso dell&#39;esempio di [!DNL MailChimp Members] riportato di seguito, l&#39;unica proprietà richiesta è `listId`, che significa `listId` e corrisponde al valore ID dell&#39;ambiente [!DNL Postman].

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
>Tutte le variabili di esempio seguenti sono valori segnaposto da aggiornare, ad eccezione di `flowSpecificationId` e `targetConnectionSpecId`, che sono valori fissi.

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `x-api-key` | Identificatore univoco utilizzato per autenticare le chiamate alle API Experience Platform. Per informazioni su come recuperare `x-api-key`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni di `x-gw-ims-org-id`, consulta il tutorial su [come configurare la console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md). | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Il token di autorizzazione necessario per completare le chiamate alle API Experience Platform. Per informazioni su come recuperare `authorizationToken`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `Bearer authorizationToken` |
| `schemaId` | Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Versione univoca corrispondente allo schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | `meta:altId` restituito insieme a `schemaId` durante la creazione di un nuovo schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l&#39;esercitazione su [creazione di un set di dati utilizzando l&#39;API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | I set di mappatura possono essere utilizzati per definire il modo in cui i dati in uno schema di origine vengono mappati a quelli di uno schema di destinazione. Per i passaggi dettagliati su come creare una mappatura, consulta l&#39;esercitazione su [creazione di un set di mappatura tramite l&#39;API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | L’ID univoco che corrisponde al set di mappatura. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | ID della specifica di connessione corrispondente alla sorgente. Questo è l&#39;ID generato dopo [la creazione di una nuova specifica di connessione](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | ID della specifica di flusso di `RestStorageToAEP`. **Valore fisso**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | ID della connessione di destinazione del data lake in cui arrivano i dati acquisiti. **Valore fisso**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | L’intervallo di tempo designato da seguire durante il controllo del completamento di un’esecuzione del flusso. | `40` |
| `startTime` | Ora di inizio designata per il flusso di dati. L&#39;ora di inizio deve essere formattata come ora unix. | `1597784298` |

Dopo aver fornito tutte le variabili di ambiente, è possibile avviare l&#39;esecuzione della raccolta utilizzando l&#39;interfaccia [!DNL Postman]. Nell&#39;interfaccia [!DNL Postman], selezionare i puntini di sospensione (**...**) accanto a [!DNL Sources SSSs Verification Collection], quindi selezionare **Esegui raccolta**.

![runner](../assets/runner.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner], che consente di configurare l&#39;ordine di esecuzione del flusso di dati. Selezionare **Esegui raccolta di verifica SSS** per eseguire la raccolta.

>[!NOTE]
>
>È possibile disabilitare **Elimina flusso** dall&#39;elenco di controllo dell&#39;ordine di esecuzione se si preferisce utilizzare il dashboard di monitoraggio delle origini nell&#39;interfaccia utente di Platform. Tuttavia, una volta terminato il test, devi assicurarti che i flussi di test vengano eliminati.

![run-collection](../assets/run-collection.png)

## Invia l&#39;origine

Una volta che la tua sorgente è in grado di completare l’intero flusso di lavoro, puoi procedere a contattare il rappresentante del tuo Adobe e inviare la sorgente per l’integrazione.
