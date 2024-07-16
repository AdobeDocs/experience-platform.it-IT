---
keywords: Experience Platform;home;argomenti popolari;ECID;ecid
solution: Experience Platform
title: Dati di identità per richieste di privacy
description: Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste dei clienti sulla privacy.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# Dati di identità per le richieste di privacy

Affinché Adobe Experience Platform [!DNL Privacy Service] possa elaborare le richieste dei clienti relative ai propri dati privati (incluse le richieste di accesso, eliminazione o rinuncia alla vendita), è necessario che gli vengano forniti identificatori univoci che colleghino un cliente specifico ai dati privati archiviati nelle applicazioni abilitate per Adobe Experience Cloud. [!DNL Privacy Service] utilizza quindi questi identificatori per raccogliere tutti i dati archiviati con l&#39;identità del cliente in [!DNL Experience Cloud] ed elaborarli in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste dei clienti sulla privacy.

## Identità e namespace

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da tali numerose interazioni. Questo a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nelle applicazioni [!DNL Experience Cloud].

Quando si gestiscono richieste di dati cliente in [!DNL Privacy Service], ad esempio, un&#39;identità può rappresentare un valore cookie impostato in un dominio controllato da Adobe, un valore cookie in un dominio di terze parti e condiviso con Adobe o un identificatore personalizzato definito in modo esplicito all&#39;interno dell&#39;organizzazione.

È pertanto necessario che ogni identità inviata a [!DNL Privacy Service] sia accompagnata da uno spazio dei nomi che fornisca contesto correlando il valore di identità al relativo sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, come un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Il servizio Adobe Experience Platform Identity gestisce un archivio di spazi dei nomi di identità definiti a livello globale e dall’utente. Per informazioni più dettagliate sugli spazi dei nomi, consulta la [panoramica dello spazio dei nomi delle identità](../identity-service/features/namespaces.md). Per un elenco degli spazi dei nomi standard e dei qualificatori degli spazi dei nomi comunemente utilizzati in [!DNL Privacy Service], vedere la [sezione dell&#39;appendice](api/appendix.md) nella guida dell&#39;API.

## ECID e servizio Opt-in

Adobe Experience Cloud [!DNL Identity Service] funge da framework di identificazione comune per [!DNL Experience Cloud] e assegna un ID univoco e costante a ogni visitatore del sito. L&#39;ID [!DNL Experience Cloud] (ECID) tiene traccia dell&#39;attività di un cliente tramite l&#39;utilizzo di un cookie di prima parte, può identificare in modo univoco un dispositivo tra più applicazioni e consente di identificare lo stesso visitatore del sito e i relativi dati in diverse applicazioni [!DNL Experience Cloud]. Per ulteriori informazioni, consulta la [panoramica del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it).

Il servizio Opt-in, un&#39;estensione di [!DNL Experience Cloud Identity Service], consente di configurare i protocolli nell&#39;applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul servizio Opt-in, tra cui la modalità di configurazione del servizio per l&#39;applicazione, consulta la [documentazione del servizio Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it).

Dopo aver assegnato gli ECID ai visitatori del sito, puoi utilizzare l&#39;Adobe [!DNL Privacy JavaScript Library] per recuperare gli ID da utilizzare nelle richieste di accesso a dati personali, come descritto nella sezione successiva.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] fornisce diverse funzioni che consentono di recuperare e rimuovere le identità del cliente memorizzate nel browser. La libreria può essere configurata per recuperare informazioni sull’identità da diverse applicazioni Adobe, incluso ECID. Tramite l&#39;utilizzo di callback o promesse, è possibile gestire in modo programmatico gli ID recuperati correttamente e inviarli all&#39;API [!DNL Privacy Service].

Per ulteriori informazioni su [!DNL Privacy JS Library], inclusi esempi di codice per diversi casi d&#39;uso comuni, consulta la [Panoramica sulla libreria JS per la privacy](js-library.md).

## Passaggi successivi

Questo documento fornisce una breve panoramica dei concetti centrali coinvolti nel recupero dei dati di identità del cliente da utilizzare nelle richieste di accesso a dati personali. Per informazioni più dettagliate su questi concetti e servizi, si consiglia di consultare i collegamenti alla documentazione forniti in ciascuna sezione. Per i passaggi su come inviare gli ID recuperati a [!DNL Privacy Service] per la creazione di richieste di accesso, eliminazione o rinuncia alla vendita, consulta la [guida dell&#39;API Privacy Service](api/overview.md).
