---
title: Tipi di elementi di dati nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di elementi dati forniti dall’estensione Adobe Experience Platform Web SDK in  Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 78%

---


# Tipi di elementi dati

Dopo aver impostato i [tipi di azione](action-types.md) nell&#39; [estensione Adobe Experience Platform Web SDK](web-sdk-extension.md) per [ Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configura i tipi di elemento dati.

Questa pagina descrive i tipi di elementi dati disponibili.

## ID unione evento

Quando viene utilizzato, questo elemento dati fornisce un ID unione evento. Per questo elemento dati non è necessaria alcuna configurazione. L&#39;elemento dati fornito rimane lo stesso finché il visitatore non esce dalla pagina o finché non viene utilizzato il tipo di azione &quot;Ripristina ID unione evento&quot;.

## Mappa delle identità

L&#39;elemento dati Mappa delle identità consente di creare identità da altri elementi dati o altri valori specificati. Tutte le identità create devono essere legate a uno spazio nomi corrispondente. Questo elemento dati fornisce un elenco a discesa che mostra tutti gli spazi dei nomi predefiniti, oltre a quelli creati dall&#39;utente.

![](./assets/identity-map-data-element.png)

## Oggetto XDM

I dati inviati ad Adobe Experience Platform Web SDK devono essere in formato XDM. La formattazione dei dati è più semplice con l&#39;elemento dati dell&#39;oggetto XDM. La prima volta che apri questo elemento dati, seleziona la sandbox e lo schema di Adobe Experience Platform corretti. Dopo aver selezionato lo schema, ne verrà visualizzata la struttura che potrai compilare senza difficoltà.

![](./assets/XDM-object.png)

Tieni presente che quando apri alcuni campi dello schema, ad esempio `web.webPageDetails.URL`, alcuni elementi vengono raccolti automaticamente. Anche se diversi elementi vengono raccolti automaticamente, se necessario, puoi sovrascriverne alcuni. Tutti i valori possono essere compilati manualmente o utilizzando altri elementi dati.

>[!NOTE]
>
>Devi solo compilare le informazioni che sei interessato a raccogliere. Tutto ciò che non viene compilato verrà omesso quando i dati vengono inviati alle soluzioni.
