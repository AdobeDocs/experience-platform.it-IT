---
title: Testare E Inviare Il Source
description: Il documento seguente illustra come verificare e testare una nuova origine utilizzando l’API del servizio Flusso e integrare una nuova origine tramite Origini self-service (Streaming SDK).
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Testare e inviare l’origine

>[!NOTE]
>
>L’SDK di streaming per origini self-service è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

I passaggi finali per integrare la nuova origine in Adobe Experience Platform utilizzando Self-Serve Sources (Streaming SDK) consistono nel testare e inviare la nuova origine. Dopo aver completato la specifica di connessione e aggiornato la specifica del flusso di streaming, puoi iniziare a testare la funzionalità della sorgente tramite l’API o l’interfaccia utente. In caso di esito positivo, puoi inviare la nuova sorgente contattando il rappresentante dell’Adobe.

Nel documento seguente vengono descritti i passaggi necessari per verificare ed eseguire il debug dell&#39;origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

* Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).
* Per informazioni su come generare le credenziali per le API di Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md).
* Per informazioni sulla configurazione di [!DNL Postman] per le API di Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md).
* Per facilitare il processo di test e debug, scarica la raccolta di verifica delle [origini self-service e l&#39;ambiente qui](../assets/sdk-verification.zip) e segui i passaggi descritti di seguito.

## Verifica l’origine utilizzando l’API

Per testare l&#39;origine utilizzando l&#39;API, è necessario eseguire la raccolta di verifica [Origini self-service e l&#39;ambiente](../assets/sdk-verification.zip) in [!DNL Postman] fornendo le variabili di ambiente appropriate relative all&#39;origine.

Per avviare il test, è necessario prima impostare la raccolta e l&#39;ambiente in [!DNL Postman]. Specificare quindi l&#39;ID della specifica di connessione che si desidera verificare.

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
| `flowSpecificationId` | ID della specifica di flusso di `GenericStreamingAEP`. **Valore fisso**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
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

## Verifica l’origine tramite l’interfaccia utente

Per testare l’origine nell’interfaccia utente, vai al catalogo delle origini della sandbox della tua organizzazione nell’interfaccia utente di Platform. Da qui dovresti vedere la tua nuova origine apparire nella categoria *Streaming*.

Con la nuova origine ora disponibile nella sandbox, devi seguire il flusso di lavoro delle sorgenti per testare le funzionalità. Per iniziare, selezionare **[!UICONTROL Configurazione]**.

![Catalogo origini che visualizza la nuova origine di streaming.](../assets/testing/catalog-test.png)

Viene visualizzato il passaggio [!UICONTROL Aggiungi dati]. Per verificare che l&#39;origine possa inviare dati in streaming, utilizza il lato sinistro dell&#39;interfaccia per caricare [dati JSON di esempio](../assets/testing/raw.json.zip). Una volta caricati i dati, il lato destro dell’interfaccia si aggiorna in un’anteprima della gerarchia dei file dei dati. Seleziona **[!UICONTROL Avanti]** per procedere.

![Il passaggio Aggiungi dati nel flusso di lavoro delle origini da cui puoi caricare e visualizzare in anteprima i dati prima dell&#39;acquisizione.](../assets/testing/add-data-test.png)

La pagina [!UICONTROL Dettagli flusso di dati] consente di scegliere se utilizzare un set di dati esistente o nuovo. Durante questo processo, puoi anche configurare i dati da acquisire nel profilo e abilitare impostazioni come [!UICONTROL Diagnostica errori] e [!UICONTROL Acquisizione parziale].

Per il test, selezionare **[!UICONTROL Nuovo set di dati]** e fornire un nome per il set di dati di output. Durante questo passaggio, puoi anche fornire una descrizione facoltativa per aggiungere ulteriori informazioni al set di dati. Quindi, seleziona uno schema a cui mappare utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] o scorrendo l&#39;elenco degli schemi esistenti nel menu a discesa. Dopo aver selezionato uno schema, fornisci un nome e una descrizione per il flusso di dati.

Al termine, selezionare **[!UICONTROL Avanti]**.

![Passaggio dei dettagli del flusso di dati nel flusso di lavoro delle origini.](../assets/testing/dataflow-details-test.png)

Viene visualizzato il passaggio [!UICONTROL Mappatura] che fornisce un&#39;interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../data-prep/ui/mapping.md)

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Avanti]**.

![Passaggio di mappatura del flusso di lavoro di origine.](../assets/testing/mapping-test.png)

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: visualizza il nome dell&#39;account, il tipo di origine e altre informazioni specifiche dell&#39;origine di archiviazione cloud in streaming in uso.
* **[!UICONTROL Assegna set di dati e mappa campi]**: visualizza il set di dati di destinazione e lo schema utilizzati per il flusso di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e attendi che venga creato un po&#39; di tempo.

![Passaggio di revisione del flusso di lavoro origini.](../assets/testing/review-test.png)

Infine, devi recuperare l’endpoint di streaming del flusso di dati. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experience Platform. Per recuperare l&#39;endpoint di streaming, vai alla pagina [!UICONTROL Attività flusso di dati] del flusso di dati appena creato e copia l&#39;endpoint dalla parte inferiore del pannello [!UICONTROL Proprietà].

![Endpoint di streaming nell&#39;attività del flusso di dati.](../assets/testing/endpoint-test.png)

## Invia l&#39;origine

Una volta che la tua sorgente è in grado di completare l’intero flusso di lavoro, puoi procedere a contattare il rappresentante dell’Adobe e inviare la sorgente per l’integrazione in altre organizzazioni Experienci Platform.
