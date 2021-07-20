---
title: Supporto IAB TCF 2.0 nell’SDK Web per Adobe Experience Platform
description: Scopri come supportare le preferenze di consenso IAB TCF 2.0 utilizzando l’SDK web di Adobe Experience Platform
keywords: consenso;setConsent;gruppo di campi per la privacy dei profili;gruppo di campi per la privacy degli eventi di esperienza;gruppo di campi per la privacy;IAB TCF 2.0;Real-time CDP;Profilo dati cliente in tempo reale
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# Supporto di IAB TCF 2.0 nell’SDK Web per Adobe Experience Platform

Adobe Experience Platform Web SDK supporta la versione 2.0 di Interactive Advertising Bureau Transparency &amp; Consent Framework (IAB TCF 2.0). Questa guida mostra i requisiti per supportare IAB TCF 2.0 tramite Adobe Experience Platform Web SDK integrato con Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics ed Experience Edge.

Sono inoltre disponibili le seguenti guide per aiutarti a integrare IAB TCF 2.0 con e senza Adobe Experience Platform Launch.

- [Con Adobe Experience Platform Launch](./with-launch.md)
- [Senza Adobe Experience Platform Launch](./without-launch.md)

## Introduzione

Per implementare l’SDK web con IAB TCF 2.0, è necessario avere una comprensione funzionante di Experience Data Model (XDM) e degli eventi Experience. Prima di iniziare, controlla il seguente documento:

- [Panoramica](../../../xdm/home.md) del sistema Experience Data Model (XDM): La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. [!DNL Experience Data Model (XDM)], guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

## Integrazione Experience Platform

Per inviare i dati di consenso a Adobe Experience Platform utilizzando l’SDK, è necessario quanto segue:

- Un set di dati il cui schema è basato sulla classe [!DNL XDM Individual Profile] e contiene i campi di consenso TCF 2.0, abilitato per l’utilizzo in [!DNL Real-time Customer Profile].
- Un datastream configurato con Platform e il set di dati abilitati per il profilo di cui sopra.

Fai riferimento alla guida sulla [conformità TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) per istruzioni su come creare i set di dati e il datastream richiesti.

## Integrazione Audience Manager

Adobe Audience Manager (AAM) include il supporto per IAB TCF 2.0, che ti consente di valutare, onorare e inoltrare le scelte relative alla privacy dei clienti ai partner a valle. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Per eseguire l’integrazione con Audience Manager tramite Adobe Experience Platform Web SDK, assicurati di disporre di un datastream configurato per l’inoltro a Adobe Audience Manager.

## Integrazione di Experience Events e Adobe Analytics

Mentre il pubblico di Real-time CDP e Audience Manager tiene traccia delle preferenze di consenso correnti di un cliente, gli eventi di esperienza possono contenere le preferenze di consenso di un cliente che erano attive al momento della raccolta dell&#39;evento.

Per raccogliere le informazioni sul consenso sugli eventi, è necessario quanto segue:

- Un set di dati basato sulla classe [!DNL XDM Experience Event], con il gruppo di campi dello schema di privacy [!DNL Experience Event].
- Un datastream configurato con il set di dati [!DNL XDM Experience Event] sopra.

Per ulteriori informazioni su come convertire un evento esperienza XDM in un hit di Analytics, inizia leggendo la documentazione [Panoramica di Analytics](../../data-collection/adobe-analytics/analytics-overview.md) .

## Integrazione Adobe Experience Platform Web SDK

Le sezioni seguenti descrivono i punti di integrazione principali tra IAB TCF 2.0 e Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Anche senza la configurazione di Real-time CDP o Audience Manager, puoi comunque integrare IAB TCF 2.0 con l’SDK web. Le preferenze di consenso possono essere utilizzate per controllare la raccolta di Experience Events e per impostare un cookie di identità.

### Consenso predefinito

Il consenso predefinito viene utilizzato quando per un cliente non è già stata salvata alcuna preferenza di consenso. Ciò significa che le opzioni di consenso predefinite possono controllare il comportamento di Adobe Experience Platform Web SDK e cambiare in base all&#39;area geografica del cliente.

Ad esempio, se un cliente non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`, ma all’interno della giurisdizione del RGPD, il consenso predefinito può essere impostato su `pending`. La piattaforma di gestione del consenso (CMP) potrebbe rilevare l’area geografica del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito.

Per ulteriori informazioni sul consenso predefinito, consulta la sezione [consenso predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione dell&#39;SDK.

### Impostazione del consenso quando cambia

Adobe Experience Platform Web SDK dispone di un comando `setConsent` che comunica le preferenze di consenso del cliente a tutti i servizi di Adobe utilizzando IAB TCF 2.0. Se si esegue l&#39;integrazione con Real-time CDP, questo aggiorna il profilo del cliente. Se esegui l’integrazione con Audience Manager, le informazioni del cliente vengono aggiornate. Una chiamata di questo imposta anche un cookie con una preferenza di consenso all-or-nothing che controlla se gli eventi Experience futuri possono essere inviati. Questa azione viene chiamata ogni volta che cambia il consenso. Nei caricamenti di pagine future, il cookie di consenso di Experience Edge verrà letto per determinare se gli eventi di esperienza possono essere inviati e se è possibile impostare un cookie di identità.

Analogamente all’integrazione IAB TCF 2.0 di Audience Manager, Experience Edge fornisce il consenso quando un cliente ha fornito il proprio consenso esplicito alle seguenti finalità:

- **Finalità 1:** archiviare e/o accedere alle informazioni su un dispositivo
- **Finalità 10:** sviluppare e migliorare i prodotti
- **Scopo speciale 1:** garantire la sicurezza, prevenire frodi ed eseguire il debug. (Per le normative IAB TCF, questo è sempre consentito)
- **Autorizzazione fornitore Adobe:** consenso per Adobe (fornitore 565)

Per ulteriori informazioni sul comando `setConsent`, consulta la documentazione su [Supporto del consenso](../../consent/supporting-consent.md).

### Aggiunta di consenso agli eventi Experience

Adobe Experience Platform Web SDK dispone di un comando `sendEvent` che raccoglie un evento esperienza. Se effettui l’integrazione con Experience Events o Adobe Analytics e desideri le preferenze di consenso per ogni Experience Event, devi aggiungere le informazioni di consenso a ogni comando `sendEvent`.

Per ulteriori informazioni sul comando `sendEvent`, consulta la documentazione relativa agli [eventi di tracciamento](../../fundamentals/tracking-events.md).

## Passaggi successivi

Ora che conosci le nozioni di base di IAB Transparency &amp; Consent Framework 2.0, fai riferimento a una delle guide sull&#39;utilizzo di IAB TCF 2.0 [con Adobe Experience Platform Launch](./with-launch.md) o [senza Adobe Experience Platform Launch](./without-launch.md).
