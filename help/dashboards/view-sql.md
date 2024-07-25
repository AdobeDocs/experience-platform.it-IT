---
title: Visualizza SQL approfondimento
description: Visualizza le istruzioni SQL alla base di Profilo, Pubblico, Destinazione e approfondimenti personalizzati ed esegui la query su richiesta tramite l’Editor query.
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Visualizza SQL approfondimento

Utilizza la funzione [!UICONTROL Visualizza SQL] per visualizzare le istruzioni SQL dietro a Profilo, Pubblico, Destinazione e approfondimenti personalizzati ed eseguire la query su richiesta tramite l&#39;Editor query. Ispirati all’SQL di oltre 40 informazioni esistenti per creare nuove query che derivano informazioni univoche dai dati di Platform in base alle esigenze aziendali.

## Passa alla panoramica del dashboard {#navigate-to-overview}

Per aprire il dashboard scelto, seleziona **[!UICONTROL Profili]**, **[!UICONTROL Tipi di pubblico]** o **[!UICONTROL Destinazioni]** dal menu di navigazione a sinistra. Selezionare **[!UICONTROL Panoramica]** dalle opzioni di scheda se l&#39;area di lavoro non viene visualizzata automaticamente.

In alternativa, seleziona **[!UICONTROL Dashboard]** dal menu di navigazione a sinistra seguito dal nome del dashboard personalizzato. Viene visualizzata la panoramica del dashboard definito dall&#39;utente.

![Interfaccia utente Experience Platform con [!UICONTROL Profili], [!UICONTROL Tipi di pubblico], [!UICONTROL Destinazioni] e [!UICONTROL Dashboard] evidenziati.](./images/view-sql/dashboard-navigation.png)

## Visualizza/nascondi SQL {#toggle}

È disponibile un interruttore dalla panoramica delle dashboard di Profilo, Pubblico, Destinazione e definite dall’utente per abilitare o disabilitare la funzione.

>[!NOTE]
>
>Se si abilita l&#39;interruttore [!UICONTROL Visualizza SQL], non sarà possibile modificare i filtri globali e i filtri a livello di widget finché non si disabilita la funzionalità.

![L&#39;interruttore [!UICONTROL Visualizza SQL] è evidenziato.](./images/view-sql/view-sql-toggle.png)

Attiva l&#39;interruttore per visualizzare [!UICONTROL Visualizza il testo SQL] su ogni singola informazione.

![Informazioni approfondite con [!UICONTROL Visualizza SQL] evidenziate.](./images/view-sql/insight-view-sql.png)

Selezionare **[!UICONTROL Visualizza SQL]** per aprire una finestra di dialogo contenente l&#39;istruzione SQL del widget.

## Finestra di dialogo SQL {#sql-dialog}

Viene visualizzata una finestra di dialogo che contiene il titolo dell’approfondimento e l’istruzione SQL che lo genera.

>[!TIP]
>
>È possibile copiare l&#39;intera istruzione SQL negli Appunti selezionando l&#39;icona Copia (![Icona Copia.](/help/images/icons/copy.png)) in alto a destra nella finestra di dialogo.

![Una finestra di dialogo di approfondimento con l&#39;istruzione SQL evidenziata.](./images/view-sql/sql-dialog.png)

Selezionare **[!UICONTROL Esegui SQL]** per aprire l&#39;editor di query con la query precompilata.

![È evidenziata una finestra di dialogo di approfondimento con [!UICONTROL Esegui SQL].](./images/view-sql/run-sql.png)

## Modifica SQL esistente {#edit-sql}

Viene visualizzato l&#39;editor delle query. Ora puoi modificare l’istruzione ed eseguire query sui dati della piattaforma in modo che soddisfino meglio le tue esigenze di reporting. Salva il nuovo modello di query con un nome appropriato.

![L&#39;editor di query con l&#39;istruzione SQL di approfondimento precompilata.](./images/view-sql/edit-sql.png)

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di accedere al linguaggio SQL per ottenere informazioni approfondite all’interno dei dashboard standard o di un dashboard definito dall’utente. Se non lo hai già fatto, ti consigliamo di leggere il [documento del modello dati di Real-time Customer Data Platform Insights](./data-models/cdp-insights-data-model-b2c.md). Questo documento contiene informazioni sulla personalizzazione dei modelli SQL per i rapporti di Real-Time CDP personalizzati in base alle tue esigenze di marketing e KPI.
