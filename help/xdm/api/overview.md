---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;Experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guida API del registro dello schema
description: L’API Schema Registry consente agli sviluppatori di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) all’interno di Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 5%

---

# Guida dell’API di [!DNL Schema Registry]

Il [!DNL Schema Registry] viene utilizzato per accedere alla libreria di schemi in Adobe Experience Platform, fornendo un’interfaccia utente e un’API RESTful da cui tutte le risorse della libreria disponibili sono accessibili.

L’API Schema Registry fornisce diversi endpoint che consentono di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) disponibili in Platform. Sono inclusi quelli definiti dall&#39;Adobe, [!DNL Experience Platform] partner e fornitori di cui utilizzi le applicazioni.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

>[!IMPORTANT]
>
>XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati acquisiti sull’esperienza del cliente. Prima di lavorare con l’API Schema Registry, è consigliabile rivedere [Documentazione ufficiale sullo schema JSON](https://json-schema.org/) per comprendere meglio questa tecnologia di base.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [Riferimento API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schemi

Gli schemi XDM rappresentano e convalidano la struttura e il formato dei dati acquisiti in Platform. Uno schema è composto da una classe e da zero o più gruppi di campi dello schema. Puoi creare, visualizzare, modificare ed eliminare gli schemi utilizzando `/schemas` endpoint. Per informazioni su come utilizzare questo endpoint, consulta [guida all’endpoint degli schemi](./schemas.md).

Per una guida dettagliata su come creare manualmente uno schema completo nell’API Schema Registry, inclusa la creazione e l’aggiunta di gruppi di campi e tipi di dati, consulta la sezione [Tutorial sulla creazione di schemi API](../tutorials/create-schema-api.md).

Se acquisisci dati CSV, consulta la sezione su [Conversione da CSV a schema](#csv-to-schema).

## Comportamenti

I comportamenti definiscono la natura dei dati descritti da uno schema. Ogni classe XDM deve fare riferimento a un comportamento specifico che verrà ereditato da tutti gli schemi che utilizzano tale classe. Consulta la [guida dell’endpoint &quot;behaviors&quot;](./behaviors.md) per scoprire come visualizzare i comportamenti disponibili nell’API.

## Classi

Una classe definisce la struttura di base delle proprietà comuni che tutti gli schemi basati su tale classe devono contenere e determina quali gruppi di campi sono idonei per l’utilizzo in tali schemi. Ogni classe deve essere associata a un comportamento esistente. Consulta la [guida dell’endpoint &quot;classes&quot;](./classes.md) per informazioni dettagliate sull’utilizzo delle classi nell’API.

## Gruppi di campi

I gruppi di campi sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo postale o un ambiente di browser web. I gruppi di campi sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). Consulta la [guida dell’endpoint &quot;field groups&quot;](./field-groups.md) per scoprire come utilizzare i gruppi di campi nell’API.

## Tipi di dati

I tipi di dati vengono utilizzati come campi del tipo di riferimento nelle classi o nei gruppi di campi allo stesso modo dei campi letterali di base, con la differenza fondamentale che i tipi di dati possono definire più sottocampi. Sebbene siano simili ai gruppi di campi in quanto consentono l’utilizzo coerente di una struttura a più campi, i tipi di dati sono più flessibili in quanto possono essere inclusi ovunque nella struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo al livello principale. Consulta la [guida dell’endpoint &quot;data types&quot;](./data-types.md) per ulteriori informazioni sull’utilizzo dei tipi di dati nell’API.

## Descrittori

I descrittori sono insiemi di metadati assegnati a campi specifici all’interno di uno schema, che forniscono vari dettagli contestuali, tra cui il modo in cui tali campi (e lo schema stesso) sono correlati ad altri schemi. A ogni schema possono essere applicate una o più entità descrittive ed esistono diversi tipi di descrittori per scopi diversi. Consulta la [guida dell’endpoint &quot;descriptors&quot;](./descriptors.md) per ulteriori informazioni sull’utilizzo dei descrittori nell’API e una panoramica dei diversi tipi di descrittori e dei relativi casi d’uso.

## Unioni

Platform consente di comporre schemi per casi d’uso specifici, ma consente anche di comporre un’&quot;unione&quot; di schemi appartenenti a una classe specifica. Uno schema di unione aggrega i campi di tutti gli schemi che condividono la stessa classe in un’unica rappresentazione. Attivando uno schema da utilizzare con [Profilo cliente in tempo reale](../../profile/home.md), tale schema viene incluso nell’unione per la relativa classe specifica. Di conseguenza, gli schemi di unione non possono essere modificati direttamente e possono essere interessati solo dall’inclusione o esclusione di schemi da utilizzare nel profilo.

Per informazioni su come visualizzare le unioni nell’API del registro dello schema, consulta [guida dell’endpoint &quot;unions&quot;](./unions.md).

## Conversione da CSV a schema {#csv-to-schema}

Puoi generare automaticamente uno schema XDM utilizzando come modello un file CSV, che ti consente di creare modelli per importare in blocco i campi dello schema e ridurre il lavoro manuale dell’API o dell’interfaccia utente.

Consulta la [Guida dell’endpoint di conversione da CSV a schema](./export.md) per ulteriori informazioni.

>[!NOTE]
>
>Puoi anche utilizzare l’interfaccia utente per [mappare un CSV a uno schema utilizzando i consigli generati dall’intelligenza artificiale](../../ingestion/tutorials/map-csv/recommendations.md) (attualmente in versione beta).

## Esporta {#export}

L’API Schema Registry consente di trasferire e condividere risorse XDM tra sandbox e organizzazioni. Per qualsiasi schema, gruppo di campi o tipo di dati, puoi generare un payload di esportazione contenente la struttura della risorsa ed eventuali risorse dipendenti. Questo payload può quindi essere utilizzato per importare la risorsa in una sandbox e in un’organizzazione di destinazione.

Consulta la [guida dell’endpoint di esportazione](./export.md) per ulteriori informazioni su come creare un payload di esportazione per una risorsa XDM esistente.

## Importa

Se si utilizza [esportare](#export) o [Conversione da CSV a schema](./import.md) endpoint per creare un payload di esportazione, puoi inviare tale payload a un’organizzazione target e a una sandbox per importare le risorse specificate.

Consulta la [importa guida dell’endpoint](./export.md) per ulteriori informazioni su come generare risorse XDM dai payload di esportazione.

## Dati di esempio

È possibile generare dati di esempio per qualsiasi schema specificato all&#39;interno della Raccolta schemi. L’oggetto di risposta restituito può quindi essere utilizzato come origine dell’acquisizione dei dati.

Consulta la [guida di esempio dell’endpoint dati](./sample-data.md) per ulteriori informazioni sull’utilizzo di questo endpoint.

## Registro di controllo

Il registro degli schemi gestisce un registro di tutte le modifiche apportate a una risorsa (classe, gruppo di campi, tipo di dati o schema) tra diversi aggiornamenti. Per recuperare il registro di una particolare risorsa, fornisci i `$id` o `meta:altId` nel percorso di una richiesta GET a questo endpoint.

Consulta la [guida dell’endpoint del registro di controllo](./audit-log.md) per ulteriori informazioni sull’utilizzo di questo endpoint.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API Schema Registry, leggi la [guida introduttiva](./getting-started.md) e seleziona una delle guide degli endpoint per capire come utilizzare endpoint specifici.
