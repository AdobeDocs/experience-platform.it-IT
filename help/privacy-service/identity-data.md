---
keywords: Experience Platform;home;argomenti popolari;ECID;ecid
solution: Experience Platform
title: Dati di identità per richieste di privacy
description: Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste dei clienti sulla privacy.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 2%

---

# Dati di identità per le richieste di privacy

In ordine per Adobe Experience Platform [!DNL Privacy Service] per elaborare le richieste dei clienti relative ai loro dati privati (comprese le richieste di accesso, cancellazione o rinuncia alla vendita), è necessario fornire identificatori univoci che colleghino un cliente specifico ai suoi dati privati memorizzati nelle applicazioni abilitate per Adobe Experience Cloud. [!DNL Privacy Service] utilizza quindi questi identificatori per raccogliere tutti i dati memorizzati sotto l’identità del cliente in [!DNL Experience Cloud], ed elaborarlo in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste dei clienti sulla privacy.

## Identità e namespace

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da tali numerose interazioni. Questo a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nel tuo [!DNL Experience Cloud] applicazioni.

Ad esempio, quando gestisci le richieste di dati dei clienti in [!DNL Privacy Service], un’identità può rappresentare un valore di cookie impostato in un dominio controllato da Adobe, un valore di cookie in un dominio di terze parti e condiviso con Adobe oppure un identificatore personalizzato definito esplicitamente all’interno della tua organizzazione IMS.

È pertanto necessario che ogni identità inviata a [!DNL Privacy Service] è accompagnato da uno spazio dei nomi che fornisce contesto correlando il valore di identità al relativo sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, come un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Il servizio Adobe Experience Platform Identity gestisce un archivio di spazi dei nomi di identità definiti a livello globale e dall’utente. Per informazioni più dettagliate sugli spazi dei nomi, vedi [panoramica dello spazio dei nomi delle identità](../identity-service/namespaces.md). Per un elenco degli spazi dei nomi standard e dei qualificatori degli spazi dei nomi comunemente utilizzati in [!DNL Privacy Service], vedere [sezione dell&#39;appendice](api/appendix.md) nella guida dell’API.

## ECID e servizio Opt-in

Adobe Experience Cloud [!DNL Identity Service] funge da quadro comune di identificazione per [!DNL Experience Cloud]e assegna un ID univoco e costante a ciascun visitatore del sito. Il [!DNL Experience Cloud] L’ID (ECID) tiene traccia dell’attività di un cliente tramite l’utilizzo di un cookie di prima parte, può identificare in modo univoco un dispositivo tra più applicazioni e consente di identificare lo stesso visitatore del sito e i suoi dati in diversi [!DNL Experience Cloud] applicazioni. Consulta la [Panoramica del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) per ulteriori informazioni.

Servizio Opt-in, estensione di [!DNL Experience Cloud Identity Service], consente di configurare i protocolli nell’applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul Servizio Opt-in, tra cui la modalità di configurazione del servizio per l&#39;applicazione, fare riferimento a [Documentazione del servizio Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it).

Una volta assegnati gli ECID ai visitatori del sito, puoi utilizzare l’Adobe [!DNL Privacy JavaScript Library] per recuperare gli ID da utilizzare nelle richieste di accesso a dati personali, come descritto nella sezione successiva.

## [!DNL Privacy JS Library]

Il [!DNL Adobe Privacy JavaScript Library] fornisce diverse funzioni che ti consentono di recuperare e rimuovere le identità dei clienti memorizzate nel browser. La libreria può essere configurata per recuperare informazioni sull’identità da diverse applicazioni Adobe, incluso ECID. Tramite l’utilizzo di callback o promesse, puoi gestire in modo programmatico gli ID recuperati correttamente e inviarli al [!DNL Privacy Service] API.

Per ulteriori informazioni su [!DNL Privacy JS Library], inclusi esempi di codice per diversi casi d’uso comuni, consulta [Panoramica della libreria JS per la privacy](js-library.md).

## Passaggi successivi

Questo documento fornisce una breve panoramica dei concetti centrali coinvolti nel recupero dei dati di identità del cliente da utilizzare nelle richieste di accesso a dati personali. Per informazioni più dettagliate su questi concetti e servizi, si consiglia di consultare i collegamenti alla documentazione forniti in ciascuna sezione. Per i passaggi su come inviare gli ID recuperati a [!DNL Privacy Service] per creare richieste di accesso, cancellazione o rinuncia alla vendita, vedi [Guida all’API di Privacy Service](api/overview.md).
