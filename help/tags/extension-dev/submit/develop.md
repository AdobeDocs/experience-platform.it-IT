---
title: Sviluppare un’estensione
description: Questo documento fornisce una panoramica generale del processo di sviluppo dell’estensione dei tag con collegamenti ad ulteriore documentazione per processi più dettagliati.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 43%

---

# Sviluppare un’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un’estensione tag deve essere pensata come un prodotto (piccolo) con i propri requisiti. È utile determinare in che modo un utente di Adobe Experience Platform potrebbe voler utilizzare l’estensione, e definire quindi di conseguenza le funzionalità e i tipi di eventi, condizioni, azioni ed elementi dati che tale estensione dovrà fornire.

Con questa conoscenza, puoi pianificare quali componenti devono essere forniti nell’estensione.

## Guide

Una volta delineato un piano, le guide seguenti saranno utili per comprendere il processo di sviluppo delle estensioni:

* La [guida introduttiva](../getting-started.md) e altri documenti in **Sviluppo estensioni** nella navigazione a sinistra sono ottimi materiali di riferimento per comprendere le estensioni. Includono dettagli su cosa possono fare le estensioni, come vengono memorizzate e trasmesse le informazioni utente tra l&#39;estensione e Adobe Experience Platform, come il codice viene raggruppato nelle librerie e come il codice di estensione viene interpretato e utilizzato in fase di esecuzione nel browser.
* Il video tutorial [estensione](https://youtu.be/rxjtC9o4rl0) è un ottimo punto di partenza.
* La playlist YouTube di [introduzione alle estensioni](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) spiega come creare pacchetti di estensione.
* L’articolo [Understanding JSON Schema](https://spacetelescope.github.io/understanding-json-schema/index.html#) spiega lo schema JSON.
* Strumento di convalida [JSON Lint/Validator](http://jsonlint.com/).
* L’estensione [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) per Chrome consente di evidenziare e stampare il codice JSON e JSONP.
* L’editor [jsonschema.net](https://jsonschema.net/#/editor) facilita la creazione dello schema JSON dall’oggetto..
* [JSON Schema Validator](http://www.jsonschemavalidator.net/) è uno strumento online interattivo per la convalida dello schema JSON.

## Strumenti

Sono inoltre disponibili diversi strumenti npm per lo sviluppo del pacchetto di estensione:

* [Lo ](https://www.npmjs.com/package/@adobe/reactor-scaffold) strumento di scaffolding dell’estensione tag consente di creare facilmente un progetto iniziale sul computer locale.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-sandbox) Sandbox ti aiuta a convalidare le visualizzazioni e i moduli di estensione sul computer locale.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-packager) Packagerè un&#39;utilità a riga di comando per creare il pacchetto di un&#39;estensione di tag in un file zip.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-uploader) Uploaderè uno strumento interattivo della riga di comando per aiutarti a inserire le credenziali del tuo account tecnico e caricare il pacchetto di estensione sui tag.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-releaser) Releaser è uno strumento interattivo della riga di comando per aiutarti a rilasciare l’estensione a disponibilità privata.

## Estensioni di esempio

Esistono estensioni di esempio su GitHub che puoi esaminare o utilizzare come progetti iniziali:

* [Estensione di esempio Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Estensione di esempio Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Estensione di esempio Typekit](https://github.com/jeffchasin/extension-typekit)
* [Estensione di esempio Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Workspace Slack

Puoi richiedere l&#39;accesso all&#39;area di lavoro della community di Slack in cui gli autori delle estensioni possono supportarsi a vicenda utilizzando questo [modulo di richiesta](http://join.launchdevelopers.chat).

**Nota**: mentre ci sono membri di Adobe in questo spazio di lavoro Slack, è una risorsa community non sponsorizzata o moderata da Adobe.
