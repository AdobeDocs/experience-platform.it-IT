---
title: Monitorare l’utilizzo delle licenze per query batch
description: L’interfaccia utente di Adobe Experience Platform fornisce una dashboard tramite la quale puoi visualizzare informazioni importanti sull’utilizzo delle licenze di Data Distiller da parte della tua organizzazione.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
hide: true
hidefromtoc: true
recommendations: noCatalog, display
source-git-commit: fa573dcf03eb711e946afe40d107871f5166ff58
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# (Alfa) Monitorare l’utilizzo delle licenze per query batch {#monitor-license-usage}

>[!IMPORTANT]
>
>La possibilità di monitorare l’utilizzo delle licenze per query batch tramite l’interfaccia utente non è ancora disponibile per tutti gli utenti. Questa funzione è in formato alfa ed è ancora in fase di test. Questo documento è soggetto a modifiche.

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard tramite la quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze di Query Service da parte dell’organizzazione.

Per istruzioni dettagliate su come accedere e interagire con la dashboard Utilizzo licenze nell’interfaccia utente, nonché per ulteriori informazioni sulle metriche disponibili visualizzate nella dashboard, visita [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md).

Leggi le [panoramica delle dashboard](../../dashboards/home.md) per un riepilogo di tutte le funzionalità del dashboard in Experience Platform.

## Widget {#widgets}

Il dashboard utilizzo licenze è composto da widget che visualizzano metriche di sola lettura contenenti informazioni importanti sull’utilizzo delle licenze da parte dell’organizzazione. Le metriche visibili dipendono dalle licenze specifiche della tua organizzazione.

Seleziona un pulsante di scelta per scegliere una sandbox per l’analisi e utilizza il menu a discesa per selezionare un periodo di tempo per l’analisi. Le opzioni disponibili sono un periodo di 30 giorni, 90 giorni, 12 mesi, l’ultimo anno, l’intero periodo contrattuale o una data personalizzata.

## Calcola ore {#compute-hours}

Il [!UICONTROL Calcola ore] il widget utilizza un grafico a linee per visualizzare ogni giorno il tempo di elaborazione delle query batch dell’organizzazione. Il widget mostra tre metriche indicate da un numero in alto a sinistra. Sono

- [!UICONTROL Effettivo]: numero totale di ore di calcolo per il periodo di tempo scelto nel menu a discesa Panoramica. Questa metrica è indicata anche nel grafico da una linea continua.
- [!UICONTROL Concesso in licenza]: il numero totale di ore di calcolo consentite dal contratto di licenza della tua organizzazione. Anche questa metrica è indicata sul grafico da una linea tratteggiata.
- [!UICONTROL Utilizzo]: questa è la percentuale di utilizzo relativa al numero massimo di ore di calcolo concordato dalla licenza.

>[!IMPORTANT]
>
>Il [!UICONTROL Calcola ore] Il widget è applicabile solo ai clienti con la licenza Data Distiller per le query batch.

![Dashboard di utilizzo della licenza con widget ore di calcolo evidenziato.](../images/data-distiller/compute-hours.png)

