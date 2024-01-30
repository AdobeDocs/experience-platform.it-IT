---
title: Modelli di query
description: I modelli di query sono query SQL salvate riutilizzabili che possono essere riutilizzate da altri utenti per risparmiare tempo e fatica. Possono essere create utilizzando Query Editor o Query Service API e sono disponibili per l’utilizzo su tutti i set di dati di Experienci Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: 1a44be939a4678078b414658199472e07dee153b
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Modelli di query

Adobe Experience Platform Query Service consente di salvare e riutilizzare il codice SQL sotto forma di modelli di query. I modelli consentono di risparmiare tempo evitando la ripetizione di operazioni eseguite di frequente. È possibile condividere i modelli all&#39;interno dell&#39;organizzazione e modificare facilmente i valori delle query senza dover accedere o comprendere le istruzioni SQL sottostanti.

Questo documento fornisce le informazioni necessarie per creare modelli di query in Query Service.

## Prerequisiti

È necessario disporre di [!UICONTROL Gestire le query] autorizzazione abilitata per accedere all’editor delle query e visualizzare il dashboard delle query nell’interfaccia utente di Platform. L’autorizzazione è abilitata tramite l’Adobe [Admin Console](https://adminconsole.adobe.com/). Se non disponi dei privilegi di amministratore per abilitare questa autorizzazione, contatta l’amministratore della tua organizzazione. Consulta la documentazione sul controllo degli accessi per [istruzioni complete sull’aggiunta di autorizzazioni tramite Admin Console](../../access-control/home.md).

## Creare un modello di query

È possibile creare modelli di query tramite due metodi, effettuando una richiesta POST all’API di Query Service `query-templates` o scrivendo, denominando e salvando una query tramite l&#39;editor delle query.

### Utilizza l’editor delle query per creare e salvare una query come modello

Per istruzioni su come utilizzare l’editor di query per [scrivere](./user-guide.md#query-authoring) e [salvare le query](./user-guide.md#saving-queries). Una volta denominata e salvata la query, questa può essere riutilizzata come modello di query dall&#39; [!UICONTROL Modelli] scheda.

>[!TIP]
>
>Quando salvi una query nell’editor delle query, viene visualizzato un messaggio di conferma per informarti dell’azione riuscita. Questo messaggio a comparsa contiene un collegamento che consente di accedere facilmente all’area di lavoro di pianificazione delle query. Consulta la [documentazione sulle query di pianificazione](./query-schedules.md) per scoprire come eseguire query su una cadenza personalizzata.

## Sfoglia modelli di query {#browse}

Dall’area di lavoro Query dell’interfaccia utente di Platform, seleziona **[!UICONTROL Modelli]** per visualizzare l&#39;elenco delle query salvate disponibili.

![L’area di lavoro delle query con la scheda Modelli evidenziata.](../images/ui/query-templates/query-templates.png)

Per trovare informazioni rilevanti sul modello, seleziona un modello di query dall’elenco disponibile per aprire il pannello dei dettagli.

![Il pannello dei dettagli nell’area di lavoro query con l’ID query evidenziato.](../images/ui/query-templates/details-panel.png)

Dal pannello dei dettagli è possibile eseguire le azioni seguenti:

* Seleziona **[!UICONTROL Esegui come CTAS]** per creare una nuova tabella selezionando i dati da una o più tabelle esistenti. Questa opzione è disponibile solo se si dispone di una query SELECT.
* Seleziona **[!UICONTROL Aggiungi pianificazione]** per iniziare a modificare la pianificazione per il modello di query.
* Seleziona **[!UICONTROL Visualizza pianificazione]** per passare al [!UICONTROL Schedules] dell&#39;editor di query. Questa visualizzazione contiene tutte le informazioni sulla programmazione associate alla query.
* Seleziona **[!UICONTROL Elimina query]** per eliminare il modello.
* Selezionare il nome del modello per passare all&#39;editor di query in cui l&#39;istruzione SQL è precompilata per la modifica.

### Utilizzare l’API Query Service per creare un modello

Per istruzioni su, consulta la documentazione di [come creare un modello di query](../api/query-templates.md#create-a-query-template) utilizzando l’API Query Service. I dettagli di un modello di query appena creato sono contenuti nel corpo della risposta.

>[!NOTE]
>
>I modelli creati utilizzando l’API sono visibili anche nella scheda Modelli del servizio di query dell’interfaccia utente di Platform.

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio come creare modelli di query in Query Service. Consulta la [Panoramica dell’interfaccia utente](./overview.md)o [Guida API di Query Service](../api/getting-started.md) per ulteriori informazioni sulle funzionalità di Query Service.

Consulta la [guida dell’endpoint &quot;scheduled queries&quot;](../api/scheduled-queries.md) per scoprire come pianificare le query utilizzando l’API o [Guida all’editor delle query](./user-guide.md#scheduled-queries) per l’interfaccia utente.
