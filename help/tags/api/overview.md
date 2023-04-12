---
title: Guida dell’API di Reactor
description: L’API di Reactor consente agli sviluppatori di gestire in modo programmatico tutte le risorse per i tag in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 94%

---

# Guida dell’API di [!DNL Reactor]

L’API di Reactor fornisce diversi endpoint che consentono di gestire in modo programmatico tutte le risorse per i tag in Adobe Experience Platform.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, consulta la [guida di riferimento per l’API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Aziende

Un’azienda rappresenta l’organizzazione di un utente di tag, in genere una divisione business. Queste aziende corrispondono a 1:1 con gli ID organizzazione. Gli utenti API hanno visibilità solo delle aziende a cui hanno accesso.

Per informazioni su come visualizzare le aziende disponibili nell’API, consulta la [guida dell’endpoint “companies”](./endpoints/companies.md).

## Proprietà

Una proprietà è un contenitore che raccoglie la maggior parte delle altre risorse disponibili nell’API di Reactor. Le uniche risorse che non appartengono a una proprietà sono eventi di controllo, società, pacchetti di estensione e profili. Una proprietà appartiene esattamente a una società e una società può avere molte proprietà.

Per informazioni su come gestire le proprietà nell’API, consulta la [guida dell’endpoint “properties”](./endpoints/properties.md).

## Elementi dati

Un elemento dati funziona come una variabile che punta a un elemento di dati importante nell’applicazione. Gli elementi dati vengono utilizzati nelle configurazioni delle regole e delle estensioni. Quando la regola viene attivata in fase di runtime in un browser o in un’applicazione, il valore dell’elemento dati viene risolto e utilizzato all’interno della regola.

Per informazioni su come gestire gli elementi dati nell’API, consulta la [guida dell’endpoint “data_elements”](./endpoints/data-elements.md).

## Regole

Le regole controllano il comportamento delle risorse contenute in una libreria distribuita. Una regola è un gruppo di uno o più componenti della regola ed esiste per collegare i componenti in modo logico.

Per informazioni su come gestire le regole nell’API, consulta la [guida dell’endpoint “rules”](./endpoints/rules.md).

## Componenti della regola

I componenti delle regole sono i singoli elementi che compongono una regola. I componenti delle regole hanno tre tipi di base:

* **Eventi**: cosa attiva una regola
* **Condizioni**: cosa viene verificato dalla regola per determinare un’azione
* **Azioni**: ciò che viene eseguito dalla regola a seconda che la condizione sia soddisfatta

Per informazioni su come gestire le regole nell’API, consulta la [guida dell’endpoint “rules”](./endpoints/rules.md).

## Pacchetti di estensione

Un pacchetto di estensione rappresenta un raggruppamento di singole funzionalità che possono essere rese disponibili a un utente di tag. Nella maggior parte dei casi queste funzionalità si presentano sotto forma di componenti regola ed elementi dati, ma possono anche includere moduli principali e moduli condivisi. Le funzionalità fornite da un pacchetto di estensione vengono installate come estensione quando sono incluse in una libreria.

Per informazioni su come gestire i pacchetti di estensione nell’API, consulta la [guida dell’endpoint “extension_packages”](./endpoints/extension-packages.md).

## Estensioni

Un’estensione rappresenta l’istanza installata di un pacchetto di estensione. Un’estensione rende disponibili a una proprietà le funzioni definite da un pacchetto di estensione. Queste funzioni vengono utilizzate durante la creazione di elementi dati e componenti regola.

Per informazioni su come gestire le estensioni nell’API, consulta la [guida dell’endpoint “extensions”](./endpoints/extensions.md).

## Librerie

Una libreria è una raccolta di risorse (estensioni, regole ed elementi dati) che rappresentano il comportamento desiderato di una proprietà. Le librerie vengono compilate in build e tali build vengono assegnate ad ambienti diversi mentre passano lungo il flusso di pubblicazione, dal test alla produzione.

Per informazioni su come gestire le librerie nell’API, consulta la [guida dell’endpoint “libraries”](./endpoints/libraries.md).

## Build

Una libreria di tag viene compilata come build per essere assegnata a un ambiente per i test e la distribuzione. Il contenuto di una build varia a seconda delle risorse incluse nella libreria, della configurazione dell’ambiente a cui è assegnata la build, e della piattaforma della proprietà a cui appartiene.

Per informazioni su come gestire le build nell’API, consulta la [guida dell’endpoint “builds”](./endpoints/builds.md).

## Ambienti

Un ambiente indica l’host specifico in cui è possibile distribuire una build, e se la build deve essere distribuita come set di file o compressa in un formato di archivio. Nell’API di Reactor, gli ambienti sono distinti dagli host stessi, che sono gestiti dall’endpoint `/hosts`.

Per informazioni su come gestire le build nell’API, consulta la [guida dell’endpoint “builds”](./endpoints/builds.md).

## Host

Un host rappresenta una destinazione ospitata in cui è possibile distribuire e infine implementare una build della libreria. Gli host possono essere server Akamai o SFTP.

Per informazioni su come gestire gli host nell’API, consulta la [guida dell’endpoint “hosts”](./endpoints/hosts.md).

## Configurazioni delle app

Le configurazioni dell’app consentono di memorizzare le credenziali e recuperarle per un utilizzo successivo. Per informazioni su come gestire le configurazioni di app nell’API, consulta la [guida dell’endpoint “app_configurations”](./endpoints/app-configurations.md).

## Eventi di audit

Un evento di controllo è un record di una specifica modifica apportata a un’altra risorsa tag, generata al momento della modifica. Si tratta di eventi di sistema a cui è possibile abbonarsi tramite una funzione di callback.

Per informazioni su come gestire gli eventi di controllo nell’API, consulta la [guida dell’endpoint “audit events”](./endpoints/audit-events.md).

## Callback

Un callback è un messaggio che Platform invia a un host URL ogni volta che viene generato un nuovo evento di audit. Per informazioni su come gestire i callback nell’API, consulta la [guida dell’endpoint “callbacks”](./endpoints/callbacks.md).

## Note

Le note sono annotazioni testuali che possono essere aggiunte ad alcune risorse tag, come elementi dati, estensioni, librerie, proprietà, regole e componenti regola. Per informazioni su come gestire le note nell’API, consulta la [guida dell’endpoint “notes”](./endpoints/notes.md).

## Profilo

Un profilo contiene tutte le informazioni sull’utente connesso, comprese tutte le organizzazioni Adobe e i profili di prodotto all’interno di ogni organizzazione a cui apparttiene, e le autorizzazioni di cui dispone per ciascun profilo di prodotto.

Per informazioni su come visualizzare queste informazioni nell’API, consulta la [guida dell’endpoint “profile”](./endpoints/profile.md).

## Cerca

L’endpoint `/search` fpermette di trovare le risorse che corrispondono a un dato criterio, espresso come query. Tutte le query prendono in esame la società corrente e le proprietà accessibili. Per informazioni sull’utilizzo di questa funzionalità, consulta la [guida dell’endpoint “search”](./endpoints/search.md).

## Segreti

Un segreto contiene credenziali che consentono l&#39;inoltro degli eventi per l&#39;autenticazione in un altro sistema per lo scambio sicuro dei dati. Consulta la sezione [guida ai segreti](./guides/secrets.md) per una panoramica del funzionamento dei segreti nell&#39;inoltro degli eventi e [guida all’endpoint segreti](./endpoints/secrets.md) per scoprire come gestirli nell’API di Reactor.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API Schema Registry, leggi la [guida introduttiva](./getting-started.md) e seleziona una delle guide degli endpoint per capire come utilizzare endpoint specifici.
