---
title: Creare una connessione sorgente di Marketo Engage e un flusso di dati per i dati di attività personalizzati nell’interfaccia utente
description: Questo tutorial descrive i passaggi necessari per creare una connessione di origine del Marketo Engage e un flusso di dati nell’interfaccia utente per inserire dati personalizzati sulle attività in Adobe Experience Platform.
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Creare un [!DNL Marketo Engage] connessione di origine e flusso di dati per i dati di attività personalizzati nell’interfaccia utente

>[!NOTE]
>
>Questa esercitazione fornisce passaggi specifici su come impostare e portare **attività personalizzata** dati da [!DNL Marketo] all&#39;Experience Platform. Per i passaggi su come portare **attività standard** dati, leggi [[!DNL Marketo] Guida all’interfaccia utente](./marketo.md).

Oltre a [attività standard](../../../../connectors/adobe-applications/mapping/marketo.md#activities), è inoltre possibile utilizzare [!DNL Marketo] per inserire dati di attività personalizzati in Adobe Experience Platform. Questo documento descrive come creare una connessione di origine e un flusso di dati per i dati delle attività personalizzate utilizzando [!DNL Marketo] nell’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Spazi dei nomi B2B e utilità di generazione automatica dello schema](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): l’utility di generazione automatica degli spazi dei nomi B2B e dello schema consente di utilizzare [!DNL Postman] per generare automaticamente i valori per gli spazi dei nomi e gli schemi B2B. Prima di creare uno schema e uno spazio dei nomi B2B, devi completare [!DNL Marketo] connessione sorgente e flusso di dati.
* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Creare e modificare gli schemi nell’interfaccia utente](../../../../../xdm/ui/resources/schemas.md): scopri come creare e modificare gli schemi nell’interfaccia utente di.
* [Spazi dei nomi delle identità](../../../../../identity-service/features/namespaces.md): gli spazi dei nomi di identità sono un componente di [!DNL Identity Service] che fungono da indicatori del contesto a cui si riferisce un’identità. Un’identità completa include un valore ID e uno spazio dei nomi.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Recuperare i dettagli dell’attività personalizzata

Il primo passaggio per importare dati di attività personalizzati da [!DNL Marketo] Ad Experience Platform, per recuperare il nome API e il nome visualizzato dell’attività personalizzata.

Accedi al tuo account utilizzando [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) di rete. Nel menu di navigazione a sinistra, sotto [!DNL Database Management], seleziona **Attività personalizzate Marketo**.

L’interfaccia viene aggiornata con una visualizzazione delle attività personalizzate, che include informazioni sui rispettivi nomi visualizzati e nomi API. Puoi anche utilizzare la barra a destra per selezionare e visualizzare altre attività personalizzate dal tuo account.

