---
keywords: Experience Platform;home;argomenti popolari;ECID;ecid
solution: Experience Platform
title: Dati di identità per le richieste di privacy
topic-legacy: overview
description: Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# Dati di identità per richieste di privacy

Affinché Adobe Experience Platform [!DNL Privacy Service] possa elaborare le richieste dei clienti per i loro dati privati (incluse le richieste di accesso, cancellazione o rinuncia alla vendita), deve essere fornito con identificatori univoci che collegano un cliente specifico ai suoi dati privati memorizzati nelle applicazioni abilitate per Adobe Experience Cloud. [!DNL Privacy Service] utilizza quindi questi identificatori per raccogliere tutti i dati memorizzati sotto l&#39;identità del cliente all&#39;interno  [!DNL Experience Cloud] e elaborarli in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.

## Identità e namespace

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da quelle numerose interazioni. Questo a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nelle applicazioni [!DNL Experience Cloud].

Ad esempio, quando gestisci le richieste di dati del cliente in [!DNL Privacy Service], un&#39;identità può rappresentare un valore cookie impostato in un dominio controllato da Adobe, un valore cookie in un dominio di terze parti e condiviso con Adobe o un identificatore personalizzato definito esplicitamente all&#39;interno dell&#39;organizzazione IMS.

È pertanto necessario che ogni identità inviata a [!DNL Privacy Service] sia accompagnata da un namespace che fornisca contesto collegando il valore dell&#39;identità al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Il servizio Adobe Experience Platform Identity conserva un archivio di namespace di identità definiti a livello globale e definiti dall’utente. Per informazioni più dettagliate sugli spazi dei nomi, consulta la [panoramica dello spazio dei nomi di identità](../identity-service/namespaces.md). Per un elenco dei namespace standard e dei qualificatori dello spazio dei nomi comunemente utilizzati in [!DNL Privacy Service], consulta la sezione [appendice](api/appendix.md) nella guida per gli sviluppatori.

## Servizio ECID e Opt-in

Adobe Experience Cloud [!DNL Identity Service] funge da framework di identificazione comune per [!DNL Experience Cloud] e assegna un ID univoco e costante a ogni visitatore del sito. L’ [!DNL Experience Cloud] ID (ECID) tiene traccia dell’attività di un cliente tramite l’utilizzo di un cookie di prima parte, può identificare in modo univoco un dispositivo su più applicazioni e consente di identificare lo stesso visitatore del sito e i relativi dati in diverse applicazioni [!DNL Experience Cloud]. Per ulteriori informazioni, consulta la [Panoramica del servizio Experience Cloud Identity](https://docs.adobe.com/content/help/it-IT/id-service/using/intro/overview.html) .

Il servizio Opt-in, un&#39;estensione di [!DNL Experience Cloud Identity Service], consente di impostare protocolli sull&#39;applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul servizio Opt-in e su come configurare il servizio per la tua applicazione, consulta la [documentazione del servizio Opt-in](https://docs.adobe.com/content/help/it-IT/id-service/using/implementation/opt-in-service/optin-overview.html) .

Una volta che ai visitatori del sito sono stati assegnati gli ECID, puoi utilizzare l’Adobe [!DNL Privacy JavaScript Library] per recuperare tali ID da utilizzare nelle richieste di privacy, come descritto nella sezione successiva.

## [!DNL Privacy JS Library]

Il [!DNL Adobe Privacy JavaScript Library] fornisce diverse funzioni che ti consentono di recuperare e rimuovere le identità cliente memorizzate nel browser. La libreria può essere configurata per recuperare informazioni di identità da diverse applicazioni di Adobe, incluso ECID. Utilizzando callback o promesse, puoi gestire in modo programmatico gli ID recuperati e inviarli all’ [!DNL Privacy Service] API.

Per ulteriori informazioni su [!DNL Privacy JS Library], inclusi esempi di codice per diversi casi d&#39;uso comuni, consulta la [Panoramica della libreria JS sulla privacy](js-library.md).

## Passaggi successivi

Questo documento fornisce una breve panoramica dei concetti fondamentali relativi al recupero dei dati di identità del cliente da utilizzare nelle richieste sulla privacy. Per informazioni più dettagliate su questi concetti e servizi, è consigliabile consultare i collegamenti alla documentazione forniti in ciascuna sezione. Per informazioni su come inviare gli ID recuperati a [!DNL Privacy Service] per creare richieste di accesso, cancellazione o rinuncia alla vendita, consulta la [Guida per gli sviluppatori di Privacy Service](api/getting-started.md).
