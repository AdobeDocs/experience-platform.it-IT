---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dati identità per richieste di privacy
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Dati identità per richieste di privacy

Affinché Adobe Experience Platform Privacy Service possa elaborare le richieste dei clienti per i loro dati privati (comprese le richieste di accesso, eliminazione o rinuncia alla vendita), è necessario fornire identificatori univoci che colleghino uno specifico cliente ai dati privati memorizzati nelle applicazioni abilitate Adobe Experience Cloud. Il servizio per la privacy utilizza quindi questi identificatori per raccogliere tutti i dati memorizzati sotto l&#39;identità del cliente in Experience Cloud ed elaborarli in base alla richiesta del cliente.

Questo documento fornisce indicazioni generali su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.

## Identità e spazi dei nomi

Quando un cliente può interagire con il tuo marchio attraverso diversi canali, può essere difficile riconciliare i diversi identificatori registrati da queste molteplici interazioni. Ciò a sua volta può rendere difficile determinare quali dati appartengono a una particolare persona nelle applicazioni Experience Cloud.

Ad esempio, quando gestisci le richieste di dati dei clienti in Servizio privacy, un&#39;identità può rappresentare un valore di cookie impostato in un dominio controllato da Adobe, un valore di cookie in un dominio di terze parti condiviso con Adobe o un identificatore personalizzato che hai esplicitamente definito all&#39;interno dell&#39;organizzazione IMS.

È pertanto necessario che ogni identità inviata al Servizio Privacy sia accompagnata da uno **spazio dei nomi** che fornisca contesto, collegando il valore dell&#39;identità al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service conserva un archivio di spazi dei nomi di identità definiti a livello globale e definiti dall&#39;utente. Per informazioni più dettagliate sugli spazi dei nomi, consultate la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)identità. Per un elenco degli spazi dei nomi e dei qualificatori standard comunemente utilizzati nel servizio Privacy, consultate la sezione [](api/appendix.md) appendice della guida per gli sviluppatori.

## ECID e servizio di consenso

Il servizio Adobe Experience Cloud Identity Service funge da framework di identificazione comune per Experience Cloud e assegna un ID univoco e costante a ciascun visitatore del sito. L&#39;Experience Cloud ID (ECID) monitora l&#39;attività di un cliente tramite l&#39;uso di un cookie di prime parti, può identificare in modo univoco un dispositivo tra più applicazioni e consente di identificare lo stesso visitatore del sito e i relativi dati in diverse applicazioni Experience Cloud. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/it-IT/id-service/using/intro/overview.html) for more information.

Il servizio di consenso, un&#39;estensione del servizio Experience Cloud Identity, consente di impostare protocolli sull&#39;applicazione per consentire ai visitatori di determinare se è possibile impostare un cookie sul dispositivo o sul browser del visitatore. Per informazioni più dettagliate sul servizio di consenso, comprese le modalità di configurazione del servizio per l&#39;applicazione, fare riferimento alla documentazione [del servizio di](https://docs.adobe.com/content/help/it-IT/id-service/using/implementation/opt-in-service/optin-overview.html)consenso.

Una volta assegnati ai visitatori del sito ECID, potete utilizzare la libreria Adobe Privacy JavaScript per recuperare gli ID da usare nelle richieste di privacy, come descritto nella sezione successiva.

## Privacy JS Library

La libreria JavaScript per la privacy di Adobe offre diverse funzioni che consentono di recuperare e rimuovere le identità dei clienti memorizzate nel browser. La libreria può essere configurata per recuperare informazioni di identità da diverse applicazioni Adobe, incluso ECID. Mediante callback o promesse potete gestire in modo programmatico gli ID recuperati e inviarli all’API del servizio per la privacy.

Per ulteriori informazioni sulla Libreria JS per la privacy, compresi esempi di codice per diversi casi d&#39;uso comuni, fare riferimento alla panoramica [della Libreria JS per la](js-library.md)privacy.

## Passaggi successivi

Questo documento ha fornito una breve panoramica dei concetti fondamentali relativi al recupero dei dati di identità dei clienti da utilizzare nelle richieste di privacy. Si consiglia di consultare i collegamenti della documentazione forniti in ciascuna sezione per informazioni più dettagliate su questi concetti e servizi. Per informazioni sull&#39;invio degli ID recuperati al servizio Privacy per la creazione di richieste di accesso, eliminazione o rinuncia alla vendita, consultate la guida [per gli sviluppatori del servizio](api/getting-started.md)Privacy.