---
keywords: Experience Platform ;home;argomenti più comuni;ECID;ecid
solution: Experience Platform
title: Dati identità per richieste di privacy
topic: overview
description: Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare  tecnologie di Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---


# Dati identità per richieste di privacy

Affinché Adobe Experience Platform [!DNL Privacy Service] possa elaborare le richieste dei clienti per i propri dati privati (comprese le richieste di accesso, eliminazione o rinuncia alla vendita), deve essere fornito con identificatori univoci che collegano uno specifico cliente ai dati privati memorizzati nelle applicazioni abilitate per Adobe Experience Cloud. [!DNL Privacy Service] quindi utilizza questi identificatori per raccogliere tutti i dati memorizzati sotto l&#39;identità del cliente all&#39;interno  [!DNL Experience Cloud]ed elaborarli in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare  tecnologie di Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.

## Identità e spazi dei nomi

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da queste molteplici interazioni. Ciò a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nelle applicazioni [!DNL Experience Cloud].

Ad esempio, quando si gestiscono le richieste di dati dei clienti in [!DNL Privacy Service], un&#39;identità può rappresentare un valore di cookie impostato in un dominio controllato dal Adobe , un valore di cookie in un dominio di terze parti condiviso con  Adobe o un identificatore personalizzato esplicitamente definito all&#39;interno dell&#39;organizzazione IMS.

È pertanto necessario che ogni identità inviata a [!DNL Privacy Service] sia accompagnata da uno spazio dei nomi che fornisce contesto, collegando il valore dell&#39;identità al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o  Adobe Target ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service gestisce un archivio di spazi dei nomi di identità definiti a livello globale e definiti dall&#39;utente. Per informazioni più dettagliate sugli spazi dei nomi, vedere la [panoramica dello spazio dei nomi identità](../identity-service/namespaces.md). Per un elenco dei namespace standard e dei qualificatori dello spazio nomi comunemente utilizzati in [!DNL Privacy Service], consultare la sezione [appendice](api/appendix.md) nella guida per gli sviluppatori.

## ECID e servizio di consenso

Adobe Experience Cloud [!DNL Identity Service] funge da framework di identificazione comune per [!DNL Experience Cloud] e assegna un ID univoco e costante a ciascun visitatore del sito. L&#39; [!DNL Experience Cloud] ID (ECID) tiene traccia dell&#39;attività di un cliente attraverso l&#39;utilizzo di un cookie di prime parti, può identificare in modo univoco un dispositivo tra più applicazioni e consente di identificare lo stesso visitatore del sito e i relativi dati in diverse applicazioni [!DNL Experience Cloud]. Per ulteriori informazioni, vedere la [ Panoramica del servizio identità Experience Cloud](https://docs.adobe.com/content/help/it-IT/id-service/using/intro/overview.html).

Il servizio di consenso, un&#39;estensione di [!DNL Experience Cloud Identity Service], consente di impostare protocolli sull&#39;applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul servizio di consenso, comprese le modalità di configurazione del servizio per l&#39;applicazione, fare riferimento alla [documentazione del servizio di consenso](https://docs.adobe.com/content/help/it-IT/id-service/using/implementation/opt-in-service/optin-overview.html).

Una volta assegnati ai visitatori del sito ECID, potete utilizzare l&#39;Adobe  [!DNL Privacy JavaScript Library] per recuperare tali ID da utilizzare nelle richieste di privacy, come descritto nella sezione successiva.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] offre diverse funzioni che consentono di recuperare e rimuovere le identità dei clienti memorizzate nel browser. La libreria può essere configurata per recuperare informazioni di identità da diverse applicazioni  Adobe, incluso ECID. Mediante callback o promesse potete gestire in modo programmatico gli ID recuperati e inviarli all&#39;API [!DNL Privacy Service].

Per ulteriori informazioni su [!DNL Privacy JS Library], inclusi esempi di codice per diversi casi d&#39;uso comuni, fare riferimento alla [Panoramica della libreria JS sulla privacy](js-library.md).

## Passaggi successivi

Questo documento ha fornito una breve panoramica dei concetti fondamentali relativi al recupero dei dati di identità dei clienti da utilizzare nelle richieste di privacy. Si consiglia di consultare i collegamenti della documentazione forniti in ciascuna sezione per informazioni più dettagliate su questi concetti e servizi. Per istruzioni su come inviare gli ID recuperati a [!DNL Privacy Service] per creare richieste di accesso, eliminazione o rinuncia alla vendita, consultate la [guida per gli sviluppatori di Privacy Service ](api/getting-started.md).