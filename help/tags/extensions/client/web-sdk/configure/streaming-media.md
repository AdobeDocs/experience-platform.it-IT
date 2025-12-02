---
title: Impostazioni di configurazione di Streaming Media
description: Personalizza il modo in cui l’estensione tag Web SDK raccoglie i dati multimediali in streaming.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---

# Impostazioni di configurazione di Streaming Media

La funzione di raccolta multimediale consente di raccogliere i dati relativi alle sessioni multimediali, ad esempio riproduzioni, pause, completamenti e altri eventi correlati. Una volta raccolti, puoi inviare questi dati a Adobe Experience Platform o Adobe Analytics per generare rapporti. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Streaming media]**.

![Immagine che mostra le impostazioni della raccolta multimediale dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag](../assets/media-collection.png)

## Prerequisiti

Per utilizzare il componente Streaming Media del Web SDK, è necessario soddisfare i seguenti prerequisiti:

* Assicurati di avere accesso a Adobe Experience Platform o Adobe Analytics.
* Abilitare l&#39;opzione **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** per lo stream di dati in uso.
* Assicurati che lo schema utilizzato dallo stream di dati includa i campi dello schema di Media Collection.
* Configura la funzione Streaming Media nell’estensione tag Web SDK, come illustrato in questa pagina.

## [!UICONTROL Channel]

Nome del canale in cui si verifica la raccolta multimediale. Ad esempio, `Video channel`. Qualsiasi valore stringa è valido.

## [!UICONTROL Player Name]

Nome del lettore multimediale utilizzato dalla proprietà per la riproduzione multimediale.

## [!UICONTROL Application Version]

Versione dell’applicazione lettore multimediale utilizzata dalla proprietà per la riproduzione di contenuti multimediali.

## [!UICONTROL Main ping interval]

Frequenza dei ping per il contenuto principale, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `10` e `50` secondi. Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizzano [sessioni con tracciamento automatico](/help/collection/js/commands/createmediasession.md#automatic).

## [!UICONTROL Ad ping interval]

Frequenza dei ping per il contenuto dell’annuncio, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `1` e `10` secondi. Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizzano [sessioni con tracciamento automatico](/help/collection/js/commands/createmediasession.md#automatic).
