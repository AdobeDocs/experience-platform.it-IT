---
keywords: Experience Platform;home;argomenti popolari;servizio di segmentazione;segmentazione;segmentazione;creare un set di dati;esportare segmenti di pubblico;esportare segmenti;
solution: Experience Platform
title: Creare un set di dati per l’esportazione di un segmento di pubblico
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per creare un set di dati che può essere utilizzato per esportare un segmento di pubblico utilizzando l’interfaccia utente di Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Creare un set di dati per esportare un segmento di pubblico

[!DNL Adobe Experience Platform] consente di segmentare facilmente i profili dei clienti in audience in base ad attributi specifici. Una volta creati i segmenti, puoi esportare il pubblico in un set di dati a cui è possibile accedervi e su cui agisce. Affinché l’esportazione abbia successo, il set di dati deve essere configurato correttamente.

Questa esercitazione descrive i passaggi necessari per creare un set di dati che può essere utilizzato per esportare un segmento di pubblico utilizzando l’ [!DNL Experience Platform] interfaccia utente .

Questa esercitazione è direttamente correlata ai passaggi descritti nell&#39;esercitazione per [valutare e accedere ai risultati dei segmenti](./evaluate-a-segment.md). L’esercitazione di valutazione di un segmento fornisce passaggi per la creazione di un set di dati utilizzando l’ API [!DNL Catalog Service] , mentre questa esercitazione descrive i passaggi per creare un set di dati utilizzando l’ [!DNL Experience Platform] interfaccia utente.

## Introduzione

Per esportare un segmento, il set di dati deve essere basato su [!DNL XDM Individual Profile Union Schema]. Uno schema di unione è uno schema generato dal sistema e di sola lettura che aggrega i campi di tutti gli schemi che condividono la stessa classe, in questo caso si tratta della classe [!DNL XDM Individual Profile]. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, consulta la sezione [Profilo del cliente in tempo reale della guida per gli sviluppatori del registro dello schema](../../xdm/schema/composition.md#union).

Per visualizzare gli schemi di unione nell&#39;interfaccia utente, fai clic su **[!UICONTROL Profiles]** nel menu di navigazione a sinistra, quindi fai clic sulla scheda **[!UICONTROL Union schema]** come mostrato di seguito.

![Scheda schema unione nell’interfaccia utente di Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Area di lavoro dei set di dati

L’area di lavoro dei set di dati all’interno dell’ [!DNL Experience Platform] interfaccia utente consente di visualizzare e gestire tutti i set di dati creati dall’organizzazione IMS e di crearne di nuovi.

Per visualizzare l’area di lavoro dei set di dati, fai clic su **[!UICONTROL Datasets]** nella navigazione a sinistra, quindi fai clic sulla scheda **[!UICONTROL Browse]** . L’area di lavoro dei set di dati contiene un elenco di set di dati, tra cui colonne che mostrano nome, data e ora create, origine, schema e stato dell’ultimo batch, nonché la data e l’ora dell’ultimo aggiornamento del set di dati. A seconda della larghezza di ogni colonna, potrebbe essere necessario scorrere a sinistra o a destra per visualizzare tutte le colonne.

>[!NOTE]
>
>Fai clic sull’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per [!DNL Real-time Customer Profile].

![Visualizza tutti i set di dati](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Creare un set di dati

Per creare un set di dati, fai clic su **[!UICONTROL Create Dataset]** nell’angolo in alto a destra dell’area di lavoro **[!UICONTROL Datasets]**.

![Fai clic su Crea set di dati](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Nella schermata **[!UICONTROL Create Dataset]**, fai clic su **[!UICONTROL Create Dataset from Schema]** per continuare.

![Seleziona origine dati](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleziona schema di unione profili individuale XDM

Per selezionare il [!DNL XDM Individual Profile Union Schema] da utilizzare nel set di dati, trova lo schema &quot;[!UICONTROL XDM Individual Profile]&quot; con un tipo di &quot;[!UICONTROL Union]&quot; nella schermata **[!UICONTROL Select Schema]**.

Selezionato il pulsante di scelta accanto a **[!UICONTROL XDM Individual Profile]**, quindi fai clic su **[!UICONTROL Next]** nell’angolo in alto a destra.

![Seleziona schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurare il set di dati

Nella schermata **[!UICONTROL Configure Dataset]** , ti verrà richiesto di assegnare un nome al set di dati e può anche fornire una descrizione del set di dati.

**Note sui nomi dei set di dati:**
- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono anche essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il set di dati ha un nome e una descrizione, fai clic su **[!UICONTROL Finish]**.

![Configurare il set di dati](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Attività set di dati

Ora è stato creato un set di dati vuoto e sei stato riportato nella scheda **[!UICONTROL Dataset Activity]** nell’area di lavoro **[!UICONTROL Datasets]**. Dovresti visualizzare il nome del set di dati nell’angolo in alto a sinistra dell’area di lavoro, insieme a una notifica che indica che non sono stati aggiunti batch. Questo è da aspettarsi, in quanto non hai ancora aggiunto batch a questo set di dati.

Sul lato destro dell’area di lavoro Set di dati viene visualizzata la scheda **[!UICONTROL Info]** contenente informazioni relative al nuovo set di dati come ID set di dati, nome, descrizione, nome tabella, schema, streaming e origine. La scheda **[!UICONTROL Info]** include anche informazioni su quando è stato creato il set di dati e la sua ultima data di modifica.

Prendi nota del **[!UICONTROL Dataset ID]**, in quanto questo valore è necessario per completare il flusso di lavoro di esportazione del segmento di pubblico.

![Attività set di dati](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Passaggi successivi

Dopo aver creato un set di dati basato su [!DNL XDM Individual Profile Union Schema], puoi utilizzare l’ID set di dati per continuare l’ esercitazione [valutazione e accesso ai risultati del segmento](./evaluate-a-segment.md) .

Al momento, torna all’esercitazione sui risultati del segmento di valutazione e seleziona dal passaggio [generazione di profili per i membri del pubblico](./evaluate-a-segment.md#generate-profiles) dell’esportazione di un flusso di lavoro del segmento.
