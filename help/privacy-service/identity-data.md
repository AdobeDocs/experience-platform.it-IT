---
keywords: Experience Platform;home;argomenti popolari;ECID;ecid
solution: Experience Platform
title: Dati di identità per le richieste di privacy
description: Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# Dati di identità per richieste di privacy

Per Adobe Experience Platform [!DNL Privacy Service] per elaborare le richieste dei clienti per i loro dati privati (incluse le richieste di accesso, cancellazione o rinuncia alla vendita), è necessario fornire loro identificatori univoci che collegano un cliente specifico ai suoi dati privati memorizzati nelle applicazioni abilitate per Adobe Experience Cloud. [!DNL Privacy Service] utilizza quindi questi identificatori per raccogliere tutti i dati memorizzati sotto l&#39;identità del cliente in [!DNL Experience Cloud], ed elaboralo in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.

## Identità e namespace

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da quelle numerose interazioni. Questo a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nel tuo [!DNL Experience Cloud] applicazioni.

Ad esempio, quando gestisci le richieste di dati dei clienti in [!DNL Privacy Service], un&#39;identità può rappresentare un valore cookie impostato in un dominio controllato da Adobe, un valore cookie in un dominio di terze parti e condiviso con Adobe oppure un identificatore personalizzato definito esplicitamente all&#39;interno dell&#39;organizzazione.

È pertanto necessario che ogni identità inviata a [!DNL Privacy Service] è accompagnato da uno spazio dei nomi che fornisce contesto collegando il valore dell&#39;identità al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Il servizio Adobe Experience Platform Identity conserva un archivio di namespace di identità definiti a livello globale e definiti dall’utente. Per informazioni più dettagliate sugli spazi dei nomi, consulta la sezione [panoramica dello spazio dei nomi identità](../identity-service/namespaces.md). Per un elenco dei namespace standard e dei qualificatori dello spazio dei nomi comunemente utilizzati in [!DNL Privacy Service], vedi [sezione appendice](api/appendix.md) nella guida API.

## Servizio ECID e Opt-in

Adobe Experience Cloud [!DNL Identity Service] funge da quadro comune di identificazione per [!DNL Experience Cloud]e assegna un ID univoco e costante a ogni visitatore del sito. La [!DNL Experience Cloud] L’ID (ECID) tiene traccia dell’attività di un cliente tramite l’utilizzo di un cookie di prima parte, può identificare in modo univoco un dispositivo su più applicazioni e consente di identificare lo stesso visitatore del sito e i relativi dati in diversi [!DNL Experience Cloud] applicazioni. Consulta la sezione [Panoramica del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) per ulteriori informazioni.

Servizio Opt-in, un&#39;estensione di [!DNL Experience Cloud Identity Service], consente di impostare protocolli sull’applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul servizio Opt-in e su come configurare il servizio per la tua applicazione, consulta [Documentazione del servizio Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it).

Una volta assegnati gli ECID ai visitatori del sito, puoi utilizzare l’Adobe [!DNL Privacy JavaScript Library] per recuperare gli ID da utilizzare nelle richieste di accesso a dati personali, come descritto nella sezione successiva.

## [!DNL Privacy JS Library]

La [!DNL Adobe Privacy JavaScript Library] fornisce diverse funzioni che ti consentono di recuperare e rimuovere le identità cliente memorizzate nel browser. La libreria può essere configurata per recuperare informazioni di identità da diverse applicazioni di Adobe, incluso ECID. Utilizzando callback o promesse, puoi gestire gli ID recuperati e inviarli al [!DNL Privacy Service] API.

Per ulteriori informazioni [!DNL Privacy JS Library], compresi i campioni di codice per diversi casi d&#39;uso comuni, si prega di fare riferimento al [Panoramica sulla libreria JS per la privacy](js-library.md).

## Passaggi successivi

Questo documento fornisce una breve panoramica dei concetti fondamentali relativi al recupero dei dati di identità del cliente da utilizzare nelle richieste sulla privacy. Per informazioni più dettagliate su questi concetti e servizi, è consigliabile consultare i collegamenti alla documentazione forniti in ciascuna sezione. Per i passaggi su come inviare gli ID recuperati a [!DNL Privacy Service] per creare richieste di accesso, cancellazione o rinuncia alla vendita, consulta la [Guida all’API di Privacy Service](api/overview.md).
