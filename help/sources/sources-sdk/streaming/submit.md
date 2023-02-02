---
title: Test E Invio Dell'Origine
description: Il seguente documento fornisce passaggi su come testare e verificare una nuova origine utilizzando l’API del servizio di flusso e integrare una nuova origine tramite l’SDK per streaming (Streaming SDK).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# Test e invio dell&#39;origine

I passaggi finali per integrare la nuova origine in Adobe Experience Platform utilizzando Origini self-service (Streaming SDK) consistono nel testare e inviare la nuova origine. Una volta completate le specifiche di connessione e aggiornate le specifiche di flusso in streaming, puoi iniziare a testare le funzionalità della sorgente tramite l’API o l’interfaccia utente. In caso di esito positivo, puoi inviare la nuova origine contattando il rappresentante di Adobe.

Il seguente documento fornisce passaggi su come verificare ed eseguire il debug dell&#39;origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

* Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).
* Per informazioni su come generare le credenziali per le API di Platform, consulta l’esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md).
* Per informazioni su come impostare [!DNL Postman] per le API di Platform, consulta l’esercitazione su [configurazione di Developer Console e [!DNL Postman]](../../../landing/postman.md).
* Per facilitare il processo di test e debug, scarica il [Raccolta e ambiente di verifica di Origini self-service qui](../assets/sdk-verification.zip) e segui i passaggi descritti di seguito.

## Verificare la sorgente utilizzando l’API

Per testare la sorgente utilizzando l’API, è necessario eseguire il [Raccolta e ambiente di verifica di Origini self-service](../assets/sdk-verification.zip) su [!DNL Postman] fornendo le variabili di ambiente appropriate relative all’origine.

Per avviare il test, devi prima impostare la raccolta e l’ambiente su [!DNL Postman]. Quindi, specifica l&#39;ID della specifica di connessione da verificare.

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
| `flowSpecificationId` | ID della specifica di flusso di `GenericStreamingAEP`. **Questo è un valore fisso**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
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

## Verificare la sorgente utilizzando l’interfaccia utente

Per testare l’origine nell’interfaccia utente, passa al catalogo delle sorgenti della sandbox dell’organizzazione nell’interfaccia utente di Platform. Da qui, dovresti vedere la tua nuova sorgente sotto il *Streaming* categoria.

Con la nuova origine ora disponibile nella sandbox, è necessario seguire il flusso di lavoro origini per testare le funzionalità. Per iniziare, seleziona **[!UICONTROL Configurazione]**.

![Catalogo delle sorgenti che visualizza la nuova origine streaming.](../assets/testing/catalog-test.png)

La [!UICONTROL Aggiungi dati] viene visualizzato il passaggio . Per verificare che la sorgente possa inviare dati in streaming, utilizza il lato sinistro dell’interfaccia per caricare [un esempio di dati JSON](../assets/testing/raw.json.zip). Una volta caricati i dati, il lato destro dell’interfaccia si aggiorna in un’anteprima della gerarchia dei file dei dati. Seleziona **[!UICONTROL Successivo]** per procedere.

![Il passaggio Aggiungi dati nel flusso di lavoro origini , che consente di caricare e visualizzare in anteprima i dati prima dell’acquisizione.](../assets/testing/add-data-test.png)

La [!UICONTROL Dettaglio flusso di dati] consente di selezionare se si desidera utilizzare un set di dati esistente o un nuovo set di dati. Durante questo processo puoi anche configurare i dati da acquisire in Profilo e abilitare impostazioni come [!UICONTROL Diagnostica degli errori] e [!UICONTROL Acquisizione parziale].

Per eseguire il test, seleziona **[!UICONTROL Nuovo set di dati]** e fornisci il nome di un set di dati di output. Durante questo passaggio, puoi anche fornire una descrizione facoltativa per aggiungere ulteriori informazioni al set di dati. Quindi, seleziona uno schema a cui eseguire il mapping utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco degli schemi esistenti nel menu a discesa. Dopo aver selezionato uno schema, fornisci un nome e una descrizione per il flusso di dati.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Il passaggio dei dettagli del flusso di lavoro origini.](../assets/testing/dataflow-details-test.png)

La [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un&#39;interfaccia per mappare i campi di origine dallo schema di origine ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura e dei campi calcolati, consulta la sezione [Guida all’interfaccia utente della preparazione dei dati](../../../data-prep/ui/mapping.md)

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](../assets/testing/mapping-test.png)

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Visualizza il nome dell’account, il tipo di origine e altre informazioni varie specifiche dell’origine di archiviazione cloud in streaming che stai utilizzando.
* **[!UICONTROL Assegna set di dati e mappa campi]**: Visualizza il set di dati di destinazione e lo schema utilizzato per il flusso di dati.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

![Il passaggio di revisione del flusso di lavoro origini.](../assets/testing/review-test.png)

Infine, devi recuperare l’endpoint di streaming del flusso del flusso di dati. Questo endpoint verrà utilizzato per abbonarsi al tuo webhook, consentendo alla tua sorgente di streaming di comunicare con Experience Platform. Per recuperare l’endpoint di streaming, vai a [!UICONTROL Attività del flusso di dati] della pagina del flusso di dati appena creato e copia l’endpoint dalla parte inferiore della sezione [!UICONTROL Proprietà] pannello.

![L’endpoint di streaming nell’attività del flusso di dati.](../assets/testing/endpoint-test.png)

## Invia l&#39;origine

Una volta che la sorgente è in grado di completare l’intero flusso di lavoro, puoi contattare il tuo rappresentante di Adobe e inviare la tua sorgente per l’integrazione tra altre organizzazioni Experience Platform.