![L’interfaccia Attività personalizzate nell’interfaccia utente di Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Seleziona **Campi** dall’intestazione superiore per visualizzare i campi associati all’attività personalizzata. In questa pagina puoi visualizzare i nomi, i nomi API, le descrizioni e i tipi di dati dei campi nell’attività personalizzata. I dettagli relativi ai singoli campi verranno utilizzati in un passaggio successivo, durante la creazione di uno schema.

![La pagina Dettagli campi attività personalizzati di Marketo nell’interfaccia utente del Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Impostare gruppi di campi per attività personalizzate nello schema delle attività B2B

In *[!UICONTROL Schemi]* dashboard dell’interfaccia utente di Experienci Platform, seleziona **[!UICONTROL Sfoglia]** e quindi seleziona **[!UICONTROL Attività B2B]** dall’elenco degli schemi.

>[!TIP]
>
>Utilizza la barra di ricerca per accelerare la navigazione nell’elenco degli schemi.

![L’area di lavoro degli schemi nell’interfaccia utente Experienci Platform con lo schema di attività B2B selezionato.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Crea un nuovo gruppo di campi per l’attività personalizzata

Quindi, aggiungi un nuovo gruppo di campi al [!DNL B2B Activity] schema. Questo gruppo di campi deve corrispondere all’attività personalizzata che desideri acquisire e deve utilizzare il nome visualizzato dell’attività personalizzata recuperato in precedenza.

Per aggiungere un nuovo gruppo di campi, seleziona **[!UICONTROL + Aggiungi]** accanto al *[!UICONTROL Gruppi di campi]* pannello in *[!UICONTROL Composizione]*.

![Struttura dello schema.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

Il *[!UICONTROL Aggiungi gruppi di campi]* viene visualizzata la finestra. Seleziona **[!UICONTROL Crea nuovo gruppo di campi]** quindi specifica lo stesso nome visualizzato per l’attività personalizzata recuperata in un passaggio precedente e, facoltativamente, una descrizione per il nuovo gruppo di campi. Al termine, seleziona **[!UICONTROL Aggiungi gruppi di campi]**.

![Finestra per l&#39;etichettatura e la creazione di un nuovo gruppo di campi.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Una volta creato, il nuovo gruppo di campi per l’attività personalizzata viene visualizzato nel [!UICONTROL Gruppi di campi] catalogo.

![Struttura dello schema con un nuovo gruppo di campi aggiunto nel pannello gruppo di campi.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Aggiungere un nuovo campo alla struttura dello schema

Quindi, aggiungi un nuovo campo allo schema. Questo nuovo campo deve essere impostato su `type: object` e conterrà i singoli campi dell’attività personalizzata.

Per aggiungere un nuovo campo, selezionare il segno più (`+`) accanto al nome dello schema. Una voce per *[!UICONTROL Campo senza titolo | Tipo]* viene visualizzato. Quindi, configura le proprietà del campo utilizzando *[!UICONTROL Proprietà campo]* pannello. Imposta il nome del campo come nome API dell&#39;attività personalizzata e imposta il nome visualizzato come nome visualizzato dell&#39;attività personalizzata. Quindi, impostate il tipo come `object` e assegna il gruppo di campi al gruppo di campi attività personalizzato creato nel passaggio precedente. Al termine, seleziona **[!UICONTROL Applica]**.

![La struttura dello schema con il segno più (`+`) selezionato per consentire l&#39;aggiunta di un nuovo campo.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

Il nuovo campo viene visualizzato nello schema.

![È stato aggiunto un nuovo campo allo schema.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Aggiungi campi secondari al campo oggetto {#add-sub-fields-to-the-object-field}

L’ultimo passaggio nella preparazione dello schema consiste nell’aggiungere singoli campi all’interno del campo creato nel passaggio precedente.

![Un gruppo di sottocampi aggiunti a un campo all’interno dello schema.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Creare un flusso di dati

Al termine dell’impostazione dello schema, ora puoi procedere con la creazione di un flusso di dati per i dati delle attività personalizzate.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL applicazioni Adobe] categoria, seleziona **[!UICONTROL Marketo Engage]**. Quindi, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL Marketo] flusso di dati.

![Catalogo delle origini nell’interfaccia utente di Experienci Platform con l’origine del Marketo Engage selezionata.](../../../../images/tutorials/create/marketo/catalog.png)

### Selezionare i dati

Seleziona **[!UICONTROL Attività]** dall’elenco di [!DNL Marketo] set di dati e quindi seleziona **[!UICONTROL Successivo]**.

![Il passaggio Seleziona dati nel flusso di lavoro origini con il set di dati attività selezionato.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Dettagli del flusso di dati

Avanti, [fornire informazioni per il flusso di dati](./marketo.md#provide-dataflow-details), inclusi nomi e descrizioni per il set di dati e il flusso di dati, lo schema che verrà utilizzato e le configurazioni per [!DNL Profile] acquisizione, diagnostica degli errori e acquisizione parziale.

![Passaggio dei dettagli del flusso di dati.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Mappatura

Le mappature per i campi attività standard vengono compilate automaticamente, ma i campi attività personalizzati devono essere mappati manualmente sui campi di destinazione corrispondenti.

Per iniziare a mappare i campi di attività personalizzati, seleziona **[!UICONTROL Nuovo tipo di campo]** e quindi seleziona **[!UICONTROL Aggiungi nuovo campo]**.

![Il passaggio di mappatura con il menu a discesa per aggiungere un nuovo campo.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Passa alla struttura dei dati di origine e trova il campo attività personalizzato da acquisire. Al termine, seleziona **[!UICONTROL Seleziona]**.

>[!TIP]
>
>Per evitare confusione e gestire nomi di campo duplicati, i campi di attività personalizzati hanno il prefisso nome API.

![Struttura dei dati di origine.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Per aggiungere un campo di destinazione, seleziona l’icona schema ![icona schema](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) quindi seleziona i campi di attività personalizzati dallo schema di destinazione.

![Struttura dello schema di destinazione.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Ripeti i passaggi per aggiungere gli altri campi personalizzati di mappatura attività. Al termine, seleziona **[!UICONTROL Successivo]**.

![Tutte le mappature per i dati di origine e di destinazione.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Revisione

Il *[!UICONTROL Revisione]* viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente dell’entità di origine scelta e l’importo delle colonne all’interno di tale entità di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Salva e acquisisci]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio di revisione finale che riepiloga le informazioni sui campi di connessione, set di dati e mappatura.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### Aggiungere attività personalizzate a un flusso di dati di attività esistente {#add-to-existing-dataflows}

Per aggiungere dati di attività personalizzati a un flusso di dati esistente, modifica le mappature di un flusso di dati di attività esistente con i dati di attività personalizzati che desideri acquisire. Questo consente di acquisire l’attività personalizzata nello stesso set di dati delle attività esistenti. Per ulteriori informazioni su come aggiornare le mappature di un flusso di dati esistente, consulta la guida su [aggiornamento dei flussi di dati nell’interfaccia utente](../../update-dataflows.md).

### Utilizzare [!DNL Query Service] per filtrare le attività per le attività personalizzate {#query-service-filter}

Una volta completato il flusso di dati, puoi utilizzare [Servizio query](../../../../../query-service/home.md) per filtrare le attività in base ai dati delle attività personalizzate.

Quando le attività personalizzate vengono acquisite in Platform, il nome API dell’attività personalizzata diventa automaticamente il relativo `eventType`. Utilizzare `eventType={API_NAME}` per filtrare i dati di attività personalizzati.

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

Utilizza il `IN` clausola per filtrare più attività personalizzate:

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

L&#39;immagine seguente mostra un esempio di istruzione SQL nella [Editor query](../../../../../query-service/ui/user-guide.md) che filtra i dati di attività personalizzati.

![Nell’interfaccia utente di Platform viene visualizzato un esempio di query per attività personalizzate.](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## Passaggi successivi

Seguendo questa esercitazione, hai impostato uno schema di Platform per [!DNL Marketo] ha personalizzato i dati di attività e creato un flusso di dati per trasferirli a Platform. Per informazioni generali su [!DNL Marketo] sorgente, leggi [[!DNL Marketo] panoramica dell’origine](../../../../connectors/adobe-applications/marketo/marketo.md).
