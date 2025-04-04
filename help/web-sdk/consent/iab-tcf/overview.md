---
title: Supporto IAB TCF 2.0 nel Adobe Experience Platform Web SDK
description: Scopri come supportare le preferenze di consenso IAB TCF 2.0 utilizzando Adobe Experience Platform Web SDK
keywords: consenso;setConsent;Gruppo campi privacy profilo;Gruppo campi privacy evento esperienza;Gruppo campi privacy;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Supporto IAB TCF 2.0 in Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK supporta Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0). Questa guida illustra i requisiti per supportare IAB TCF 2.0 tramite Adobe Experience Platform Web SDK con integrazione con Adobe Real-Time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics e Edge Network.

Sono inoltre disponibili le seguenti guide per scoprire come integrare IAB TCF 2.0 con e senza tag.

- [Con tag](./with-tags.md)
- [Senza tag](./without-tags.md)

## Introduzione

Per implementare il Web SDK con IAB TCF 2.0, è necessario avere una buona conoscenza del Experience Data Model (XDM) e degli eventi di esperienza. Prima di iniziare, consulta il seguente documento:

- [Panoramica del sistema Experience Data Model (XDM)](../../../xdm/home.md): la standardizzazione e l&#39;interoperabilità sono concetti chiave di Adobe Experience Platform. [!DNL Experience Data Model (XDM)], gestito da Adobe, è un tentativo di standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

## Integrazione con Experience Platform

Per inviare i dati del consenso a Adobe Experience Platform utilizzando SDK, è necessario quanto segue:

- Set di dati il cui schema è basato sulla classe [!DNL XDM Individual Profile] e contiene campi di consenso TCF 2.0, abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile].
- Un flusso di dati configurato con Experience Platform e il set di dati abilitato al profilo indicato sopra.

Per istruzioni sulla creazione dei set di dati e dello stream di dati richiesti, consulta la guida sulla conformità a [TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md).

## Integrazione con Audience Manager

Adobe Audience Manager (AAM) include il supporto per IAB TCF 2.0, che consente di valutare, rispettare e inoltrare le scelte sulla privacy dei clienti ai partner a valle. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Per l’integrazione con Audience Manager tramite Adobe Experience Platform Web SDK, assicurati di disporre di uno stream di dati configurato per l’inoltro a Adobe Audience Manager.

## Eventi esperienza e integrazione con Adobe Analytics

Mentre i tipi di pubblico di Real-Time CDP e Audience Manager tengono traccia delle preferenze di consenso correnti di un cliente, gli Eventi esperienza possono contenere le preferenze di consenso di un cliente che erano attive al momento della raccolta dell’evento.

Per raccogliere le informazioni sul consenso relative agli eventi, è necessario quanto segue:

- Un set di dati basato sulla classe [!DNL XDM Experience Event], con il gruppo di campi dello schema di privacy [!DNL Experience Event].
- Uno stream di dati configurato con il set di dati [!DNL XDM Experience Event] precedente.

Per ulteriori informazioni su come convertire un evento esperienza XDM in un hit di Analytics, consulta [Invio di dati ad Adobe Analytics tramite Web SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Integrazione con Adobe Experience Platform Web SDK

Le sezioni seguenti descrivono i principali punti di integrazione tra IAB TCF 2.0 e Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Anche senza la configurazione di Real-Time CDP o Audience Manager, è comunque possibile integrare IAB TCF 2.0 con il Web SDK. Le preferenze di consenso possono essere utilizzate per controllare la raccolta di eventi esperienza e l’impostazione di un cookie di identità.

### Consenso predefinito

Il consenso predefinito viene utilizzato quando per un cliente non è già stata salvata alcuna preferenza di consenso. Ciò significa che le opzioni di consenso predefinite possono controllare il comportamento di Adobe Experience Platform Web SDK e cambiare in base all’area geografica del cliente.

Ad esempio, se un cliente non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`, ma all&#39;interno della giurisdizione del RGPD, il consenso predefinito può essere impostato su `pending`. La piattaforma di gestione del consenso (CMP) potrebbe rilevare l&#39;area geografica del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito. Per ulteriori informazioni, vedere [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md).

### Impostazione del consenso in caso di modifiche

Adobe Experience Platform Web SDK dispone di un comando `setConsent` che comunica le preferenze di consenso del cliente a tutti i servizi Adobe utilizzando IAB TCF 2.0. Se esegui l’integrazione con Real-Time CDP, questo aggiorna il profilo del cliente. Se esegui l’integrazione con Audience Manager, le informazioni del cliente vengono aggiornate. Una chiamata a questo indirizzo imposta anche un cookie con una preferenza di consenso &quot;tutto o niente&quot; che controlla se è consentito inviare eventi di esperienza futuri. Questa azione deve essere chiamata ogni volta che cambia il consenso. Al caricamento delle pagine future, il cookie di consenso di Edge Network verrà letto per determinare se è possibile inviare eventi di esperienza e impostare un cookie di identità.

Simile all’integrazione IAB TCF 2.0 di Audience Manager, Edge Network fornisce il consenso quando un cliente ha fornito il proprio consenso esplicito per le seguenti finalità:

- **Scopo 1:** Archiviare e/o accedere a informazioni su un dispositivo
- **Scopo 10:** sviluppare e migliorare i prodotti
- **Scopo speciale 1:** Garantire la sicurezza, prevenire le frodi ed eseguire il debug. (In base alle normative IAB TCF, questo è sempre consentito)
- **Autorizzazione fornitore Adobe:** Consenso per Adobe (fornitore 565)

Per ulteriori informazioni sul comando `setConsent`, leggere la documentazione dedicata di Web SDK in [setConsent](../../../web-sdk/commands/setconsent.md).

### Aggiunta di consenso agli eventi esperienza

Adobe Experience Platform Web SDK dispone di un comando [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) che raccoglie un evento esperienza. Se ti stai integrando con Experience Events o Adobe Analytics e desideri le preferenze di consenso per ogni evento esperienza, aggiungi informazioni di consenso a ogni comando `sendEvent`.

## Passaggi successivi

Ora che hai una conoscenza di base di IAB Transparency &amp; Consent Framework 2.0, consulta una delle guide sull&#39;utilizzo di IAB TCF 2.0 [con tag](./with-tags.md) o [senza tag](./without-tags.md).
