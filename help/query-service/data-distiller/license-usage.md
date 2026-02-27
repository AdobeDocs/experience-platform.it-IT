---
title: Monitorare l’utilizzo delle licenze per query batch
description: L’interfaccia utente di Adobe Experience Platform fornisce una dashboard tramite la quale puoi visualizzare informazioni importanti sull’utilizzo delle licenze di Data Distiller da parte della tua organizzazione.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: dce631923bd38f3237da3e1928e2203dc1a266ca
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Monitorare l’utilizzo delle licenze per query batch {#monitor-license-usage}

Il dashboard utilizzo licenze fornisce report granulari sull’utilizzo delle licenze di Query Service e sulle metriche di utilizzo per ogni prodotto acquistato. Per ulteriori informazioni sulle metriche disponibili visualizzate nel dashboard, visita la [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#available-metrics).

Il dashboard fornisce le metriche di utilizzo per ciascun prodotto acquistato, l’utilizzo consolidato delle metriche in tutte le sandbox di produzione o di sviluppo e le metriche di utilizzo da una sandbox specifica. Le informazioni visualizzate qui vengono acquisite durante un’istantanea giornaliera dell’istanza Experience Platform. Gli amministratori possono monitorare e terminare le sessioni inattive di Query Service per liberare capacità quando non sono disponibili sessioni aggiuntive e gli utenti sono bloccati a causa di sessioni inattive (non attive). Per informazioni dettagliate, consulta [Gestire le sessioni di Query Service](../ui/session-management.md).

>[!NOTE]
>
>Per impostazione predefinita, il dashboard utilizzo licenze non è attivato. Per poter visualizzare la dashboard, gli utenti devono disporre dell’autorizzazione &quot;Visualizza dashboard utilizzo licenze&quot;. Per i passaggi relativi alla concessione delle autorizzazioni di accesso per la visualizzazione del dashboard di utilizzo delle licenze, fare riferimento alla [guida alle autorizzazioni del dashboard](../../dashboards/permissions.md).

## Calcola ore {#compute-hours}

La metrica [!UICONTROL Compute hours] è applicabile solo ai clienti con la licenza Data Distiller per le query batch. [!UICONTROL Compute hours] sono la misura del tempo impiegato dai motori di Query Service per leggere, elaborare e riscrivere i dati nel data lake quando viene eseguita una query batch.

![Dashboard di utilizzo della licenza con la metrica delle ore di calcolo evidenziata.](../images/data-distiller/compute-hours.png)

Per ulteriori informazioni sulle metriche disponibili per la tua organizzazione in base alla licenza acquistata della tua organizzazione, consulta la [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md).
