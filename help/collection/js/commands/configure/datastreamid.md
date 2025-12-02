---
title: datastreamId
description: Determina l’ID dello stream di dati a cui desideri inviare i dati.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# `datastreamId`

La proprietà `datastreamId` è una stringa che determina a quale [flusso di dati](/help/datastreams/overview.md) in Adobe Experience Platform desideri inviare i dati. Questa proprietà è obbligatoria per l’invio di dati ad Adobe. Le versioni 2.20.0 o precedenti di Web SDK utilizzano invece `edgeConfigId`.

Per individuare un ID dello stream di dati:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Utilizza il campo di ricerca per individuare lo stream di dati desiderato, quindi seleziona **[!UICONTROL Copy]** ![Copia](../../assets/copy.png) accanto all&#39;ID dello stream di dati.

In alternativa, puoi selezionare il nome dello stream di dati desiderato e l’ID dello stream di dati viene visualizzato nella colonna di destra per consentirne la copia.

## Esempio di codice

Impostare la proprietà stringa `datastreamID` durante l&#39;esecuzione del comando `configure`. Questa proprietà è obbligatoria per tutte le implementazioni di Web SDK. Se si omette questa proprietà, il SDK Web non sa a quale flusso di dati inviare i dati, causandone la perdita permanente.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Se si configurano più istanze del Web SDK in una singola pagina, è necessario configurare un `datastreamId` diverso per ogni istanza.

## Seleziona l’ID dello stream di dati utilizzando l’estensione tag Web SDK

Per informazioni su come impostare lo stream di dati desiderato per ogni ambiente che utilizza i tag, consulta le [impostazioni di configurazione dello stream di dati](/help/tags/extensions/client/web-sdk/configure/datastreams.md) nella documentazione dell&#39;estensione tag di Web SDK. Puoi inviare dati a diversi flussi di dati per ambienti di tag di produzione, staging e sviluppo.
