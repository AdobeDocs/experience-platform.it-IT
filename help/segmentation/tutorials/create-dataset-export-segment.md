---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un dataset per l'esportazione di un segmento di pubblico
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# Creare un dataset per l&#39;esportazione di un segmento di pubblico

[!DNL Adobe Experience Platform] consente di segmentare facilmente i profili dei clienti in audience in base a attributi specifici. Una volta creati i segmenti, puoi esportare il pubblico in un dataset dal quale è possibile accedervi e agire. Affinché l&#39;esportazione abbia esito positivo, il dataset deve essere configurato correttamente.

Questa esercitazione descrive i passaggi necessari per creare un dataset che possa essere utilizzato per esportare un segmento di pubblico utilizzando l&#39; [!DNL Experience Platform] interfaccia utente.

Questa esercitazione è direttamente correlata ai passaggi descritti nell&#39;esercitazione per la [valutazione e l&#39;accesso ai risultati](./evaluate-a-segment.md)del segmento. L&#39;esercitazione di valutazione di un segmento fornisce i passaggi per la creazione di un dataset utilizzando l&#39; [!DNL Catalog Service] API, mentre questa esercitazione descrive i passaggi per creare un dataset utilizzando l&#39; [!DNL Experience Platform] interfaccia utente.

## Introduzione

Per esportare un segmento, il set di dati deve essere basato sul [!DNL XDM Individual Profile Union Schema]. Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi di tutti gli schemi che condividono la stessa classe, in questo caso si tratta della [!DNL XDM Individual Profile] classe. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, vedere la sezione Profilo cliente in tempo [reale della guida](../../xdm/schema/composition.md#union)per gli sviluppatori del Registro di sistema dello schema.

Per visualizzare gli schemi di unione nell&#39;interfaccia utente, fate clic **[!UICONTROL Profiles]** nel menu di navigazione a sinistra, quindi fate clic sulla **[!UICONTROL Union schema]** scheda come mostrato di seguito.

![Scheda Schema unione nell&#39;interfaccia utente  Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Area di lavoro DataSet

L&#39;area di lavoro dei set di dati nell&#39; [!DNL Experience Platform] interfaccia utente consente di visualizzare e gestire tutti i set di dati creati dall&#39;organizzazione IMS e di crearne di nuovi.

Per visualizzare l&#39;area di lavoro dei set di dati, fare clic **[!UICONTROL Datasets]** nella barra di navigazione a sinistra, quindi fare clic sulla *[!UICONTROL Browse]* scheda. L&#39;area di lavoro dei dataset contiene un elenco di set di dati, tra cui colonne che mostrano *[!UICONTROL Name]*, *[!UICONTROL Created]* (data e ora), *[!UICONTROL Source]*, *[!UICONTROL Schema]* e *[!UICONTROL Last Batch Status]* la data e l&#39;ora in cui si trovava il dataset *[!UICONTROL Last Updated]*. A seconda della larghezza di ciascuna colonna, potrebbe essere necessario scorrere verso sinistra o verso destra per visualizzare tutte le colonne.

>[!NOTE]
>
>Fate clic sull&#39;icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati [!DNL Real-time Customer Profile].

![Visualizza tutti i set di dati](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Creare un dataset

Per creare un dataset, fate clic **[!UICONTROL Create Dataset]** nell&#39;angolo superiore destro dell&#39; [!UICONTROL Datasets] area di lavoro.

![Fate clic su Crea set di dati](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Sullo *[!UICONTROL Create Dataset]* schermo, fare clic **[!UICONTROL Create Dataset from Schema]** per continuare.

![Seleziona origine dati](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleziona schema unione profilo singolo XDM

Per selezionare l&#39; [!DNL XDM Individual Profile Union Schema] utilizzo nel dataset, individuare lo schema &quot;[!UICONTROL XDM Individual Profile]&quot; con un tipo di &quot;[!UICONTROL Union]&quot; sullo *[!UICONTROL Select Schema]* schermo.

Selezionato il pulsante di scelta accanto a **[!UICONTROL XDM Individual Profile]**, quindi fate clic **[!UICONTROL Next]** nell&#39;angolo superiore destro.

![Seleziona schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configura set di dati

Sullo **[!UICONTROL Configure Dataset]** schermo, sarà necessario fornire al dataset un *[!UICONTROL Name]* e può anche fornire un *[!UICONTROL Description]* del dataset.

**Note sui nomi dei set di dati:**
- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo di descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il dataset ha un nome e una descrizione, fare clic su **[!UICONTROL Finish]**.

![Configura set di dati](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Attività DataSet

Ora è stato creato un set di dati vuoto e si è tornati alla *[!UICONTROL Dataset Activity]* scheda nell&#39; [!UICONTROL Datasets] area di lavoro. Il nome del set di dati deve essere visualizzato nell’angolo in alto a sinistra dell’area di lavoro, insieme alla notifica che &quot;Non sono stati aggiunti batch&quot;. Questo è previsto perché non avete ancora aggiunto alcun batch a questo set di dati.

Sul lato destro dell&#39;area di lavoro Set di dati è visibile la **[!UICONTROL Info]** scheda contenente informazioni relative al nuovo set di dati, ad esempio *[!UICONTROL Dataset ID]*, *[!UICONTROL Name]*, *[!UICONTROL Description]*, *[!UICONTROL Table Name]*, *[!UICONTROL Schema]*, *[!UICONTROL Streaming]* e *[!UICONTROL Source]*. La [!UICONTROL Info] scheda include inoltre informazioni su quando il set di dati era *[!UICONTROL Created]* e la relativa *[!UICONTROL Last Modified]* data.

Tenete presente **[!UICONTROL Dataset ID]**, in quanto questo valore è richiesto per completare il flusso di lavoro di esportazione del segmento di pubblico.

![Attività DataSet](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Passaggi successivi

Dopo aver creato un set di dati basato su [!DNL XDM Individual Profile Union Schema], puoi utilizzare il set **[!UICONTROL Dataset ID]** per continuare l’esercitazione sui risultati [di](./evaluate-a-segment.md) valutazione e accesso ai segmenti.

Al momento, tornate all’esercitazione sui risultati del segmento di valutazione e fate clic sul passaggio dei profili di [generazione per i membri](./evaluate-a-segment.md#generate-profiles) dell’audience nel passaggio del flusso di lavoro di esportazione di un segmento.
