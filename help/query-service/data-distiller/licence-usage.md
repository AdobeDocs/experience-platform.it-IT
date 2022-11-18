---
title: Monitoraggio utilizzo licenza query batch
description: L’interfaccia utente di Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sull’utilizzo della licenza di Data Distiller dell’organizzazione.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: 9d543b5c7c7f39e809b6a13b8adc46b9a99f51c7
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# (Beta) Monitora l&#39;utilizzo della licenza di query batch {#monitor-license-usage}

>[!IMPORTANT]
>
>La possibilità di monitorare l’utilizzo della licenza di query batch tramite l’interfaccia utente è in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche.

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sull’utilizzo della licenza di Query Service della propria organizzazione.

Per istruzioni dettagliate su come accedere e interagire con il dashboard dell’utilizzo delle licenze nell’interfaccia utente e per ulteriori informazioni sulle metriche disponibili visualizzate nel dashboard, visita il [guida all&#39;utilizzo della licenza](../../dashboards/guides/license-usage.md).

Per piacere, leggi le [panoramica delle dashboard](../../dashboards/home.md) per un riepilogo di tutte le funzioni del dashboard in Experience Platform.

## Widget {#widgets}

Il dashboard per l&#39;utilizzo delle licenze è composto da widget che visualizzano metriche di sola lettura che forniscono informazioni importanti sull&#39;utilizzo delle licenze dell&#39;organizzazione. Le metriche visibili dipendono dalle licenze specifiche della tua organizzazione.

Seleziona un pulsante di scelta per scegliere una sandbox da analizzare e utilizza il menu a discesa per selezionare un periodo di tempo per l’analisi. Le opzioni disponibili sono un periodo di 30 giorni, 90 giorni, 12 mesi, l’ultimo anno, l’intero periodo di contratto o una data personalizzata.

## Orari di calcolo {#compute-hours}

La [!UICONTROL Orari di calcolo] widget utilizza un grafico a linee per visualizzare ogni giorno il tempo di elaborazione delle query batch dell&#39;organizzazione. Il widget visualizza tre metriche indicate da un numero in alto a sinistra nel widget. Sono

- [!UICONTROL Effettivo]: Numero totale di ore di calcolo per il periodo di tempo scelto nel menu a discesa della panoramica. Questa metrica è indicata anche sul grafico da una linea continua.
- [!UICONTROL Concesso in licenza]: Numero totale di ore di calcolo consentite dal contratto di licenza dell&#39;organizzazione. Questa metrica è indicata anche sul grafico da una linea tratteggiata.
- [!UICONTROL Utilizzo]: Questa è la percentuale dell&#39;utilizzo rispetto alle ore di calcolo massime concordate dalla licenza.

>[!IMPORTANT]
>
>La [!UICONTROL Orari di calcolo] widget è applicabile solo ai clienti con la licenza Data Distiller per le query batch.

![Dashboard di utilizzo della licenza con il widget ore di calcolo evidenziato.](../images/data-distiller/compute-hours.png)
