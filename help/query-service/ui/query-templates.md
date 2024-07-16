---
title: Modelli di query
description: I modelli di query sono query SQL salvate riutilizzabili che possono essere riutilizzate da altri utenti per risparmiare tempo e fatica. Possono essere create utilizzando Query Editor o Query Service API e sono disponibili per l’utilizzo su tutti i set di dati di Experience Platform.
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

Per accedere all&#39;editor delle query e visualizzare il dashboard delle query nell&#39;interfaccia utente di Platform, è necessario che sia abilitata l&#39;autorizzazione [!UICONTROL Gestisci query]. L&#39;autorizzazione è abilitata tramite l&#39;Adobe [Admin Console](https://adminconsole.adobe.com/). Se non disponi dei privilegi di amministratore per abilitare questa autorizzazione, contatta l’amministratore della tua organizzazione. Consulta la documentazione sul controllo degli accessi per [istruzioni complete sull&#39;aggiunta di autorizzazioni tramite Admin Console](../../access-control/home.md).

## Creare un modello di query

È possibile creare modelli di query tramite due metodi, effettuando una richiesta POST all&#39;endpoint API `query-templates` di Query Service oppure scrivendo, denominando e salvando una query tramite l&#39;editor di query.

### Utilizza l’editor delle query per creare e salvare una query come modello

Consulta la documentazione per istruzioni su come utilizzare l&#39;editor query per [scrivere](./user-guide.md#query-authoring) e [salvare le query](./user-guide.md#saving-queries). Una volta denominata e salvata la query, è possibile riutilizzarla come modello di query dalla scheda [!UICONTROL Modelli].

>[!TIP]
>
>Quando salvi una query nell’editor delle query, viene visualizzato un messaggio di conferma per informarti dell’azione riuscita. Questo messaggio a comparsa contiene un collegamento che consente di accedere facilmente all’area di lavoro di pianificazione delle query. Per informazioni su come eseguire query su una cadenza personalizzata, consulta la [documentazione sulle query di pianificazione](./query-schedules.md).

## Sfoglia modelli di query {#browse}

Dall&#39;area di lavoro Query dell&#39;interfaccia utente di Platform, selezionare **[!UICONTROL Modelli]** per visualizzare l&#39;elenco delle query salvate disponibili.

![Area di lavoro query con la scheda Modelli evidenziata.](../images/ui/query-templates/query-templates.png)

Per trovare informazioni rilevanti sul modello, seleziona un modello di query dall’elenco disponibile per aprire il pannello dei dettagli.

![Il pannello dei dettagli nell&#39;area di lavoro delle query con l&#39;ID della query evidenziato.](../images/ui/query-templates/details-panel.png)

Dal pannello dei dettagli è possibile eseguire le azioni seguenti:

* Selezionare **[!UICONTROL Esegui come CTAS]** per creare una nuova tabella selezionando i dati da una o più tabelle esistenti. Questa opzione è disponibile solo se si dispone di una query SELECT.
* Seleziona **[!UICONTROL Aggiungi pianificazione]** per iniziare a modificare la pianificazione per il modello di query.
* Seleziona **[!UICONTROL Visualizza pianificazione]** per passare alla scheda [!UICONTROL Pianificazioni] dell&#39;editor query. Questa visualizzazione contiene tutte le informazioni sulla programmazione associate alla query.
* Selezionare **[!UICONTROL Elimina query]** per eliminare il modello.
* Selezionare il nome del modello per passare all&#39;editor di query in cui l&#39;istruzione SQL è precompilata per la modifica.

### Utilizzare l’API Query Service per creare un modello

Per istruzioni su [come creare un modello di query](../api/query-templates.md#create-a-query-template) utilizzando l&#39;API di Query Service, vedere la documentazione. I dettagli di un modello di query appena creato sono contenuti nel corpo della risposta.

>[!NOTE]
>
>I modelli creati utilizzando l’API sono visibili anche nella scheda Modelli del servizio di query dell’interfaccia utente di Platform.

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio come creare modelli di query in Query Service. Per ulteriori informazioni sulle funzionalità di Query Service, consulta la [Panoramica dell&#39;interfaccia utente](./overview.md) o la [Guida API di Query Service](../api/getting-started.md).

Per informazioni su come pianificare le query utilizzando l&#39;API o la [guida dell&#39;editor query](./user-guide.md#scheduled-queries) per l&#39;interfaccia utente, consulta la [guida dell&#39;endpoint query pianificate](../api/scheduled-queries.md).
