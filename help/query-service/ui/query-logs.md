---
title: Registri query
description: I registri delle query vengono generati automaticamente ogni volta che viene eseguita una query e sono disponibili tramite l’interfaccia utente per facilitare la risoluzione dei problemi. Questo documento illustra come utilizzare e navigare nella sezione Registri di Query Service dell’interfaccia utente.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# Registri query

>[!IMPORTANT]
>
>Alcune funzioni dei registri di query sono attualmente in una versione limitata e non sono disponibili per tutti i clienti. L’interfaccia utente potrebbe apparire leggermente diversa senza un’icona di modifica. Inoltre, il processo di selezione di un nome di query potrebbe richiedere lo spostamento all’Editor query invece che al [!UICONTROL Dettagli registro query] visualizzazione.

Adobe Experience Platform mantiene un registro di tutti gli eventi di query che si verificano sia tramite l’API che tramite l’interfaccia utente. Queste informazioni sono disponibili nell’interfaccia utente di Query Service da [!UICONTROL Registri] scheda.

I file di registro vengono generati automaticamente da qualsiasi evento di query e contengono informazioni quali l&#39;istruzione SQL utilizzata, lo stato della query, il tempo impiegato e l&#39;ultima esecuzione. È possibile utilizzare i dati di registro delle query come strumento potente per la risoluzione di problemi inefficienti o di query con problemi. Informazioni di registro più complete sono conservate come parte della funzione di registro di audit e sono disponibili nella sezione [documentazione del registro di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## Controllare i registri query

Per controllare i registri delle query, seleziona [!UICONTROL Query] per passare all’area di lavoro del servizio query e selezionare [!UICONTROL Log] dalle opzioni disponibili.

![Interfaccia utente di Platform con Query e Registro evidenziati.](../images/ui/query-log/logs.png)

## Personalizza ed esegui ricerche {#customize-and-search}

I registri di Query Service vengono presentati in un formato di tabella personalizzabile. Per personalizzare le colonne della tabella, selezionare l&#39;icona delle impostazioni (![Un&#39;icona delle impostazioni.](../images/ui/query-log/settings-icon.png)) a destra dello schermo. A [!UICONTROL Personalizza tabella] viene visualizzata una finestra di dialogo in cui è possibile deselezionare ogni colonna.

Puoi anche cercare i registri relativi a modelli di query specifici digitando il nome del modello nel campo di ricerca.

![L’area di lavoro Registro query con la barra di ricerca e l’elenco a discesa Gestisci tabella colonne sono evidenziati.](../images/ui/query-log/customize-logs.png)

A [descrizione per ciascuna colonna della tabella di registro](./overview.md#log) sono disponibili nella sezione Log della panoramica di Query Service.

## Esplorare i dati di registro

Ogni riga rappresenta i dati di registro per un&#39;esecuzione di query associata a un modello di query. Seleziona una riga della tabella per inserire nella barra laterale a destra i dati di registro per l’esecuzione.

![L’area di lavoro Registro query con una riga selezionata ed evidenziati i dati di registro nella barra laterale a destra.](../images/ui/query-log/log-details.png)

Nel pannello dei dettagli del registro, puoi selezionare un nuovo set di dati di output e visualizzare o copiare la query SQL completa utilizzata nell’esecuzione.

![L’area di lavoro Registro query con una riga selezionata ed evidenziati il set di dati di output e la query SQL.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Alcune funzioni dei registri di query sono attualmente in una versione limitata e non sono disponibili per tutti i clienti.

È inoltre possibile selezionare il nome di un modello di query dall&#39; [!UICONTROL Nome] per passare direttamente al [!UICONTROL Dettagli registro query] visualizzazione.

>[!NOTE]
>
>Se la query è stata creata utilizzando l’API e non è stato fornito alcun nome di modello durante l’inizializzazione, vengono invece visualizzati i primi decine di caratteri della query SQL.

![Visualizzazione dei dettagli del registro query.](../images/ui/query-log/query-log-details.png)

Accanto al nome del modello di ogni riga o al frammento SQL è presente l&#39;icona a forma di matita (![Un’icona a forma di matita.](../images/ui/query-log/edit-icon.png)) che è possibile utilizzare per passare all’editor delle query. La query viene quindi precompilata nell’editor per la modifica.

![Nell’area di lavoro Registro query è evidenziata un’icona a forma di matita.](../images/ui/query-log/edit-query.png)

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio come i registri delle query vengono utilizzati e accessibili nell’interfaccia utente di Query Service.

Consulta la [Panoramica dell’interfaccia utente](./overview.md)o [Guida API di Query Service](../api/getting-started.md) per ulteriori informazioni sulle funzionalità di Query Service.

Consulta la [monitorare il documento delle query](./monitor-queries.md) per scoprire come Query Service migliora la visibilità delle esecuzioni pianificate delle query.
