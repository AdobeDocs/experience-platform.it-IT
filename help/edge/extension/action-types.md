---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch.
solution: Experience Platform
feature: SDK per web
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 27b26605cd03ff6d83a9a5bd308e55fcdc955da6
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---

# Tipi di azioni

Dopo aver configurato l&#39; [estensione Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) per [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configura i tipi di azione.

In questa pagina sono descritti i tipi di azioni disponibili.

## Invia evento

Invia un evento ad Adobe [!DNL Experience Platform] in modo che Adobe Experience Platform possa raccogliere i dati inviati e agire in base a tali informazioni. Seleziona un&#39;istanza (se ne hai più di una). Tutti i dati che desideri inviare possono essere inviati nel campo **[!UICONTROL Dati XDM]** . Utilizza un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla pagina o tramite un **[!UICONTROL Codice personalizzato]** **[!UICONTROL Elemento dati]**.

Ci sono alcuni altri campi nel tipo di azione Invia evento che potrebbero essere utili anche a seconda dell&#39;implementazione. Tieni presente che questi campi sono tutti facoltativi.

- **Tipo:** questo campo consente di specificare un tipo di evento che verrà registrato nello schema XDM. Per ulteriori informazioni sui tipi di evento predefiniti, consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) .
- **ID unione:** se desideri specificare un  [ID unione ](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) per l’evento, puoi farlo in questo campo. Tieni presente che le soluzioni a valle non sono in grado di unire i dati dell’evento in questo momento.
- **ID set di dati:** se devi inviare dati a un set di dati diverso da quello specificato nel tuo datastream, puoi specificarlo qui.
- **Il documento verrà scaricato:** se desideri che gli eventi raggiungano il server anche se l’utente si allontana dalla pagina, seleziona la casella di controllo  **[!UICONTROL Documento]** che verrà scaricata. Questo consente agli eventi di raggiungere il server ma le risposte vengono ignorate.
- **Decisioni relative alla personalizzazione visiva del rendering:** se desideri eseguire il rendering di contenuti personalizzati sulla pagina, seleziona la casella di controllo  **[!UICONTROL Rendering visual personalization]** decisionScript. Se necessario, puoi anche specificare gli ambiti decisionali. Per ulteriori informazioni sul rendering di contenuti personalizzati, consulta la [documentazione sulla personalizzazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) .

## Imposta consenso

Dopo aver ricevuto il consenso dall’utente, questo deve essere comunicato all’SDK Web di Adobe Experience Platform utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Consulta [Preferenze di supporto del consenso dei clienti](../consent/supporting-consent.md). Quando si utilizza la versione 2.0 di Adobe, è supportato solo un valore di elemento dati. Sarà necessario creare un elemento dati che si risolva nell’oggetto di consenso.

In questa azione, ti viene anche fornito un campo facoltativo per includere una mappa di identità in modo che le identità possano essere sincronizzate una volta ricevuto il consenso. La sincronizzazione è utile quando il consenso è configurato come &quot;In sospeso&quot; o &quot;Fuori&quot; perché è probabile che la chiamata di consenso sia la prima chiamata da attivare.

## Ripristina ID unione evento

Se desideri reimpostare l’ID unione eventi sulla pagina, puoi farlo con questa azione. Per reimpostare l’ID, seleziona l’ID unione da reimpostare e attiva l’azione in base alle esigenze.

## Cosa succede ora

Dopo aver impostato le azioni, [configura i tipi di elementi dati](data-element-types.md).
