---
title: Visualizza SQL approfondimento
description: Visualizza le istruzioni SQL alla base di Profilo, Pubblico, Destinazione e approfondimenti personalizzati ed esegui la query su richiesta tramite l’Editor query.
source-git-commit: be90cf38970a54431f48799bf506fb0a20ec0166
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Visualizza SQL approfondimento

Utilizza il [!UICONTROL Visualizza SQL] funzionalità per visualizzare le istruzioni SQL alla base di Profilo, Pubblico, Destinazione e approfondimenti personalizzati ed eseguire la query su richiesta tramite l’Editor query. Ispirati all’SQL di oltre 40 informazioni esistenti per creare nuove query che derivano informazioni univoche dai dati di Platform in base alle esigenze aziendali.

## Passa alla panoramica del dashboard {#navigate-to-overview}

Per aprire il dashboard scelto, seleziona una delle seguenti opzioni **[!UICONTROL Profili]**, **[!UICONTROL Tipi di pubblico]**, o **[!UICONTROL Destinazioni]** dal menu di navigazione a sinistra. Selezione successiva **[!UICONTROL Panoramica]** dalle opzioni della scheda se l’area di lavoro non viene visualizzata automaticamente.

In alternativa, seleziona **[!UICONTROL Dashboard]** dalla barra di navigazione a sinistra seguita dal nome del dashboard personalizzato. Viene visualizzata la panoramica del dashboard definito dall&#39;utente.

![L’interfaccia utente di Experienci Platform con [!UICONTROL Profili], [!UICONTROL Tipi di pubblico], [!UICONTROL Destinazioni], e [!UICONTROL Dashboard] evidenziato.](./images/view-sql/dashboard-navigation.png)

## Visualizza/nascondi SQL {#toggle}

È disponibile un interruttore dalla panoramica delle dashboard di Profilo, Pubblico, Destinazione e definite dall’utente per abilitare o disabilitare la funzione.

>[!NOTE]
>
>Se si abilita [!UICONTROL Visualizza SQL] , non è possibile modificare i filtri globali e i filtri a livello di widget finché non si disattiva la funzione.

![Il [!UICONTROL Visualizza SQL] evidenziata.](./images/view-sql/view-sql-toggle.png)

Attiva/disattiva visualizzazione [!UICONTROL Visualizza SQL] testo su ogni singola informazione.

![Approfondimenti su [!UICONTROL Visualizza SQL] evidenziato.](./images/view-sql/insight-view-sql.png)

Seleziona **[!UICONTROL Visualizza SQL]** per aprire una finestra di dialogo contenente l&#39;istruzione SQL del widget.

## Finestra di dialogo SQL {#sql-dialog}

Viene visualizzata una finestra di dialogo che contiene il titolo dell’approfondimento e l’istruzione SQL che lo genera.

>[!TIP]
>
>È possibile copiare l&#39;intera istruzione SQL negli Appunti selezionando l&#39;icona Copia (![Icona Copia.](./images/view-sql/copy-icon.png)) in alto a destra nella finestra di dialogo.

![Viene evidenziata una finestra di dialogo di approfondimento con l&#39;istruzione SQL.](./images/view-sql/sql-dialog.png)

Seleziona **[!UICONTROL Esegui SQL]** per aprire l’Editor query con la query è precompilato.

![Una finestra di dialogo di approfondimento con [!UICONTROL Esegui SQL] evidenziato.](./images/view-sql/run-sql.png)

## Modifica SQL esistente {#edit-sql}

Viene visualizzato l&#39;editor delle query. Ora puoi modificare l’istruzione ed eseguire query sui dati della piattaforma in modo che soddisfino meglio le tue esigenze di reporting. Salva il nuovo modello di query con un nome appropriato.

![L’editor delle query con l’istruzione SQL di approfondimento precompilata.](./images/view-sql/edit-sql.png)

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di accedere al linguaggio SQL per ottenere informazioni approfondite all’interno dei dashboard standard o di un dashboard definito dall’utente. Se non lo hai già fatto, ti consigliamo di leggere la [Documento del modello dati di Real-time Customer Data Platform Insights](./cdp-insights-data-model.md). Questo documento contiene informazioni sulla personalizzazione dei modelli SQL per i rapporti di Real-Time CDP personalizzati in base alle tue esigenze di marketing e KPI.
