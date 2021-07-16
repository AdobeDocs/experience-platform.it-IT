---
title: Guida all’API del reattore
description: L’API di Reactor consente agli sviluppatori di gestire in modo programmatico tutte le risorse per i tag in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 1%

---

# [!DNL Reactor] Guida all’API

L’API Reactor fornisce diversi endpoint che consentono di gestire in modo programmatico tutte le risorse per i tag in Adobe Experience Platform.

Questi punti finali sono descritti di seguito. Per informazioni dettagliate, visita le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [riferimento API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml).

## Aziende

Un&#39;azienda rappresenta l&#39;organizzazione di un utente di tag, in genere un&#39;azienda. Queste aziende corrispondono a 1:1 con gli ID organizzazione IMS. Gli utenti API avranno visibilità solo nelle aziende a cui avranno accesso.

Per informazioni su come visualizzare le aziende disponibili nell’API, consulta la [guida endpoint società](./endpoints/companies.md) .

## Proprietà

Una proprietà è un contenitore che contiene la maggior parte delle altre risorse disponibili nell’API di Reactor. Le uniche risorse che non sono di proprietà di una proprietà sono eventi di audit, società, pacchetti di estensione e profili. Una proprietà appartiene esattamente a una società e un&#39;azienda può avere molte proprietà.

Per informazioni su come gestire le proprietà nell&#39;API, consulta la [guida all&#39;endpoint delle proprietà](./endpoints/properties.md) .

## Elementi dati

Un elemento dati funziona come una variabile che punta a un elemento importante di dati all’interno dell’applicazione. Gli elementi dati vengono utilizzati nelle configurazioni delle regole e delle estensioni. Quando la regola viene attivata in fase di runtime in un browser o in un’applicazione, il valore dell’elemento dati viene risolto e utilizzato all’interno della regola.

Per informazioni su come gestire gli elementi dati nell’API, consulta la [guida endpoint per gli elementi dati](./endpoints/data-elements.md) .

## Regole

Le regole controllano il comportamento delle risorse contenute in una libreria distribuita. Una regola è un gruppo di uno o più componenti della regola ed esiste per collegare i componenti della regola in modo logico.

Per informazioni su come gestire le regole nell&#39;API, consulta la [guida endpoint regole](./endpoints/rules.md) .

## Componenti della regola

I componenti delle regole sono i singoli elementi che compongono una regola. I componenti delle regole hanno tre tipi di base:

* **Eventi**: Cosa attiva una regola
* **Condizioni**: Controllo della regola per determinare un&#39;azione
* **Azioni**: Cosa viene eseguito dalla regola a seconda che la condizione sia soddisfatta

Per informazioni su come gestire le regole nell&#39;API, consulta la [guida endpoint regole](./endpoints/rules.md) .

## Pacchetti di estensione

Un pacchetto di estensione rappresenta un raggruppamento di singole funzionalità che possono essere rese disponibili a un utente di tag. Nella maggior parte dei casi queste funzionalità si presentano sotto forma di componenti regola ed elementi dati, ma possono anche includere moduli principali e moduli condivisi. Le funzionalità fornite da un pacchetto di estensione vengono installate come estensione quando viene incluso in una libreria.

Per informazioni su come gestire i pacchetti di estensione nell&#39;API, consulta la [guida endpoint per i pacchetti di estensione](./endpoints/extension-packages.md) .

## Estensioni

Un&#39;estensione rappresenta l&#39;istanza installata di un pacchetto di estensione. Un&#39;estensione rende disponibili a una proprietà le funzioni definite da un pacchetto di estensione. Queste funzioni vengono utilizzate durante la creazione di elementi dati e componenti regola.

Per informazioni su come gestire le estensioni nell’API, consulta la [guida all’endpoint delle estensioni](./endpoints/extensions.md) .

## Librerie

Una libreria è una raccolta di risorse (estensioni, regole ed elementi dati) che rappresentano il comportamento desiderato di una proprietà. Le librerie vengono compilate in build e tali build vengono assegnate a ambienti diversi mentre passano dal flusso di pubblicazione al flusso di pubblicazione, passando dal test alla produzione.

Per informazioni su come gestire le librerie nell’API, consulta la [guida endpoint delle librerie](./endpoints/libraries.md) .

## Build

Una libreria di tag viene compilata in una build per essere assegnata a un ambiente per i test e la distribuzione. Il contenuto di una build varia a seconda delle risorse incluse nella libreria, della configurazione dell’ambiente a cui è assegnata la build e della piattaforma della proprietà a cui appartiene la build.

Per informazioni su come gestire le build nell&#39;API, consulta la [guida all&#39;endpoint build](./endpoints/builds.md) .

## Ambienti

Un ambiente indica l’host specifico in cui è possibile distribuire una build e se la build deve essere distribuita come set di file o compressa in un formato di archivio. Nell’API di Reactor, gli ambienti sono separati dagli host stessi, che sono gestiti dall’endpoint `/hosts`.

Per informazioni su come gestire le build nell&#39;API, consulta la [guida all&#39;endpoint build](./endpoints/builds.md) .

## Host

Un host rappresenta una destinazione ospitata in cui è possibile distribuire e infine distribuire una build della libreria. Gli host possono essere server Akamai o SFTP.

Per informazioni su come gestire gli host nell’API, consulta la [guida endpoint host](./endpoints/hosts.md) .

## Configurazioni app

Le configurazioni dell’app consentono di memorizzare le credenziali e recuperarle per un utilizzo successivo. Per informazioni su come gestire le configurazioni dell’app nell’API, consulta la [guida endpoint per le configurazioni dell’app](./endpoints/app-configurations.md) .

## Eventi di controllo

Un evento di controllo è un record di una specifica modifica apportata a un’altra risorsa di tag, generata al momento della modifica. Si tratta di eventi di sistema a cui è possibile effettuare la sottoscrizione tramite una funzione di callback.

Per informazioni su come gestire gli eventi di controllo nell’API, consulta la [guida endpoint per gli eventi di controllo ](./endpoints/audit-events.md) .

## Callback

Un callback è un messaggio che Platform invia a un host URL ogni volta che viene generato un nuovo evento di controllo. Per informazioni su come gestire i callback nell’API, consulta la [guida all’endpoint dei callback](./endpoints/callbacks.md) .

## Note

Le note sono annotazioni testuali che possono essere aggiunte ad alcune risorse di tag, come elementi dati, estensioni, librerie, proprietà, regole e componenti regola. Per informazioni su come gestire le note nell&#39;API, consulta la [guida all&#39;endpoint delle note](./endpoints/notes.md) .

## Profilo

Un profilo contiene tutte le informazioni sull’utente connesso, comprese tutte le organizzazioni di Adobe a cui appartengono, i profili di prodotto a cui appartengono all’interno di ogni organizzazione e i diritti di cui dispongono da ciascun profilo di prodotto.

Per informazioni su come visualizzare queste informazioni nell’API, consulta la [guida all’endpoint del profilo](./endpoints/profile.md) .

## Cerca

L’endpoint `/search` fornisce un modo per trovare le risorse che corrispondono a un criterio desiderato, espresso come query. Tutte le query hanno ambito per la società corrente e le proprietà accessibili. Per informazioni sull’utilizzo di questa funzionalità, consulta la [guida all’endpoint di ricerca](./endpoints/search.md) .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API del Registro di sistema dello schema, leggi la [guida introduttiva](./getting-started.md) e seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare endpoint specifici.
