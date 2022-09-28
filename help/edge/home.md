---
title: Panoramica dell’SDK per web Adobe Experience Platform
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Platform nel sito web.
keywords: SDK per web Adobe Experience Platform;SDK per web Platform;SDK per web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK per web;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Panoramica di Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nel [!DNL Experience Cloud] tramite Adobe Experience Platform Edge Network. Oltre alla libreria JavaScript, è disponibile un [estensione tag](./extension/web-sdk-extension-configuration.md) per informazioni sulle configurazioni dell&#39;SDK per web.

Per una guida dettagliata alla configurazione dell’SDK per web con tag e invio di dati alle soluzioni, consulta la nostra [Esercitazione sull’implementazione di Adobe Experience Cloud con SDK per web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>Questo prodotto è in continua evoluzione e in crescita per supportare sempre più casi d&#39;uso. Per essere sempre al passo con le ultime novità e vedere cosa sono attualmente supportati, consulta [pagina dei casi d’uso supportati](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] fa parte della raccolta che costituisce il [!DNL Adobe Experience Edge]. [!DNL Experience Edge] è costituito dalle seguenti tecnologie:

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** SDK JavaScript ed estensione tag per semplificare notevolmente la distribuzione [!DNL Adobe] tecnologie.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** Estensione all’SDK per dispositivi mobili v5 per consentire ai clienti di utilizzare la nuova metodologia di distribuzione
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** Una rete distribuita globale di server che consenta una nuova metodologia di distribuzione [!DNL Adobe] products

La [!DNL Adobe Experience Edge] è un nuovo framework per la raccolta di dati a bassa latenza, il calcolo collegabile e l&#39;attivazione rapida dei dati su tutti i canali indirizzabili.

[!DNL Adobe Experience Edge] fornisce un singolo SDK consolidato per ogni canale (JavaScript, Mobile, lato server), che invia dati a un dominio di Adobe comune (`adobedc.net`) e riceve un singolo payload per i dati e la distribuzione dell’esperienza.

Sul lato server, un gateway edge unificato e un framework comune di servizi di piattaforma facilitano il plug-in e l&#39;implementazione di nuove funzionalità in questo ambiente informatico in tempo reale.  Tale architettura:

* Diminuisce il time-to-value del cliente
* Termina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduzione dei costi
* Aumenta la velocità dell&#39;innovazione
* Offre vantaggi competitivi duraturi per i clienti di Adobi

Un unico sistema Edge consolidato consente ai clienti di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come esperienza integrata. Permette [!DNL Adobe] fornire servizi con un costo totale di proprietà inferiore per i clienti.  Aiuta inoltre ad aumentare la velocità dell&#39;innovazione del prodotto rendendo il bordo in tempo reale collegabile e permettendo [!DNL Adobe] e ai suoi clienti di aggiungere più rapidamente nuove funzionalità e logica definita dal cliente a tale sistema in tempo reale.

## Video introduttivo {#video}

Il video seguente offre una panoramica di Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Librerie sostituite dall’SDK per web {#sdks}

L&#39;SDK per web non è solo un wrapper intorno alle librerie esistenti. È una libreria completamente nuova, scritta da zero per incorporare le funzionalità delle librerie esistenti. Il suo scopo è quello di porre fine alle sfide con i tag che devono attivarsi nell&#39;ordine giusto, incoerenza con le problematiche di gestione delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo per implementare [!DNL Experience Cloud] e [open source](https://github.com/adobe/alloy).

L’SDK per web sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata ad Adobe Target, DIL.js aveva inviato una chiamata a Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata ad Adobe Analytics. Questa nuova libreria ed endpoint possono recuperare un ID, recuperare un [!DNL Target] esperienza, inviare dati a [!DNL Audience Manager], e passa i dati a Adobe Experience Platform in una singola chiamata.

Il video seguente illustra Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] in azione. L’esempio video utilizza una singola chiamata all’Adobe che invia i dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrazione da librerie esistenti a SDK web {#migrating-to-web-sdk}

Per semplificare la migrazione da una delle [librerie esistenti](#sdks) all’SDK per web, Adobe offre un percorso di aggiornamento semplificato, che consente di migrare ogni singola pagina del sito web all’SDK per web, senza la necessità di eseguire la migrazione dell’intero sito web contemporaneamente.

Ciò significa che puoi utilizzare l’SDK per web in una pagina e lasciare le librerie esistenti nelle altre pagine, fino a quando non potrai eseguirne la migrazione.

### Considerazioni sulla migrazione da at.js a SDK per web {#considerations}

Prima di eseguire la migrazione delle pagine che utilizzano [!DNL at.js] all&#39;SDK per web, assicurati di abilitare le seguenti opzioni di configurazione dell&#39;SDK per web. In questo modo il profilo del visitatore viene mantenuto durante la navigazione dalle pagine con [!DNL at.js ] alle pagine che utilizzano SDK per web.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [`targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Le seguenti funzionalità di Target non sono supportate durante la migrazione da at.js all’SDK web:
> * [Offerte di reindirizzamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [Supporto per CNAME e tra domini diversi](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


Dopo la migrazione da at.js all’SDK web, devi rimuovere la `targetMigrationEnabled` dalla configurazione.



