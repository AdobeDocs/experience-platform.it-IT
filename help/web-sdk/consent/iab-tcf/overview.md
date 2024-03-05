---
title: Supporto IAB TCF 2.0 nell’SDK per web di Adobe Experience Platform
description: Scopri come supportare le preferenze di consenso IAB TCF 2.0 utilizzando Adobe Experience Platform Web SDK
keywords: consenso;setConsent;Gruppo campi privacy profilo;Gruppo campi privacy evento esperienza;Gruppo campi privacy;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Supporto IAB TCF 2.0 nell’SDK per web di Adobe Experience Platform

Adobe Experience Platform Web SDK supporta Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0). Questa guida illustra i requisiti per supportare IAB TCF 2.0 tramite Adobe Experience Platform Web SDK tramite l’integrazione con Adobe Real-time Customer Data Platform, Audienci Manager, Experience Events, Adobe Analytics ed Edge Network.

Sono inoltre disponibili le seguenti guide per scoprire come integrare IAB TCF 2.0 con e senza tag.

- [Con tag](./with-tags.md)
- [Senza tag](./without-tags.md)

## Introduzione

Per implementare l’SDK per web con IAB TCF 2.0, è necessario avere una buona conoscenza degli Experience Data Model (XDM) e degli eventi di esperienza. Prima di iniziare, consulta il seguente documento:

- [Panoramica del sistema Experience Data Model (XDM)](../../../xdm/home.md): standardizzazione e interoperabilità sono concetti chiave alla base di Adobe Experience Platform. [!DNL Experience Data Model (XDM)], guidato da un Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

## Integrazione Experienci Platform

Per inviare i dati del consenso a Adobe Experience Platform utilizzando l’SDK, è necessario quanto segue:

- Un set di dati il cui schema è basato su [!DNL XDM Individual Profile] e contiene campi di consenso TCF 2.0, abilitati per l’utilizzo in [!DNL Real-Time Customer Profile].
- Un flusso di dati configurato con Platform e il set di dati abilitato per il profilo indicato sopra.

Consulta la guida su [Conformità TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) per istruzioni sulla creazione dei set di dati e dello stream di dati richiesti.

## Integrazione Audienci Manager

Adobe Audience Manager (AAM) include il supporto per IAB TCF 2.0, che consente di valutare, rispettare e inoltrare le scelte sulla privacy dei clienti ai partner a valle. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Per l’integrazione con Audienci Manager tramite Adobe Experience Platform Web SDK, assicurati di disporre di uno stream di dati configurato per l’inoltro a Adobe Audience Manager.

## Eventi esperienza e integrazione con Adobe Analytics

Mentre il pubblico di Real-Time CDP e di Audienci Manager tiene traccia delle preferenze di consenso attuali di un cliente, gli Eventi esperienza possono contenere le preferenze di consenso di un cliente che erano attive al momento della raccolta dell’evento.

Per raccogliere le informazioni sul consenso relative agli eventi, è necessario quanto segue:

- Un set di dati basato su [!DNL XDM Experience Event] classe, con [!DNL Experience Event] gruppo di campi schema privacy.
- Un flusso di dati configurato con [!DNL XDM Experience Event] set di dati precedente.

Per ulteriori informazioni su come convertire un evento esperienza XDM in un hit di Analytics, consulta [Invio di dati ad Adobe Analytics tramite Web SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Integrazione di Adobe Experience Platform Web SDK

Le sezioni seguenti descrivono i punti di integrazione principali tra IAB TCF 2.0 e Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Anche senza la configurazione di Real-Time CDP o Audienci Manager, è comunque possibile integrare IAB TCF 2.0 con l’SDK per web. Le preferenze di consenso possono essere utilizzate per controllare la raccolta di eventi esperienza e l’impostazione di un cookie di identità.

### Consenso predefinito

Il consenso predefinito viene utilizzato quando per un cliente non è già stata salvata alcuna preferenza di consenso. Ciò significa che le opzioni di consenso predefinite possono controllare il comportamento di Adobe Experience Platform Web SDK e le modifiche in base all’area geografica del cliente.

Ad esempio, se un cliente non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`, ma all’interno della giurisdizione del RGPD, il consenso predefinito può essere impostato su `pending`. La piattaforma di gestione del consenso (CMP) potrebbe rilevare l’area geografica del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito. Consulta [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) per ulteriori informazioni.

### Impostazione del consenso in caso di modifiche

Adobe Experience Platform Web SDK dispone di un `setConsent` che comunica le preferenze di consenso del cliente a tutti i servizi Adobe utilizzando IAB TCF 2.0. Se esegui l’integrazione con Real-Time CDP, questo aggiorna il profilo del cliente. Se esegui l’integrazione con Audienci Manager, le informazioni del cliente vengono aggiornate. Una chiamata a questo indirizzo imposta anche un cookie con una preferenza di consenso &quot;tutto o niente&quot; che controlla se è consentito inviare eventi di esperienza futuri. Questa azione deve essere chiamata ogni volta che cambia il consenso. Al caricamento futuro delle pagine, il cookie di consenso della rete Edge verrà letto per determinare se è possibile inviare eventi esperienza e impostare un cookie di identità.

Analogamente all’integrazione IAB TCF 2.0 di Audienci Manager, la rete Edge fornisce il consenso quando un cliente ha fornito il proprio consenso esplicito alle seguenti finalità:

- **Scopo 1:** Memorizzare e/o accedere alle informazioni su un dispositivo
- **Scopo 10:** Sviluppo e miglioramento dei prodotti
- **Uso speciale 1:** Garantire la sicurezza, prevenire le frodi ed eseguire il debug. (In base alle normative IAB TCF, questo è sempre consentito)
- **Adobe autorizzazione fornitore:** Consenso per Adobe (fornitore 565)

Per ulteriori informazioni su `setConsent` , leggi la documentazione su [Consenso di supporto](../../consent/supporting-consent.md).

### Aggiunta di consenso agli eventi esperienza

Adobe Experience Platform Web SDK dispone di un [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) comando che raccoglie un evento esperienza. Se ti stai integrando con Experience Events o Adobe Analytics e desideri le preferenze di consenso su ogni Experience Event, aggiungi informazioni di consenso ad ogni `sendEvent` comando.

## Passaggi successivi

Ora che hai una conoscenza di base di IAB Transparency &amp; Consent Framework 2.0, consulta una delle guide sull’utilizzo di IAB TCF 2.0 [con tag](./with-tags.md) o [senza tag](./without-tags.md).
