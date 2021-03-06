---
keywords: Experience Platform;home;argomenti popolari;servizio di segmentazione;segmentazione;segmentazione;creare un set di dati;esportare segmenti di pubblico;esportare segmenti;
solution: Experience Platform
title: Creare un set di dati per l’esportazione di un segmento di pubblico
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per creare un set di dati che può essere utilizzato per esportare un segmento di pubblico utilizzando l’interfaccia utente di Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 44d7e11e79ed0e6041ff2e4438ddb7141ae3532d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Creare un set di dati per esportare un segmento di pubblico

[!DNL Adobe Experience Platform] consente di segmentare i profili dei clienti in audience in base ad attributi specifici. Una volta creato un segmento, puoi esportare il pubblico in un set di dati a cui è possibile accedervi e su cui agisce. Affinché l’esportazione abbia successo, il set di dati deve essere configurato correttamente.

Questa esercitazione descrive i passaggi necessari per creare un set di dati che può essere utilizzato per esportare un segmento di pubblico utilizzando l’ [!DNL Experience Platform] interfaccia utente .

Questa esercitazione è direttamente correlata ai passaggi descritti nell&#39;esercitazione su [valutazione e accesso ai risultati dei segmenti](./evaluate-a-segment.md). L’esercitazione sulla valutazione dei segmenti fornisce passaggi per creare un set di dati utilizzando l’ API [!DNL Catalog Service] , mentre questa esercitazione descrive i passaggi per creare un set di dati utilizzando l’ [!DNL Experience Platform] interfaccia utente.

## Introduzione

Per esportare un segmento, il set di dati deve essere basato su [!DNL XDM Individual Profile Union Schema]. Uno schema di unione è uno schema generato dal sistema e di sola lettura che aggrega i campi di tutti gli schemi che condividono la stessa classe. Per ulteriori informazioni sugli schemi di unione, consulta la guida sulle [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md#union).

Per visualizzare gli schemi di unione nell&#39;interfaccia utente, seleziona **[!UICONTROL Profili]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Schema di unione]** come mostrato di seguito.

![Scheda schema unione nell’interfaccia utente di Experience Platform](../images/tutorials/segment-export-dataset/union.png)


## Area di lavoro dei set di dati

L&#39;area di lavoro [!UICONTROL Set di dati] ti consente di visualizzare e gestire tutti i set di dati dell&#39;organizzazione.

Seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra per accedere all&#39;area di lavoro, quindi seleziona **[!UICONTROL Sfoglia]**. In questa scheda viene visualizzato un elenco dei set di dati e dei relativi dettagli. A seconda della larghezza di ogni colonna, potrebbe essere necessario scorrere a sinistra o a destra per visualizzare tutte le colonne.

>[!NOTE]
>
>Seleziona l’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per [!DNL Real-time Customer Profile].

![Visualizzare i set di dati](../images/tutorials/segment-export-dataset/browse.png)

## Creare un set di dati

Per creare un set di dati, seleziona **[!UICONTROL Crea set di dati]**.

![Seleziona Crea set di dati](../images/tutorials/segment-export-dataset/create-dataset.png)

Nella schermata successiva, seleziona **[!UICONTROL Crea set di dati da schema]**.

![Seleziona origine dati](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Seleziona schema di unione profili individuale XDM

Per selezionare il [!DNL XDM Individual Profile Union Schema] da utilizzare nel set di dati, trova lo schema &quot;[!UICONTROL XDM Singolo profilo]&quot; nella schermata **[!UICONTROL Seleziona schema]**. Dopo aver selezionato lo schema, puoi confermare se si tratta dello schema di unione in **[!UICONTROL Utilizzo API]** nella barra a destra. Se il percorso [!UICONTROL Schema] termina con `_union`, si tratta di uno schema di unione.

>[!NOTE]
>
>Nonostante gli schemi di unione partecipino per definizione al Profilo del cliente in tempo reale, vengono elencati come &quot;Non abilitati&quot; a causa del fatto che non sono abilitati per il profilo allo stesso modo degli schemi tradizionali.

Seleziona il pulsante di scelta accanto a **[!UICONTROL Profilo individuale XDM]**, quindi seleziona **[!UICONTROL Avanti]**.

![Seleziona schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurare il set di dati

Nella schermata successiva, devi assegnare un nome al set di dati. Puoi anche aggiungere una descrizione facoltativa.

**Note sui nomi dei set di dati:**
* I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
* I nomi dei set di dati devono essere univoci, il che significa che devono anche essere sufficientemente specifici da non essere riutilizzati in futuro.
* È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il set di dati ha un nome e una descrizione, seleziona **[!UICONTROL Fine]**.

![Configurare il set di dati](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Attività set di dati

Una volta creato il set di dati, vieni portato alla pagina dell’attività per quel set di dati. Dovresti visualizzare il nome del set di dati nell’angolo in alto a sinistra dell’area di lavoro, insieme a una notifica che indica che non sono stati aggiunti batch. Questo è da aspettarsi, in quanto non hai ancora aggiunto batch a questo set di dati.

La barra a destra contiene informazioni relative al nuovo set di dati quali ID set di dati, nome, descrizione, schema e altro ancora. Prendi nota del **[!UICONTROL ID set di dati]**, in quanto questo valore è necessario per completare il flusso di lavoro di esportazione del segmento di pubblico.

![Attività set di dati](../images/tutorials/segment-export-dataset/activity.png)

## Passaggi successivi

Dopo aver creato un set di dati basato su [!DNL XDM Individual Profile Union Schema], puoi utilizzare l’ID set di dati per continuare l’ esercitazione [valutazione e accesso ai risultati del segmento](./evaluate-a-segment.md) .

Al momento, torna all’esercitazione sui risultati del segmento di valutazione e seleziona dal passaggio [generazione di profili per i membri del pubblico](./evaluate-a-segment.md#generate-profiles) dell’esportazione di un flusso di lavoro del segmento.
