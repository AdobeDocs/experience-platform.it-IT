---
solution: Experience Platform
title: Creare un set di dati per l’esportazione di un pubblico
type: Tutorial
description: Scopri come creare un set di dati che può essere utilizzato per esportare un pubblico utilizzando l’interfaccia utente di Experienci Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# Creare un set di dati per esportare un pubblico

[!DNL Adobe Experience Platform] consente di segmentare i profili dei clienti in tipi di pubblico in base ad attributi specifici. Una volta creata la definizione di un segmento, puoi esportare il pubblico risultante in un set di dati in cui è possibile accedervi e intervenire. Affinché l’esportazione abbia esito positivo, il set di dati deve essere configurato correttamente.

Questo tutorial illustra i passaggi necessari per creare un set di dati che possa essere utilizzato per esportare un pubblico utilizzando [!DNL Experience Platform] UI.

Questo tutorial è direttamente correlato ai passaggi descritti in esso [valutazione e accesso ai risultati della segmentazione](./evaluate-a-segment.md). L’esercitazione sulla valutazione della definizione del segmento descrive i passaggi per creare un set di dati utilizzando [!DNL Catalog Service] , mentre questo tutorial illustra i passaggi per creare un set di dati utilizzando [!DNL Experience Platform] UI.

## Introduzione

Per esportare un pubblico, il set di dati deve essere basato su [!DNL XDM Individual Profile Union Schema]. Uno schema di unione è uno schema di sola lettura generato dal sistema che aggrega i campi di tutti gli schemi che condividono la stessa classe. Per ulteriori informazioni sugli schemi di unione, consulta la guida su [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md#union).

Per visualizzare gli schemi di unione nell’interfaccia utente, seleziona **[!UICONTROL Profili]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Schema di unione]** come mostrato di seguito.

![Viene evidenziata la scheda schema di unione.](../images/tutorials/segment-export-dataset/union.png)

## Area di lavoro Set di dati

Il [!UICONTROL Set di dati] workspace consente di visualizzare e gestire tutti i set di dati dell’organizzazione.

Seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra per accedere all’area di lavoro, quindi seleziona **[!UICONTROL Sfoglia]**. Questa scheda visualizza un elenco di set di dati e i relativi dettagli. A seconda della larghezza di ciascuna colonna, potrebbe essere necessario scorrere verso sinistra o verso destra per visualizzare tutte le colonne.

>[!NOTE]
>
>Seleziona l’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro e visualizzare solo i set di dati abilitati per [!DNL Real-Time Customer Profile].

![Viene visualizzata l’area di lavoro dei set di dati.](../images/tutorials/segment-export-dataset/browse.png)

## Creare un set di dati

Per creare un set di dati, seleziona **[!UICONTROL Crea set di dati]**.

![Viene evidenziato il pulsante Crea set di dati.](../images/tutorials/segment-export-dataset/create-dataset.png)

Nella schermata successiva, seleziona **[!UICONTROL Crea set di dati dallo schema]**.

![Viene evidenziata l’opzione Crea set di dati da schema.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Seleziona schema di unione profili individuali XDM

Per selezionare [!DNL XDM Individual Profile Union Schema] da utilizzare nel set di dati, trova la sezione &quot;[!UICONTROL Profilo individuale XDM]Schema &quot; sul **[!UICONTROL Seleziona schema]** schermo. Dopo aver selezionato lo schema, puoi confermare se si tratta dello schema di unione in **[!UICONTROL Utilizzo API]** nella barra a destra. Se il [!UICONTROL Schema] il percorso termina con `_union`, è uno schema di unione.

>[!NOTE]
>
>Nonostante gli schemi unione partecipino a Real-Time Customer Profile per definizione, vengono elencati come &quot;Non abilitati&quot; perché non sono abilitati per il profilo allo stesso modo degli schemi tradizionali.

Seleziona il pulsante di opzione accanto a **[!UICONTROL Profilo individuale XDM]**, quindi seleziona **[!UICONTROL Successivo]**.

![Viene evidenziato lo schema Profilo individuale XDM.](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurare il set di dati

Nella schermata successiva, devi assegnare un nome al set di dati. È inoltre possibile aggiungere una descrizione facoltativa.

**Note sui nomi dei set di dati:**

* I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato in un secondo momento nella libreria.
* I nomi dei set di dati devono essere univoci, ovvero devono essere sufficientemente specifici da non poter essere riutilizzati in futuro.
* È necessario fornire informazioni aggiuntive sul set di dati utilizzando il campo descrizione, in quanto potrebbe aiutare altri utenti a distinguere i set di dati in futuro.

Una volta che il set di dati ha un nome e una descrizione, seleziona **[!UICONTROL Fine]**.

![Viene visualizzata la pagina Configura set di dati. Vengono evidenziate le opzioni di configurazione.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Attività set di dati

Una volta creato il set di dati, viene visualizzata la pagina dell’attività per tale set di dati. Dovresti visualizzare il nome del set di dati nell’angolo in alto a sinistra dell’area di lavoro, insieme a una notifica che informa che &quot;Non è stato aggiunto alcun batch&quot;. Ciò è previsto perché non hai ancora aggiunto batch a questo set di dati.

La barra a destra contiene informazioni relative al nuovo set di dati, ad esempio ID set di dati, nome, descrizione, schema e altro ancora. Si prega di prendere nota della **[!UICONTROL ID set di dati]**, poiché questo valore è necessario per completare il flusso di lavoro di esportazione del pubblico.

![Viene visualizzata la pagina dell’attività del set di dati. L’ID del set di dati viene evidenziato, in quanto questo valore deve essere annotato per i passaggi futuri.](../images/tutorials/segment-export-dataset/activity.png)

## Passaggi successivi

Ora che hai creato un set di dati basato su [!DNL XDM Individual Profile Union Schema], puoi utilizzare l’ID del set di dati per continuare la [valutazione e accesso ai risultati della definizione del segmento](./evaluate-a-segment.md) esercitazione.

In questo momento, torna all’esercitazione sui risultati della definizione del segmento di valutazione e riprendi da [generazione di profili per i membri del pubblico](./evaluate-a-segment.md#generate-profiles) passaggio del flusso di lavoro esportazione di un pubblico.
