---
title: Registri delle query
description: I registri di query vengono generati automaticamente ogni volta che viene eseguita una query e sono disponibili tramite l’interfaccia utente per facilitare la risoluzione dei problemi. Questo documento illustra come utilizzare e navigare nella sezione Registri di servizio query dell’interfaccia utente.
source-git-commit: 95d3604a9589a4d0db7e426dd000ddec9cd4f2ce
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# Registro delle query

>[!IMPORTANT]
>
>Alcune funzioni dei registri di query sono attualmente in una versione limitata e non sono disponibili per tutti i clienti. L’interfaccia utente potrebbe essere leggermente diversa senza un’icona di modifica. Inoltre, il processo di selezione di un nome di query può passare all’editor delle query anziché al [!UICONTROL Dettagli del registro query] visualizza.

Adobe Experience Platform gestisce un registro di tutti gli eventi di query che si verificano tramite sia l’API che l’interfaccia utente. Queste informazioni sono disponibili nell’interfaccia utente del servizio query nel [!UICONTROL Registri] scheda .

I file di registro vengono generati automaticamente da qualsiasi evento di query e contengono informazioni quali l&#39;SQL utilizzato, lo stato della query, il tempo necessario e l&#39;ultima esecuzione. È possibile utilizzare i dati del registro delle query come potente strumento per la risoluzione dei problemi di query inefficienti o di problemi. Le informazioni di registro più complete vengono conservate come parte della funzione di registro di controllo e sono disponibili nella sezione [documentazione del registro di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## Controlla i log delle query

Per controllare i registri di query, seleziona [!UICONTROL Query] per passare all’area di lavoro Servizio query e selezionare [!UICONTROL Registro] dalle opzioni disponibili.

![Interfaccia utente della piattaforma con query e registro evidenziati.](../images/ui/query-log/logs.png)

## Personalizzare e cercare {#customize-and-search}

I registri del servizio query vengono presentati in un formato tabella personalizzabile. Per personalizzare le colonne della tabella, seleziona l’icona delle impostazioni (![Icona delle impostazioni.](../images/ui/query-log/settings-icon.png)) a destra dello schermo. A [!UICONTROL Personalizza tabella] viene visualizzata una finestra di dialogo in cui è possibile deselezionare ogni colonna.

È inoltre possibile cercare i registri relativi a specifici modelli di query digitando il nome del modello nel campo di ricerca.

![Area di lavoro Registro query con il menu a discesa della tabella delle colonne e della barra di ricerca evidenziato.](../images/ui/query-log/customize-logs.png)

A [descrizione per ciascuna colonna della tabella di registro](./overview.md#log) Si trova nella sezione Registro della panoramica del servizio query.

## Scopri i dati del registro

Ciascuna riga rappresenta i dati di registro per un’esecuzione di query associata a un modello di query. Seleziona una riga dalla tabella per compilare la barra laterale destra con i dati di registro per l’esecuzione.

![Area di lavoro Registro query con una riga selezionata e i dati di registro nella barra laterale destra evidenziati.](../images/ui/query-log/log-details.png)

Nel pannello dei dettagli del registro, è possibile selezionare un nuovo set di dati di output e visualizzare o copiare l&#39;intera query SQL utilizzata nell&#39;esecuzione.

![Area di lavoro Registro query con una riga selezionata e set di dati di output e query SQL evidenziate.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Alcune funzioni dei registri di query sono attualmente in una versione limitata e non sono disponibili per tutti i clienti.

Puoi anche selezionare un nome di modello di query dal [!UICONTROL Nome] per passare direttamente alla colonna [!UICONTROL Dettagli del registro query] visualizza.

>[!NOTE]
>
>Se la query è stata creata utilizzando l&#39;API e non è stato fornito alcun nome di modello durante l&#39;inizializzazione, vengono invece visualizzati i primi dodici caratteri della query SQL.

![Visualizzazione dei dettagli del registro query.](../images/ui/query-log/query-log-details.png)

Accanto al nome del modello di ogni riga o al frammento SQL è presente un&#39;icona a forma di matita (![Icona a forma di matita.](../images/ui/query-log/edit-icon.png)) che è possibile utilizzare per passare all’Editor query. La query viene quindi precompilata nell’editor per la modifica.

![Area di lavoro Registro query con icona a forma di matita evidenziata.](../images/ui/query-log/edit-query.png)

## Passaggi successivi

Leggendo questo documento, è ora possibile comprendere meglio come si accedono e si utilizzano i registri di query nell’interfaccia utente di Query Service.

Consulta la sezione [Panoramica dell’interfaccia utente](./overview.md)o [Guida all’API del servizio query](../api/getting-started.md) per ulteriori informazioni sulle funzionalità di Query Service.

Consulta la sezione [documento di monitoraggio delle query](./monitor-queries.md) per scoprire in che modo Query Service migliora la visibilità delle esecuzioni di query pianificate.
