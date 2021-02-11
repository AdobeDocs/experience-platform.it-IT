---
title: Tipi di azioni di estensione SDK per Web piattaforma
description: 'Adobe Experience Platform Web SDK Extension Action Types in Adobe Experience Platform Launch '
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 70%

---


# Tipi di azioni

Dopo aver configurato l&#39;estensione [Adobe Experience Platform Web SDK](web-sdk-extension.md) per [ Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configura i tipi di azione.

Questa pagina descrive i tipi di azioni disponibili.

## Invia evento

Invia un evento  Adobe [!DNL Experience Platform] in modo che Adobe Experience Platform possa raccogliere i dati inviati e agire in base a tali informazioni. Seleziona un&#39;istanza (se ne esiste più di una). Se l&#39;evento si verifica all&#39;inizio del caricamento di una pagina o durante una modifica della visualizzazione in un&#39;applicazione a pagina singola, seleziona **[!UICONTROL Occurs at the start of a view]**.

Tutti i dati che vuoi inviare possono essere inviati nel campo **[!UICONTROL XDM Data]**. Deve essere un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla pagina o attraverso un **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Imposta consenso

Dopo aver ricevuto il consenso dall&#39;utente, questo deve essere comunicato all&#39;SDK Web di Adobe Experience Platform. Puoi farlo utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Se utilizzi il consenso standard di Adobe, al momento è possibile impostarlo come &quot;In&quot;, &quot;Out&quot; oppure puoi farlo utilizzando un elemento dati. Se utilizzi il consenso standard IAB TCF, fornisci la versione e il valore che desideri utilizzare, nonché le informazioni aggiuntive relative al RGPD (Regolamento generale sulla protezione dei dati).

In questa azione ti viene fornito anche un campo facoltativo per includere una Mappa di identità in modo che, una volta ricevuto il consenso, le identità possano essere sincronizzate. Questo può essere utile quando il consenso è configurato come &quot;In sospeso&quot;, perché la chiamata relativa al consenso sarà probabilmente la prima chiamata da attivare.

## Ripristina ID unione evento

Se desideri ripristinare l&#39;ID unione evento sulla pagina, è possibile farlo con questa azione. Per ripristinarla, seleziona l&#39;ID unione da reimpostare e attiva l&#39;azione come necessario.

## Ulteriori informazioni

Dopo aver impostato i tipi di azione, [configurare i tipi di elemento dati](data-element-types.md).