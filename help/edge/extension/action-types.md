---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 33%

---


# Tipi di azioni

Dopo aver configurato l&#39; [estensione Adobe Experience Platform Web SDK](web-sdk-extension.md) per [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configura i tipi di azione.

In questa pagina sono descritti i tipi di azioni disponibili.

## Invia evento

Invia un evento ad Adobe [!DNL Experience Platform] in modo che Adobe Experience Platform possa raccogliere i dati inviati e intervenire su tali informazioni. Seleziona un&#39;istanza (se ne hai più di una). Se l&#39;evento si verifica all&#39;inizio del caricamento di una pagina o durante una modifica della visualizzazione in un&#39;applicazione a pagina singola, seleziona **[!UICONTROL Occurs at the start of a view]**.

Tutti i dati che vuoi inviare possono essere inviati nel campo **[!UICONTROL XDM Data]**. Utilizza un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla pagina o attraverso un **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Imposta consenso

Dopo aver ricevuto il consenso dall’utente, questo deve essere comunicato all’SDK web di Adobe Experience Platform utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Se utilizzi il consenso standard di Adobe, al momento è possibile impostarlo come &quot;In&quot;, &quot;Out&quot; oppure puoi farlo utilizzando un elemento dati. Se utilizzi il consenso standard IAB TCF, fornisci la versione e il valore che desideri utilizzare, nonché le informazioni aggiuntive relative al RGPD (Regolamento generale sulla protezione dei dati).

In questa azione, ti viene anche fornito un campo facoltativo per includere una mappa di identità in modo che le identità possano essere sincronizzate una volta ricevuto il consenso. La sincronizzazione è utile quando il consenso è configurato come &quot;In sospeso&quot; perché la chiamata di consenso è probabilmente la prima chiamata da attivare.

## Ripristina ID unione evento

Se desideri reimpostare l’ID unione eventi sulla pagina, puoi farlo con questa azione. Per reimpostare l’ID, seleziona l’ID unione da reimpostare e attiva l’azione in base alle esigenze.

## Ulteriori informazioni

Dopo aver impostato i tipi di azione, [configura i tipi di elementi dati](data-element-types.md).