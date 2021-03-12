---
keywords: Experience Platform;interfaccia utente;interfaccia utente;personalizzazione;dashboard utilizzo licenza;dashboard;utilizzo licenza;adesione;consumo
title: Dashboard di utilizzo della licenza
description: Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze dell’organizzazione.
topic: guida
type: Documentazione
translation-type: tm+mt
source-git-commit: 3908011b31dd24b13a58a2bc5ad5137dd3af5f63
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 3%

---


# (Beta) Dashboard di utilizzo della licenza {#license-usage-dashboard}

>[!IMPORTANT]
>
>La funzionalità del dashboard descritta in questo documento è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze dell’organizzazione, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e utilizzare il dashboard per l’utilizzo delle licenze nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica generale dell’interfaccia utente di Platform, visita la [guida all’interfaccia utente di Experience Platform](../../landing/ui-guide.md).

## Dati del dashboard per l’utilizzo della licenza

Nel dashboard sull’utilizzo delle licenze viene visualizzata un’istantanea dei dati relativi alle licenze dell’organizzazione, ad Experience Platform. I dati nel dashboard vengono visualizzati esattamente come vengono visualizzati nel momento specifico in cui è stata scattata l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard di utilizzo della licenza

Per passare al dashboard dell’utilizzo della licenza nell’interfaccia utente di Platform, seleziona **[!UICONTROL License usage]** nella barra a sinistra. Viene visualizzata la scheda **[!UICONTROL Overview]** che mostra il dashboard.

![](../images/license-usage/dashboard-overview.png)

### Selezionare una sandbox

Per scegliere una sandbox da visualizzare nel dashboard, selezionare [!UICONTROL Production] o [!UICONTROL Development]. La sandbox selezionata è indicata dal pulsante di scelta accanto al nome della sandbox.

>[!NOTE]
>
>La generazione di rapporti sui consumi per le sandbox è cumulativa per tutte le sandbox dello stesso tipo. In altre parole, selezionando [!UICONTROL Production] o [!UICONTROL Development] vengono forniti rapporti di consumo per tutte le sandbox di produzione o di sviluppo, rispettivamente.

![](../images/license-usage/select-sandbox.png)

### Selezionare un intervallo di date

Dopo aver selezionato una sandbox, puoi utilizzare il menu a discesa dell’intervallo di date per selezionare il periodo di tempo da visualizzare nel dashboard. Sono disponibili tre opzioni: [!UICONTROL Last 30 days], [!UICONTROL Last 90 days] e [!UICONTROL Last 12 months]. Per impostazione predefinita, sono selezionati gli ultimi 30 giorni.

![](../images/license-usage/select-date-range.png)

## Widget

Il dashboard per l&#39;utilizzo delle licenze è composto da widget che visualizzano metriche di sola lettura che forniscono informazioni importanti sull&#39;utilizzo delle licenze dell&#39;organizzazione. Le metriche visibili dipendono dalle licenze specifiche della tua organizzazione (consulta la sezione [metriche disponibili](#available-metrics) per i dettagli).

Ogni widget visualizza un grafico a linee che confronta i numeri effettivi per la tua organizzazione con il totale disponibile con le licenze della tua organizzazione e fornisce una percentuale dell&#39;utilizzo totale.

![](../images/license-usage/widgets.png)

## Metriche disponibili

Sono attualmente disponibili quattro metriche nel dashboard di utilizzo della licenza:

* [!UICONTROL Addressable Audience] (misurato in numero di profili)
* [!UICONTROL Average profile richness]
* [!UICONTROL Total consumed storage]
* [!UICONTROL Data scanned per segmentation ratio]

La definizione di ciascuna di queste metriche varia a seconda della licenza acquistata dalla tua organizzazione. Per le definizioni dettagliate di ciascuna metrica, fare riferimento alla documentazione appropriata relativa alla descrizione del prodotto:

| Licenza | Descrizione del prodotto |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:BUONA PESANTE</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>PIATTAFORMA DATI CLIENTE RT:OD</li><li>PIATTAFORMA DATI DEL CLIENTE RT:BUON PRFL A 10M</li><li>PIATTAFORMA DATI DEL CLIENTE RT:DA BUON PRFL A 50M</li></ul> | [Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>AEP:BUONA ATTIVAZIONE</li><li>AEP:BUONA ATTIVAZIONE PRFL A 10M</li><li>AEP:BUONA ATTIVAZIONE PRFL FINO A 50 M</li></ul> | [Attivazione Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## Passaggi successivi

Dopo aver letto questo documento, è possibile individuare il dashboard di utilizzo della licenza e selezionare una sandbox da visualizzare. Puoi anche trovare ulteriori informazioni sulle metriche disponibili per la tua organizzazione, in base alla licenza acquistata dalla tua organizzazione.

Per ulteriori informazioni sulle altre funzioni disponibili nell’interfaccia utente di Experience Platform, consulta la [Guida all’interfaccia utente della piattaforma](../../landing/ui-guide.md) .