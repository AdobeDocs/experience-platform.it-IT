---
title: Gestione della duplicazione degli eventi in Experience Platform
description: Scopri come Adobe Experience Platform gestisce la duplicazione degli eventi
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Gestione della duplicazione degli eventi in Adobe Experience Platform

Adobe Experience Platform è un sistema altamente distribuito progettato per massimizzare l&#39;affidabilità e al tempo stesso scalare volumi di dati in continua crescita.

Per la raccolta dati in tempo reale, [Eventi esperienza](../xdm/classes/experienceevent.md) vengono raccolti tramite [Edge Network](../web-sdk/home.md#edge-network) da origini lato client, ad esempio [Web SDK](../web-sdk/home.md) o [Mobile SDK](https://developer.adobe.com/client-sdks/home/), e consegnati ai livelli di elaborazione e archiviazione Experience Platform. Questi livelli compongono soluzioni quali Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it).

Per ridurre al minimo la perdita di eventi esperienza, gli SDK lato client e il servizio di consegna degli Experienci Platform interni si aspettano una conferma della corretta raccolta di un evento.

Se tale conferma non viene ricevuta, gli SDK lato client o il servizio di distribuzione interno di Platform attivano un nuovo tentativo e l’evento esperienza viene inviato di nuovo.

Si tratta di una best practice per la gestione di errori transitori. L’effetto collaterale è la possibilità di introdurre eventi duplicati.

Per comprendere meglio le best practice per la gestione degli errori transitori, vedere questo articolo su [gestione degli errori transitori](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Scenari di duplicazione degli eventi {#scenarios}

La duplicazione degli eventi può verificarsi in vari scenari, ad esempio, ma non solo:

* Problemi relativi alla rete tra gli SDK lato client e [!DNL Edge Network]. Questi problemi possono essere dovuti a guasti del provider di servizi Internet, perdita del segnale mobile o altri errori di rete, poiché la connettività tra il cliente e l’Edge Network avviene tramite Internet pubblica.
* Eventi di ridimensionamento automatico di Experience Platform interno. Talvolta, i dati possono essere riequilibrati a causa della volatilità dell’infrastruttura cloud.

Il livello di raccolta dati di Adobe Experience Platform è progettato per supportare l’elaborazione &quot;almeno una volta&quot;. Di conseguenza, la duplicazione degli eventi può verificarsi in situazioni rare e limitate.

Per ulteriori informazioni sull&#39;elaborazione &quot;almeno una volta&quot;, consulta questo articolo sulle [garanzie di consegna messaggi](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opzioni di deduplicazione degli eventi {#deduplication}

Per gli scenari aziendali sensibili agli eventi duplicati, Experience Platform utilizza più metodi di deduplicazione degli eventi nei propri sistemi di storage a valle, come quelli descritti di seguito.

* L&#39;archivio profili di Real-Time CDP rilascia gli eventi se un evento con lo stesso `_id` esiste già in [!DNL Profile store]. Per ulteriori dettagli, consulta la documentazione sulla classe [XDM ExperienceEvent](../xdm/classes/experienceevent.md).
* Il Customer Journey Analytics consente agli utenti di configurare una metrica per contare solo i valori in modo non ripetitivo. Per ulteriori informazioni, consulta la documentazione sulle [impostazioni dei componenti di deduplicazione metrica](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=it).
* Experience Platform Query Service supporta la deduplicazione dei dati quando è necessario rimuovere un’intera riga da un calcolo o ignorare un set specifico di campi, perché solo una parte dei dati nella riga sono informazioni duplicate. Per ulteriori informazioni, consulta la documentazione sulla [deduplicazione dei dati in Query Service](../query-service/key-concepts/deduplication.md).

>[!NOTE]
>
>Se riscontri problemi di duplicazione degli eventi al di fuori dei casi d’uso descritti in precedenza, contatta il rappresentante del tuo Adobe e fornisci informazioni dettagliate sul caso d’uso.
