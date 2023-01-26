---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione tag Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 4%

---

# Tipi di azioni

Dopo aver configurato le [Estensione tag Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), configura i tipi di azione.

In questa pagina sono descritti i tipi di azioni disponibili.


## Invia evento

Invia un evento ad Adobe [!DNL Experience Platform] in modo che Adobe Experience Platform possa raccogliere i dati inviati e agire in base a tali informazioni. Seleziona un&#39;istanza (se ne hai più di una). Tutti i dati che desideri inviare possono essere inviati nel **[!UICONTROL Dati XDM]** campo . Utilizza un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla pagina o attraverso un **[!UICONTROL Codice personalizzato]** **[!UICONTROL Elemento dati]**.

Ci sono alcuni altri campi nel tipo di azione Invia evento che potrebbero essere utili anche a seconda dell&#39;implementazione. Tieni presente che questi campi sono tutti facoltativi.

- **Tipo:** Questo campo consente di specificare un tipo di evento da registrare nello schema XDM. Consulta la sezione [documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) per ulteriori informazioni sui tipi di evento predefiniti.
- **Dati:** I dati che non corrispondono a uno schema XDM possono essere inviati utilizzando questo campo. Questo campo è utile se cerchi di aggiornare un profilo Adobe Target o di inviare attributi Recommendations di Target. Per esempi consulta la nostra [documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID set di dati:** Se devi inviare dati a un set di dati diverso da quello specificato nel tuo datastream, puoi specificarlo qui.
- **Il documento verrà scaricato:** Se desideri assicurarti che gli eventi raggiungano il server anche se l’utente si allontana dalla pagina, controlla **[!UICONTROL Il documento verrà scaricato]** casella di controllo. Questo consente agli eventi di raggiungere il server ma le risposte vengono ignorate.
- **Decisioni relative alla personalizzazione visiva del rendering:** Se desideri eseguire il rendering di contenuti personalizzati sulla pagina, controlla la **[!UICONTROL Decisioni relative alla personalizzazione visiva del rendering]** casella di controllo. Se necessario, è inoltre possibile specificare ambiti decisionali e/o superfici. Consulta la sezione [documentazione sulla personalizzazione](../personalization/rendering-personalization-content.md#automatically-rendering-content) per ulteriori informazioni sul rendering di contenuti personalizzati.

## Imposta consenso

Dopo aver ricevuto il consenso dall’utente, questo deve essere comunicato all’SDK Web di Adobe Experience Platform utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Vedi [Preferenze di consenso del cliente](../consent/supporting-consent.md). Quando si utilizza la versione 2.0 di Adobe, è supportato solo un valore di elemento dati. Sarà necessario creare un elemento dati che si risolva nell’oggetto di consenso.

In questa azione, ti viene anche fornito un campo facoltativo per includere una mappa di identità in modo che le identità possano essere sincronizzate una volta ricevuto il consenso. La sincronizzazione è utile quando il consenso è configurato come &quot;In sospeso&quot; o &quot;Fuori&quot; perché è probabile che la chiamata di consenso sia la prima chiamata da attivare.

## Ripristina ID unione evento

Se desideri reimpostare l’ID unione eventi sulla pagina, puoi farlo con questa azione. Per reimpostare l’ID, seleziona l’ID unione da reimpostare e attiva l’azione in base alle esigenze.

## Cosa succede ora

Dopo aver impostato le azioni, [configurare i tipi di elementi dati](data-element-types.md).
