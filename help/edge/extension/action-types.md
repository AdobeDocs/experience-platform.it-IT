---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 20%

---


# Tipi di azioni

Dopo aver configurato l&#39; [estensione Adobe Experience Platform Web SDK](web-sdk-extension.md) per [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configura i tipi di azione.

In questa pagina sono descritti i tipi di azioni disponibili.

## Invia evento

Invia un evento ad Adobe [!DNL Experience Platform] in modo che Adobe Experience Platform possa raccogliere i dati inviati e agire in base a tali informazioni. Seleziona un&#39;istanza (se ne hai più di una). Se l&#39;evento si verifica all&#39;inizio del caricamento di una pagina o durante una modifica della visualizzazione in un&#39;applicazione a pagina singola, seleziona **[!UICONTROL Occurs at the start of a view]**.

Tutti i dati che vuoi inviare possono essere inviati nel campo **[!UICONTROL XDM Data]**. Utilizza un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla pagina o attraverso un **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Imposta consenso

Dopo aver ricevuto il consenso dall’utente, questo deve essere comunicato all’SDK Web di Adobe Experience Platform utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Consulta [Preferenze di supporto del consenso dei clienti](../consent/supporting-consent.md). Quando si utilizza la versione 2.0 di Adobe, è supportato solo un valore di elemento dati. Sarà necessario creare un elemento dati che si risolva nell’oggetto di consenso.

In questa azione, ti viene anche fornito un campo facoltativo per includere una mappa di identità in modo che le identità possano essere sincronizzate una volta ricevuto il consenso. La sincronizzazione è utile quando il consenso è configurato come &quot;In sospeso&quot; o &quot;Fuori&quot; perché è probabile che la chiamata di consenso sia la prima chiamata da attivare.

## Ripristina ID unione evento

Se desideri reimpostare l’ID unione eventi sulla pagina, puoi farlo con questa azione. Per reimpostare l’ID, seleziona l’ID unione da reimpostare e attiva l’azione in base alle esigenze.

## Ulteriori informazioni

Dopo aver impostato i tipi di azione, [configura i tipi di elementi dati](data-element-types.md).