---
title: Monitorare l’utilizzo delle licenze per query batch
description: L’interfaccia utente di Adobe Experience Platform fornisce una dashboard tramite la quale puoi visualizzare informazioni importanti sull’utilizzo delle licenze di Data Distiller da parte della tua organizzazione.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
recommendations: noCatalog, display
source-git-commit: e55cada0975d771f225e829aeeeeeeb64b9acf4a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Monitorare l’utilizzo delle licenze per query batch {#monitor-license-usage}

Il dashboard utilizzo licenze fornisce report granulari sull’utilizzo delle licenze di Query Service e sulle metriche di utilizzo per ogni prodotto acquistato. Per ulteriori informazioni sulle metriche disponibili visualizzate nel dashboard, visita il [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#available-metrics).

Il dashboard fornisce le metriche di utilizzo per ciascun prodotto acquistato, l’utilizzo consolidato delle metriche in tutte le sandbox di produzione o di sviluppo e le metriche di utilizzo da una sandbox specifica. Le informazioni visualizzate qui vengono acquisite durante un’istantanea giornaliera dell’istanza Platform.

>[!NOTE]
>
>Per impostazione predefinita, il dashboard utilizzo licenze non è attivato. Per poter visualizzare la dashboard, gli utenti devono disporre dell’autorizzazione &quot;Visualizza dashboard utilizzo licenze&quot;. Per i passaggi sulla concessione delle autorizzazioni di accesso per la visualizzazione del dashboard utilizzo licenze, consulta [guida alle autorizzazioni della dashboard](../../dashboards/permissions.md).

## Calcola ore {#compute-hours}

Il [!UICONTROL Calcola ore] La metrica è applicabile solo ai clienti con la licenza Data Distiller per le query batch. [!UICONTROL Calcola ore] sono la misura del tempo impiegato dai motori di Query Service per leggere, elaborare e riscrivere i dati nel data lake quando viene eseguita una query batch.

>[!NOTE]
>
>**I dati sono disponibili con limitazioni**: i dati iniziano dal 1° ottobre 2023 senza tendenze.<br>Il **retrocompilazione** dei dati dalla data di inizio del contratto è un work-in-progress. La sua disponibilità è prevista entro la fine dell&#39;anno civile.

![Dashboard di utilizzo della licenza con la metrica ore di calcolo evidenziata.](../images/data-distiller/compute-hours.png)

Per ulteriori informazioni sulle metriche disponibili per l’organizzazione in base alla licenza acquistata, consulta [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md).
