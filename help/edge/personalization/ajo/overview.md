---
title: Utilizzo di Adobe Journey Optimizer con Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con l’SDK per web di Experience Platform utilizzando Adobe Journey Optimizer
keywords: ajo;ajo web;adobe percorsi optimizer;renderDecisions;superfici;decisioni;proposte;ambito;schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Utilizzo di [!DNL Adobe Journey Optimizer] con [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] può distribuire ed eseguire il rendering di esperienze personalizzate gestite in [!DNL Adobe Journey Optimizer] al canale web. È possibile utilizzare un editor WYSIWYG, [!DNL Adobe Journey Optimizer] [Interfaccia utente di Web Campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), per creare, attivare e consegnare [!DNL Journey Optimizer Web] campagne e esperienze di personalizzazione.

>[!IMPORTANT]
>
>Leggi le [Documentazione di Adobe Journey Optimizer Web Channel](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) per informazioni su come iniziare a utilizzare [!DNL Journey Optimizer Web] creazione di esperienze e reporting.

## Terminologia {#terminology}

**[!UICONTROL Superficie]**: una superficie web è una proprietà web identificata da un URL in cui [!DNL Adobe Journey Optimizer] il contenuto dell’esperienza verrà consegnato.

**[!UICONTROL Proposte]**: In [!DNL Adobe Journey Optimizer], le proposte sono correlate all’esperienza selezionata da un [!DNL Journey Optimizer Campaign].

## Abilitazione [!DNL Adobe Journey Optimizer] {#enable-ajo}

Per iniziare a utilizzare [!DNL Adobe Journey Optimizer], segui la procedura indicata di seguito.

1. Passare attraverso [prerequisiti](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) dal [!DNL Adobe Journey Optimizer] [Guida alle esperienze web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), in particolare:
   * Configurazione [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Abilita [!DNL Adobe Journey Optimizer] nel tuo [flusso di dati](../../../datastreams/overview.md).
   * Abilita [!UICONTROL Criterio di unione Attivo su Edge] opzione.

2. Aggiungi il `renderDecisions` agli eventi. Imposta `renderDecisions` a `true` per il rendering automatico delle proposte di contenuti Journey Optimizer distribuite sulle superfici delle pagine web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Facoltativamente, specificare superfici aggiuntive negli eventi. Per impostazione predefinita, Web SDK genera automaticamente la superficie web per la pagina web corrente e la include nella richiesta alla rete Edge. Se necessario, è possibile includere superfici aggiuntive nella richiesta specificandole nella `personalization.surfaces` opzione del `sendEvent` o nel corrispondente **[!UICONTROL Superfici]** [[!UICONTROL Invia evento] azione](../../../tags/extensions/client/web-sdk/action-types.md#send-event) configurazione dell’estensione Web SDK.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   Le superfici degli eventi sono incluse nel `query.personalization.surfaces` campo richiesta:

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

4. Analogamente ad altre funzioni di personalizzazione, puoi aggiungere **[frammento pre-hiding](../manage-flicker.md)** per nascondere solo alcune parti della pagina durante il recupero delle esperienze.

## Creazione di esperienze web Adobe Journey Optimizer {#create-ajo-web-experiences}

Segui le [authoring di campagne web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) istruzioni del [!DNL Adobe Journey Optimizer] [Guida alle esperienze web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) per creare [!DNL Journey Optimizer Web] campagne ed esperienze.

## Rendering di contenuti personalizzati {#rendering-personalized-content}

Consulta la documentazione su [rendering del contenuto di personalizzazione](../rendering-personalization-content.md) per ulteriori informazioni.

Le proposte Adobe Journey Optimizer per le superfici web vengono elaborate in modo simile al `__view__` proposte relative all’ambito decisionale. In particolare, quando `renderDecisions` è impostata su `true` nel `sendEvent` comando di rendering di questi elementi verrà eseguito automaticamente dall&#39;SDK Web.

Esempio di proposta di contenuto Journey Optimizer:

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

Per eseguire il debug delle implementazioni di personalizzazione di Adobe Journey Optimizer, utilizza [[!DNL Web SDK] debug](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] le tracce di debug sono disponibili quando si risolvono i problemi utilizzando [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Verificare la presenza di eventi con `AJO:` prefisso.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
