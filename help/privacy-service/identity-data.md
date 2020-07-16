---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dati identità per richieste di privacy
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---


# Dati identità per richieste di privacy

Affinché  Adobe Experience Platform [!DNL Privacy Service] possa elaborare le richieste dei clienti per i loro dati privati (comprese le richieste di accesso, eliminazione o rinuncia alla vendita), è necessario fornire identificatori univoci che colleghino uno specifico cliente ai dati privati memorizzati nelle applicazioni abilitate Adobe Experience Cloud. [!DNL Privacy Service] quindi utilizza questi identificatori per raccogliere tutti i dati memorizzati sotto l&#39;identità del cliente all&#39;interno [!DNL Experience Cloud]ed elaborarli in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.

## Identità e spazi dei nomi

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da queste molteplici interazioni. Ciò a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nelle [!DNL Experience Cloud] applicazioni.

Ad esempio, durante la gestione delle richieste di dati dei clienti in [!DNL Privacy Service], un&#39;identità può rappresentare un valore di cookie impostato in un dominio controllato da Adobe, un valore di cookie in un dominio di terze parti condiviso con Adobe o un identificatore personalizzato definito esplicitamente all&#39;interno dell&#39;organizzazione IMS.

È pertanto necessario che ogni identità inviata a [!DNL Privacy Service] sia accompagnata da uno **spazio dei nomi** che fornisca contesto collegando il valore dell&#39;identità al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe  Advertising Cloud ID (&quot;AdCloud&quot;) o un  Adobe Target ID (&quot;TNTID&quot;).

 Adobe Experience Platform Identity Service conserva un archivio di spazi dei nomi di identità definiti a livello globale e definiti dall&#39;utente. Per informazioni più dettagliate sugli spazi dei nomi, consultate la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)identità. Per un elenco degli spazi dei nomi e dei qualificatori standard comunemente utilizzati in [!DNL Privacy Service], vedere la sezione [](api/appendix.md) appendice nella guida per gli sviluppatori.

## ECID e servizio di consenso

Adobe Experience Cloud [!DNL Identity Service] funge da framework di identificazione comune per [!DNL Experience Cloud]e assegna un ID univoco e costante a ciascun visitatore del sito. L&#39; [!DNL Experience Cloud] ID (ECID) monitora l&#39;attività di un cliente attraverso l&#39;uso di un cookie di prime parti, può identificare in modo univoco un dispositivo tra più applicazioni e consente di identificare lo stesso visitatore del sito e i relativi dati in diverse [!DNL Experience Cloud] applicazioni. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/it-IT/id-service/using/intro/overview.html) for more information.

Il servizio di consenso, un&#39;estensione di [!DNL Experience Cloud Identity Service], consente di impostare protocolli sull&#39;applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul servizio di consenso, comprese le modalità di configurazione del servizio per l&#39;applicazione, fare riferimento alla documentazione [del servizio di](https://docs.adobe.com/content/help/it-IT/id-service/using/implementation/opt-in-service/optin-overview.html)consenso.

Una volta assegnati ai visitatori del sito ECID, potete utilizzare Adobe [!DNL Privacy JavaScript Library] per recuperare tali ID da utilizzare nelle richieste di privacy, come descritto nella sezione successiva.

## [!DNL Privacy JS Library]

Il modulo [!DNL Adobe Privacy JavaScript Library] offre diverse funzioni che consentono di recuperare e rimuovere le identità dei clienti memorizzate nel browser. La libreria può essere configurata per recuperare informazioni di identità da diverse applicazioni Adobe, incluso ECID. Mediante callback o promesse potete gestire in modo programmatico gli ID recuperati e inviarli all&#39; [!DNL Privacy Service] API.

Per ulteriori informazioni [!DNL Privacy JS Library], compresi esempi di codice per diversi casi d’uso comuni, fare riferimento alla panoramica [della libreria](js-library.md)JS sulla privacy.

## Passaggi successivi

Questo documento ha fornito una breve panoramica dei concetti fondamentali relativi al recupero dei dati di identità dei clienti da utilizzare nelle richieste di privacy. Si consiglia di consultare i collegamenti della documentazione forniti in ciascuna sezione per informazioni più dettagliate su questi concetti e servizi. Per i passaggi su come inviare gli ID recuperati [!DNL Privacy Service] per creare richieste di accesso, eliminazione o rinuncia alla vendita, consultate la guida [per gli sviluppatori di](api/getting-started.md)Privacy Service.