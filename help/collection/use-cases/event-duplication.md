---
title: Gestione della duplicazione degli eventi in Experience Platform
description: Scopri come Adobe Experience Platform gestisce la duplicazione degli eventi
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Gestione della duplicazione degli eventi in Adobe Experience Platform

Adobe Experience Platform è un sistema altamente distribuito progettato per massimizzare l&#39;affidabilità e al tempo stesso scalare volumi di dati in continua crescita.

Per la raccolta dati in tempo reale, [Eventi esperienza](/help/xdm/classes/experienceevent.md) vengono raccolti tramite Edge Network, da origini lato client, come Web SDK o [Mobile SDK](https://developer.adobe.com/client-sdks/home/), e consegnati ai livelli di elaborazione e archiviazione di Experience Platform. Questi livelli compongono soluzioni quali Experience Platform, [Real-Time CDP](/help/rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it).

Per ridurre al minimo la perdita di eventi di esperienza, gli SDK lato client e il servizio di consegna interno di Experience Platform prevedono una conferma della corretta raccolta di un evento.

Se tale conferma non viene ricevuta, gli SDK lato client o il servizio di consegna interno di Experience Platform attivano un nuovo tentativo e l’evento esperienza viene inviato di nuovo.

Si tratta di una best practice per la gestione di errori transitori. L’effetto collaterale è la possibilità di introdurre eventi duplicati.

Per comprendere meglio le best practice per la gestione degli errori transitori, vedere questo articolo su [gestione degli errori transitori](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Scenari di duplicazione degli eventi {#scenarios}

La duplicazione degli eventi può verificarsi in vari scenari, ad esempio, ma non solo:

* Problemi relativi alla rete tra gli SDK lato client e [!DNL Edge Network]. Questi problemi possono essere dovuti a errori del provider di servizi Internet, perdita di segnale mobile o altri errori di rete, poiché la connettività tra il cliente e Edge Network viene eseguita tramite Internet pubblica.
* Eventi di ridimensionamento automatico interni di Experience Platform. Talvolta, i dati possono essere riequilibrati a causa della volatilità dell’infrastruttura cloud.

Il livello di raccolta dati di Adobe Experience Platform è progettato per supportare l’elaborazione &quot;almeno una volta&quot;. Di conseguenza, la duplicazione degli eventi può verificarsi in situazioni rare e limitate.

Per ulteriori informazioni sull&#39;elaborazione &quot;almeno una volta&quot;, consulta questo articolo sulle [garanzie di consegna messaggi](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opzioni di deduplicazione degli eventi {#deduplication}

Per gli scenari aziendali sensibili agli eventi duplicati, Experience Platform utilizza più metodi di deduplicazione degli eventi nei propri sistemi di storage a valle, come quelli descritti di seguito.

* L&#39;archivio profili di Real-Time CDP rilascia gli eventi se un evento con lo stesso `_id` esiste già in [!DNL Profile store]. Per ulteriori dettagli, consulta la documentazione sulla classe [XDM ExperienceEvent](/help/xdm/classes/experienceevent.md).
* Customer Journey Analytics consente agli utenti di configurare una metrica per contare solo i valori in modo non ripetitivo. Per ulteriori informazioni, consulta la documentazione sulle [impostazioni dei componenti di deduplicazione metrica](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=it).
* Experience Platform Query Service supporta la deduplicazione dei dati quando è necessario rimuovere un’intera riga da un calcolo o ignorare un set specifico di campi, perché solo una parte dei dati nella riga sono informazioni duplicate. Per ulteriori informazioni, consulta la documentazione sulla [deduplicazione dei dati in Query Service](/help/query-service/key-concepts/deduplication.md).

>[!NOTE]
>
>Se riscontri problemi di duplicazione degli eventi al di fuori dei casi d’uso descritti in precedenza, contatta il tuo rappresentante Adobe e fornisci informazioni dettagliate sul tuo caso d’uso.
