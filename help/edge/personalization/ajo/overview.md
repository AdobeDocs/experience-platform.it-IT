---
title: Utilizzo di Adobe Journey Optimizer con Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con Experience Platform Web SDK tramite Adobe Journey Optimizer
keywords: AJO;Web AJO;adobe percorsi optimizer;renderDecision;superfici;decisioni;proposizioni;ambito;schema
exl-id: e608952c-9598-11ed-b382-d72064651cac
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Utilizzo [!DNL Adobe Journey Optimizer] con [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] può fornire ed eseguire il rendering di esperienze personalizzate gestite in [!DNL Adobe Journey Optimizer] al canale web. È possibile utilizzare un editor WYSIWYG, [!DNL Adobe Journey Optimizer] [Interfaccia utente di Campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), per creare, attivare e distribuire le [!DNL Journey Optimizer Web] campagne ed esperienze di personalizzazione.

>[!IMPORTANT]
>
>Leggi la sezione [Documentazione sul canale web Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) per informazioni su come iniziare a utilizzare [!DNL Journey Optimizer Web] creazione di esperienze e reporting.

## Terminologia {#terminology}

**[!UICONTROL Superficie]**: Una superficie web è una proprietà web identificata da un URL in cui [!DNL Adobe Journey Optimizer] il contenuto dell’esperienza verrà consegnato.

**[!UICONTROL Proposte]**: In [!DNL Adobe Journey Optimizer], le proposizioni sono correlate all’esperienza selezionata da un [!DNL Journey Optimizer Campaign].

## Abilitazione [!DNL Adobe Journey Optimizer] {#enable-ajo}

Per iniziare a utilizzare [!DNL Adobe Journey Optimizer], segui i passaggi seguenti.

1. Passare attraverso [prerequisiti](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) dal [!DNL Adobe Journey Optimizer] [Guida alle esperienze web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), in particolare:
   * Configurazione [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Abilita [!DNL Adobe Journey Optimizer] nel tuo [datastream](../../datastreams/overview.md).
   * Abilita la [!UICONTROL Criterio di unione attiva sul bordo] opzione .

2. Aggiungi il `renderDecisions` agli eventi. Imposta `renderDecisions` a `true` per il rendering automatico delle proposte di contenuto Journey Optimizer fornite sulle superfici della pagina web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Facoltativamente, specifica superfici aggiuntive negli eventi. Per impostazione predefinita, l’SDK per web genera automaticamente la superficie web per la pagina web corrente e la include nella richiesta alla rete Edge. Se necessario, è possibile includere ulteriori superfici nella richiesta specificando queste nella `personalization.surfaces` opzione `sendEvent` o nel corrispondente **[!UICONTROL Superfici]** [[!UICONTROL Invia evento] action](../../extension/action-types.md#send-event) configurazione dell&#39;estensione Web SDK.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![superficie aggiuntiva dell&#39;estensione](./assets/extension-add-surface.png)

   Le superfici dell’evento sono incluse nel `query.personalization.surfaces` campo di richiesta:

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. Simile ad altre funzioni di personalizzazione, puoi aggiungere un **[pre-hiding frammento](../manage-flicker.md)** per nascondere solo alcune parti della pagina durante il recupero delle esperienze.

## Creazione di esperienze web Adobe Journey Optimizer {#create-ajo-web-experiences}

Segui [creazione di campagne web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) le istruzioni del [!DNL Adobe Journey Optimizer] [Guida alle esperienze web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) per creare [!DNL Journey Optimizer Web] campagne ed esperienze.

## Rendering di contenuti personalizzati {#rendering-personalized-content}

Consulta la documentazione su [rendering del contenuto di personalizzazione](../rendering-personalization-content.md) per ulteriori informazioni.

Le proposte Adobe Journey Optimizer per le superfici web vengono elaborate in modo simile a `__view__` proposte relative al campo di applicazione della decisione. In particolare, quando `renderDecisions` è impostata su `true` in `sendEvent` Questo comando verrà automaticamente rappresentato dall&#39;SDK per web.

Proposta di contenuto Journey Optimizer di esempio:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Eseguire il debug di {#debugging}

Per eseguire il debug delle implementazioni di personalizzazione Adobe Journey Optimizer, utilizza [[!DNL Web SDK] debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] le tracce di debug sono disponibili quando si risolve il problema utilizzando [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Cerca eventi con `AJO:` Prefisso.

![Assurance-ajo-trace](./assets/assurance-ajo-trace.png)


