---
title: Sviluppare un’estensione
description: Questo documento fornisce una panoramica generale del processo di sviluppo delle estensioni tag, con collegamenti verso la documentazione che descrive i processi in maggior dettaglio.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 94%

---

# Sviluppare un’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un’estensione tag può essere considerata come un (piccolo) prodotto con requisiti propri. È utile determinare in che modo un utente di Adobe Experience Platform potrebbe voler utilizzare l’estensione, e definire quindi di conseguenza le funzionalità e i tipi di eventi, condizioni, azioni ed elementi dati che tale estensione dovrà fornire.

Sulla base di queste informazioni, è possibile pianificare i componenti da fornire nell’estensione.

## Guide

Una volta delineato un piano, le guide seguenti saranno utili per comprendere il processo di sviluppo delle estensioni:

* La [guida introduttiva](../getting-started.md) e altri documenti in **Sviluppo delle estensioni** accessibili dalla barra di navigazione a sinistra sono ottimi materiali di riferimento per comprendere le estensioni. Includono dettagli su cosa possono fare le estensioni, come vengono memorizzate e trasmesse le informazioni dell’utente tra l’estensione e Adobe Experience Platform, come il codice viene raggruppato in librerie, e come il codice dell’estensione viene interpretato e utilizzato in fase di esecuzione nel browser.
* Il [video tutorial sulle estensioni](https://youtu.be/rxjtC9o4rl0) rappresenta un ottimo punto di partenza.
* La playlist YouTube di [introduzione alle estensioni](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) spiega come creare pacchetti di estensione.
* L’articolo [Understanding JSON Schema](https://spacetelescope.github.io/understanding-json-schema/index.html#) spiega lo schema JSON.
* Strumento di convalida [JSON Lint/Validator](https://jsonlint.com/).
* L’estensione [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) per Chrome consente di evidenziare e stampare il codice JSON e JSONP.
* L’editor [jsonschema.net](https://jsonschema.net/#/editor) facilita la creazione dello schema JSON dall’oggetto..
* [JSON Schema Validator](https://www.jsonschemavalidator.net) è uno strumento online interattivo per la convalida dello schema JSON.

## Strumenti

Sono inoltre disponibili diversi strumenti npm per lo sviluppo del pacchetto di estensione:

* Lo strumento [Extension Scaffold Tool](https://www.npmjs.com/package/@adobe/reactor-scaffold) consente di creare facilmente un progetto iniziale sul computer locale.
* [Tag Extension Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox) consente di convalidare le visualizzazioni e i moduli delle estensioni sul computer locale.
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) è un’utility per riga di comando che consente di creare il pacchetto di un’estensione tag come file.zip.
* [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader) è uno strumento interattivo per riga di comando che facilita l’immissione delle credenziali dell’account tecnico e il caricamento del pacchetto di estensione nei tag.
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) è uno strumento interattivo per riga di comando che consente di rilasciare l’estensione con disponibilità privata.

## Estensioni di esempio

Su Github sono disponibili alcune estensioni di esempio da esaminare o usare come progetti iniziali:

* [Estensione di esempio Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Estensione di esempio Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Estensione di esempio Typekit](https://github.com/jeffchasin/extension-typekit)
* [Estensione di esempio Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Workspace Slack

Puoi richiedere l’accesso all’area di lavoro della community su Slack, in cui gli autori delle estensioni possono supportarsi a vicenda, utilizzando questo [modulo di richiesta](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Nota**: a questa area di lavoro Slack partecipano anche alcuni membri di Adobe; tuttavia si tratta comunque di una risorsa della community che non è sponsorizzata né moderata da Adobe.
