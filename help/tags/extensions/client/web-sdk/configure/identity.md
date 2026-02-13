---
title: Impostazioni di configurazione identità
description: Definisci in che modo l’estensione tag identifica i visitatori.
exl-id: 12e707f4-c37b-4c02-bfec-5ef7b98c2d3b
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---

# Impostazioni di configurazione identità {#identity}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_identity"
>title="Identità"
>abstract="Definisci in che modo l’estensione tag identifica i visitatori."

Questa sezione di configurazione consente di definire il comportamento del Web SDK per la gestione dell&#39;identificazione degli utenti.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Identity]**.

![Immagine che mostra le impostazioni di identità dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag](../assets/web-sdk-ext-identity.png)

Sono disponibili le seguenti opzioni:

## [!UICONTROL Migrate ECID from VisitorAPI]

Casella di controllo che consente al Web SDK di leggere i cookie `AMCV` e `s_ecid` e impostare il cookie `AMCV` utilizzato da `Visitor.js`. Questa funzione è importante durante la migrazione dalle librerie che utilizzano `VisitorAPI.js` al Web SDK, poiché alcune pagine potrebbero utilizzare ancora `Visitor.js`. Questa opzione consente a SDK di continuare a utilizzare lo stesso ECID in modo che gli utenti non vengano identificati come due utenti separati. La libreria JavaScript equivalente a questa casella di controllo è [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## [!UICONTROL Use third-party cookies]

Quando questa opzione è abilitata, il Web SDK tenta di memorizzare un identificatore utente in un cookie di terze parti. In caso di esito positivo, l’utente viene identificato come un singolo utente mentre si sposta tra più domini, anziché essere identificato come un utente separato su ciascun dominio. Se questa opzione è abilitata, SDK potrebbe non essere ancora in grado di memorizzare l’identificatore utente in un cookie di terze parti se il browser non supporta i cookie di terze parti o è stato configurato dall’utente per non consentire i cookie di terze parti. In questo caso, SDK memorizza l’identificatore solo nel dominio di prime parti. La libreria JavaScript equivalente a questa casella di controllo è [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md).

>[!IMPORTANT]
>
>I cookie di terze parti non sono compatibili con la funzionalità [ID dispositivo di prima parte](/help/collection/use-cases/identity/first-party-device-ids.md) in Web SDK. Puoi utilizzare gli ID dispositivo di prime parti oppure cookie di terze parti; non puoi utilizzare entrambe le funzioni contemporaneamente.
