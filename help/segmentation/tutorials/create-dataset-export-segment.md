---
keywords: ' Experience Platform;home;argomenti popolari;Segmentation Service;segmentation;creare un set di dati;esportare segmenti di pubblico;esportare segmenti;'
solution: Experience Platform
title: Creare un set di dati per l’esportazione di un segmento di pubblico
topic: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per creare un dataset che può essere utilizzato per esportare un segmento di pubblico utilizzando l'interfaccia utente del Experience Platform .
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# Creare un dataset per l&#39;esportazione di un segmento di pubblico

[!DNL Adobe Experience Platform] consente di segmentare facilmente i profili dei clienti in audience in base a attributi specifici. Una volta creati i segmenti, puoi esportare il pubblico in un dataset dal quale è possibile accedervi e agire. Affinché l&#39;esportazione abbia esito positivo, il dataset deve essere configurato correttamente.

Questa esercitazione descrive i passaggi necessari per creare un dataset che possa essere utilizzato per esportare un segmento di pubblico utilizzando l&#39;interfaccia [!DNL Experience Platform].

Questa esercitazione è direttamente correlata ai passaggi descritti nell&#39;esercitazione per [valutare e accedere ai risultati del segmento](./evaluate-a-segment.md). L&#39;esercitazione di valutazione di un segmento fornisce i passaggi per la creazione di un dataset utilizzando l&#39;API [!DNL Catalog Service], mentre questa esercitazione descrive i passaggi per creare un dataset utilizzando l&#39;interfaccia [!DNL Experience Platform].

## Introduzione

Per esportare un segmento, il dataset deve essere basato su [!DNL XDM Individual Profile Union Schema]. Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi di tutti gli schemi che condividono la stessa classe, in questo caso si tratta della classe [!DNL XDM Individual Profile]. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, vedere la sezione relativa al profilo cliente in tempo reale della guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/schema/composition.md#union).[

Per visualizzare gli schemi di unione nell&#39;interfaccia utente, fate clic su **[!UICONTROL Profiles]** nella navigazione a sinistra, quindi fate clic sulla scheda **[!UICONTROL Union schema]** come mostrato di seguito.

![Scheda Schema unione nell&#39;interfaccia utente  Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Area di lavoro DataSet

L&#39;area di lavoro dei set di dati all&#39;interno dell&#39; [!DNL Experience Platform] interfaccia utente consente di visualizzare e gestire tutti i set di dati creati dall&#39;organizzazione IMS e di crearne di nuovi.

Per visualizzare l&#39;area di lavoro dei set di dati, fare clic su **[!UICONTROL Datasets]** nella barra di navigazione a sinistra, quindi fare clic sulla scheda **[!UICONTROL Browse]**. L&#39;area di lavoro dei dataset contiene un elenco di set di dati, tra cui colonne che mostrano nome, data e ora create, origine, schema e ultimo stato batch, nonché la data e l&#39;ora dell&#39;ultimo aggiornamento del dataset. A seconda della larghezza di ciascuna colonna, potrebbe essere necessario scorrere verso sinistra o verso destra per visualizzare tutte le colonne.

>[!NOTE]
>
>Fate clic sull&#39;icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per [!DNL Real-time Customer Profile].

![Visualizza tutti i set di dati](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Creare un dataset

Per creare un set di dati, fare clic su **[!UICONTROL Create Dataset]** nell&#39;angolo superiore destro dell&#39;area di lavoro **[!UICONTROL Datasets]**.

![Fate clic su Crea set di dati](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Nella schermata **[!UICONTROL Create Dataset]**, fare clic su **[!UICONTROL Create Dataset from Schema]** per continuare.

![Seleziona origine dati](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleziona schema unione profilo singolo XDM

Per selezionare [!DNL XDM Individual Profile Union Schema] da utilizzare nel dataset, individuare lo schema &quot;[!UICONTROL XDM Individual Profile]&quot; con un tipo di &quot;[!UICONTROL Union]&quot; nella schermata **[!UICONTROL Select Schema]**.

Selezionato il pulsante di scelta accanto a **[!UICONTROL XDM Individual Profile]**, quindi fare clic su **[!UICONTROL Next]** nell&#39;angolo superiore destro.

![Seleziona schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configura set di dati

Nella schermata **[!UICONTROL Configure Dataset]**, sarà necessario assegnare al dataset un nome e fornire anche una descrizione del dataset.

**Note sui nomi dei set di dati:**
- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo di descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il dataset ha un nome e una descrizione, fare clic su **[!UICONTROL Finish]**.

![Configura set di dati](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Attività DataSet

Ora è stato creato un set di dati vuoto e si è tornati alla scheda **[!UICONTROL Dataset Activity]** nell&#39;area di lavoro **[!UICONTROL Datasets]**. Il nome del set di dati deve essere visualizzato nell’angolo in alto a sinistra dell’area di lavoro, insieme alla notifica che &quot;Non sono stati aggiunti batch&quot;. Questo è previsto perché non avete ancora aggiunto alcun batch a questo set di dati.

Sul lato destro dell&#39;area di lavoro Set di dati viene visualizzata la scheda **[!UICONTROL Info]** contenente informazioni relative al nuovo set di dati come ID dataset, nome, descrizione, nome tabella, schema, streaming e origine. La scheda **[!UICONTROL Info]** include inoltre informazioni su quando è stato creato il set di dati e sulla data dell&#39;ultima modifica.

Prendete nota di **[!UICONTROL Dataset ID]**, in quanto questo valore è richiesto per completare il flusso di lavoro di esportazione del segmento di pubblico.

![Attività DataSet](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Passaggi successivi

Dopo aver creato un set di dati basato su [!DNL XDM Individual Profile Union Schema], è possibile utilizzare l&#39;ID del set di dati per continuare l&#39;esercitazione [valutazione e accesso ai risultati del segmento](./evaluate-a-segment.md).

Al momento, tornate all&#39;esercitazione sui risultati del segmento di valutazione e fate clic sul passaggio [generatore di profili per i membri del pubblico](./evaluate-a-segment.md#generate-profiles) del flusso di lavoro di esportazione di un segmento.
