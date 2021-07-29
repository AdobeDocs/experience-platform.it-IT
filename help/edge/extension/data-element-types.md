---
title: Tipi di elementi dati nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di elementi dati forniti dall’estensione tag Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 49%

---

# Tipi di elementi dati

Dopo aver impostato i [tipi di azione](action-types.md) nell&#39; [estensione tag Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), configura i tipi di elementi dati.

Questa pagina descrive i tipi di elementi dati disponibili.

## ID unione evento

Quando viene utilizzato, questo elemento dati fornisce un ID unione evento. Per questo elemento dati non è necessaria alcuna configurazione. L&#39;elemento dati fornito rimane lo stesso finché il visitatore non esce dalla pagina o finché non viene utilizzato il tipo di azione &quot;Ripristina ID unione evento&quot;.

## Mappa delle identità

L&#39;elemento dati Mappa delle identità consente di creare identità da altri elementi dati o altri valori specificati. Tutte le identità create devono essere legate a uno spazio nomi corrispondente. Questo elemento dati fornisce un elenco a discesa che mostra tutti i namespace predefiniti e quelli creati.

![](./assets/identity-map-data-element.png)

## Oggetto XDM {#xdm-object}

Usa il formato XDM per inviare qualsiasi dato all&#39;SDK Web di Adobe Experience Platform. La formattazione dei dati è più semplice con l&#39;elemento dati dell&#39;oggetto XDM. La prima volta che apri questo elemento dati, seleziona la sandbox e lo schema di Adobe Experience Platform corretti. Dopo aver selezionato lo schema, viene visualizzata la struttura dello schema, che è possibile compilare facilmente.

![](./assets/XDM-object.png)

Tieni presente che quando apri alcuni campi dello schema, ad esempio `web.webPageDetails.URL`, alcuni elementi vengono raccolti automaticamente. Anche se vengono raccolti automaticamente diversi elementi, puoi sovrascriverli, se necessario. Tutti i valori possono essere compilati manualmente o utilizzando altri elementi dati.

>[!NOTE]
>
>Riempi solo le informazioni che ti interessano. Tutto ciò che non viene compilato viene omesso quando i dati vengono inviati alle soluzioni.
