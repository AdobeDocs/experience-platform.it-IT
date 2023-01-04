---
title: Supporto IAB TCF 2.0 nell’SDK Web per Adobe Experience Platform
description: Scopri come supportare le preferenze di consenso IAB TCF 2.0 utilizzando l’SDK web di Adobe Experience Platform
keywords: consenso;setConsent;gruppo di campi per la privacy dei profili;gruppo di campi per la privacy degli eventi di esperienza;gruppo di campi per la privacy;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Supporto di IAB TCF 2.0 nell’SDK Web per Adobe Experience Platform

Adobe Experience Platform Web SDK supporta la versione 2.0 di Interactive Advertising Bureau Transparency &amp; Consent Framework (IAB TCF 2.0). Questa guida mostra i requisiti per supportare IAB TCF 2.0 tramite Adobe Experience Platform Web SDK integrato con Adobe Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics ed Experience Edge.

Sono inoltre disponibili le seguenti guide per informazioni su come integrare IAB TCF 2.0 con e senza tag.

- [Con tag](./with-launch.md)
- [Senza tag](./without-launch.md)

## Introduzione

Per implementare l’SDK web con IAB TCF 2.0, è necessario avere una comprensione funzionante di Experience Data Model (XDM) e Experience Events. Prima di iniziare, controlla il seguente documento:

- [Panoramica del sistema Experience Data Model (XDM)](../../../xdm/home.md): La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. [!DNL Experience Data Model (XDM)], guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

## Integrazione Experience Platform

Per inviare i dati di consenso a Adobe Experience Platform utilizzando l’SDK, è necessario quanto segue:

- Un set di dati il cui schema è basato su [!DNL XDM Individual Profile] contiene campi di consenso TCF 2.0 abilitati per l’utilizzo in [!DNL Real-Time Customer Profile].
- Un datastream configurato con Platform e il set di dati abilitati per il profilo di cui sopra.

Fai riferimento alla guida su [Conformità a TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) per istruzioni su come creare i set di dati e il datastream richiesti.

## Integrazione Audience Manager

Adobe Audience Manager (AAM) include il supporto per IAB TCF 2.0, che ti consente di valutare, onorare e inoltrare le scelte relative alla privacy dei clienti ai partner a valle. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Per eseguire l’integrazione con Audience Manager tramite Adobe Experience Platform Web SDK, assicurati di disporre di un datastream configurato per l’inoltro a Adobe Audience Manager.

## Integrazione di Experience Events e Adobe Analytics

Mentre i tipi di pubblico di Real-Time CDP e Audience Manager tengono traccia delle preferenze di consenso correnti di un cliente, gli eventi di esperienza possono contenere le preferenze di consenso di un cliente che erano attive al momento della raccolta dell&#39;evento.

Per raccogliere le informazioni sul consenso sugli eventi, è necessario quanto segue:

- Un set di dati basato su [!DNL XDM Experience Event] con [!DNL Experience Event] gruppo di campi dello schema di privacy.
- Un datastream configurato con [!DNL XDM Experience Event] dataset qui sopra.

Per ulteriori informazioni su come convertire un evento esperienza XDM in un hit di Analytics, inizia leggendo il [Panoramica di Analytics](../../data-collection/adobe-analytics/analytics-overview.md) documentazione.

## Integrazione Adobe Experience Platform Web SDK

Le sezioni seguenti descrivono i punti di integrazione principali tra IAB TCF 2.0 e Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Anche senza l’impostazione di Real-Time CDP o Audience Manager, puoi comunque integrare IAB TCF 2.0 con l’SDK per web. Le preferenze di consenso possono essere utilizzate per controllare la raccolta di Experience Events e per impostare un cookie di identità.

### Consenso predefinito

Il consenso predefinito viene utilizzato quando per un cliente non è già stata salvata alcuna preferenza di consenso. Ciò significa che le opzioni di consenso predefinite possono controllare il comportamento di Adobe Experience Platform Web SDK e cambiare in base all&#39;area geografica del cliente.

Ad esempio, se un cliente non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`ma all&#39;interno della giurisdizione del RGPD, il consenso predefinito può essere impostato su `pending`. La piattaforma di gestione del consenso (CMP, Consent Management Platform) potrebbe rilevare l’area geografica del cliente e fornire il flag `gdprApplies` su IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito.

Per ulteriori informazioni sul consenso predefinito, consulta la [sezione consenso predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione dell’SDK.

### Impostazione del consenso quando cambia

L&#39;SDK web di Adobe Experience Platform ha `setConsent` , che comunica le preferenze di consenso del cliente a tutti i servizi Adobe utilizzando IAB TCF 2.0. Se ti stai integrando con Real-Time CDP, questo aggiorna il profilo del cliente. Se esegui l’integrazione con Audience Manager, le informazioni del cliente vengono aggiornate. Una chiamata di questo imposta anche un cookie con una preferenza di consenso all-or-nothing che controlla se gli eventi Experience futuri possono essere inviati. Questa azione viene chiamata ogni volta che cambia il consenso. Nei caricamenti di pagine future, il cookie di consenso di Experience Edge verrà letto per determinare se gli eventi di esperienza possono essere inviati e se è possibile impostare un cookie di identità.

Analogamente all’integrazione IAB TCF 2.0 di Audience Manager, Experience Edge fornisce il consenso quando un cliente ha fornito il proprio consenso esplicito alle seguenti finalità:

- **Scopo 1:** Archiviare e/o accedere alle informazioni su un dispositivo
- **Finalità 10:** Sviluppare e migliorare i prodotti
- **Scopo speciale 1:** Assicurati la sicurezza, evita frodi ed esegui il debug. (Per le normative IAB TCF, questo è sempre consentito)
- **Autorizzazione fornitore Adobe:** Adobe di consenso (fornitore 565)

Per ulteriori informazioni sulla `setConsent` , leggi la documentazione su [Consenso di supporto](../../consent/supporting-consent.md).

### Aggiunta di consenso agli eventi Experience

L&#39;SDK web di Adobe Experience Platform ha `sendEvent` che raccoglie un evento esperienza. Se ti stai integrando con Experience Events o Adobe Analytics e desideri le preferenze di consenso su ogni Experience Event, devi aggiungere le informazioni di consenso a ogni `sendEvent` comando.

Per ulteriori informazioni sulla `sendEvent` , leggi la documentazione su [eventi di tracciamento](../../fundamentals/tracking-events.md).

## Passaggi successivi

Ora che conosci le nozioni di base di IAB Transparency &amp; Consent Framework 2.0, consulta una delle guide sull’utilizzo di IAB TCF 2.0 [con tag](./with-launch.md) o [senza tag](./without-launch.md).
