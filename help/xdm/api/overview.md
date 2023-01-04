---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;registro schema;registro schema;
solution: Experience Platform
title: Guida all’API del Registro di sistema dello schema
description: L’API del Registro di sistema dello schema consente agli sviluppatori di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) all’interno di Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 5%

---

# Guida dell’API di [!DNL Schema Registry]

La [!DNL Schema Registry] viene utilizzato per accedere alla Libreria schema in Adobe Experience Platform, fornendo un&#39;interfaccia utente e un&#39;API RESTful da cui sono accessibili tutte le risorse della libreria disponibili.

L’API del Registro di sistema dello schema fornisce diversi endpoint che ti consentono di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) disponibili all’interno di Platform. Ciò include quelli definiti dall&#39;Adobe, [!DNL Experience Platform] partner e fornitori di cui utilizzi le applicazioni.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell’endpoint e fai riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

>[!IMPORTANT]
>
>XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati sulla customer experience acquisiti. Prima di lavorare con l&#39;API del Registro di sistema dello schema, si consiglia vivamente di rivedere il [documentazione ufficiale dello schema JSON](https://json-schema.org/) per una migliore comprensione di questa tecnologia di base.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [Riferimento API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schemi

Gli schemi XDM rappresentano e convalidano la struttura e il formato dei dati acquisiti in Platform. Uno schema è composto da una classe e da zero o più gruppi di campi dello schema. Puoi creare, visualizzare, modificare ed eliminare gli schemi utilizzando la funzione `/schemas` punto finale. Per informazioni su come utilizzare questo endpoint, consulta la sezione [guida all’endpoint degli schemi](./schemas.md).

Per una guida dettagliata su come creare uno schema completo nell’API del Registro di sistema dello schema, inclusa la creazione e l’aggiunta di gruppi di campi e tipi di dati, consulta la sezione [Esercitazione sulla creazione di uno schema API](../tutorials/create-schema-api.md).

## Comportamenti

I comportamenti definiscono la natura dei dati descritti da uno schema. Ogni classe XDM deve fare riferimento a un comportamento specifico che tutti gli schemi che utilizzano tale classe erediteranno. Consulta la sezione [guida all’endpoint dei comportamenti](./behaviors.md) per scoprire come visualizzare i comportamenti disponibili nell’API.

## Classi

Una classe definisce la struttura di base delle proprietà comuni che devono contenere tutti gli schemi basati su tale classe e determina quali gruppi di campi sono idonei per essere utilizzati in tali schemi. Ogni classe deve essere associata a un comportamento esistente. Consulta la sezione [guida all&#39;endpoint delle classi](./classes.md) per informazioni sulle operazioni con le classi nell’API.

## Gruppi di campi

I gruppi di campi sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo di posta o un ambiente browser web. I gruppi di campi sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). Consulta la sezione [guida all’endpoint dei gruppi di campi](./field-groups.md) per scoprire come lavorare con i gruppi di campi nell’API.

## Tipi di dati

I tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei gruppi di campi allo stesso modo dei campi letterali di base, con una differenza chiave che consiste nel fatto che i tipi di dati possono definire più campi secondari. Sebbene siano simili ai gruppi di campi in quanto consentono un uso coerente di una struttura a più campi, i tipi di dati sono più flessibili perché possono essere inclusi in qualsiasi punto della struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo a livello principale. Consulta la sezione [guida all’endpoint dei tipi di dati](./data-types.md) per ulteriori informazioni sulle operazioni con i tipi di dati nell’API.

## Descrittori

I descrittori sono set di metadati assegnati a campi specifici all’interno di uno schema, che forniscono vari dettagli contestuali, tra cui il modo in cui tali campi (e lo schema stesso) sono correlati ad altri schemi. A ogni schema può essere applicata una o più entità descrittore e sono disponibili diversi tipi di descrittori per scopi diversi. Consulta la sezione [guida all&#39;endpoint dei descrittori](./descriptors.md) per ulteriori informazioni sull’utilizzo dei descrittori nell’API e una panoramica dei diversi tipi di descrittori e dei relativi casi d’uso.

## Unioni

Platform consente di comporre schemi per casi d’uso particolari, ma consente anche di comporre un’&quot;unione&quot; di schemi appartenenti a una classe specifica. Uno schema di unione aggrega i campi di tutti gli schemi che condividono la stessa classe in un’unica rappresentazione. Attivando uno schema da utilizzare con [Profilo cliente in tempo reale](../../profile/home.md), tale schema viene incluso nell&#39;unione per la relativa classe specifica. Di conseguenza, gli schemi di unione non possono essere modificati direttamente e possono essere interessati solo dall’inclusione o dall’esclusione di schemi da utilizzare in Profilo.

Per informazioni su come visualizzare le unioni nell’API del Registro di sistema dello schema, consulta [guida all’endpoint sindacati](./unions.md).

## Conversione da CSV a schema {#csv-to-schema}

Puoi generare automaticamente uno schema XDM utilizzando un file CSV come modello, per creare modelli che importino in blocco i campi dello schema e tagliano le operazioni manuali di API o interfaccia utente.

Consulta la sezione [Guida all’endpoint di conversione da CSV a schema](./export.md) per ulteriori informazioni.

## Esporta {#export}

L’API del Registro di sistema dello schema consente di trasferire e condividere risorse XDM tra sandbox e organizzazioni IMS. Per qualsiasi schema, gruppo di campi o tipo di dati, puoi generare un payload di esportazione contenente la struttura della risorsa e le risorse dipendenti. Questo payload può quindi essere utilizzato per importare la risorsa in una sandbox di destinazione e in un’organizzazione IMS.

Consulta la sezione [guida all’endpoint per l’esportazione](./export.md) per ulteriori informazioni su come creare un payload di esportazione per una risorsa XDM esistente.

## Importa

Se utilizzi [esportare](#export) o [Conversione da CSV a schema](./import.md) gli endpoint per creare un payload di esportazione, puoi inviare tale payload a un’organizzazione di destinazione e a una sandbox per importare le risorse specificate.

Consulta la sezione [guida all’importazione di endpoint](./export.md) per ulteriori informazioni su come generare risorse XDM dai payload di esportazione.

## Dati di esempio

È possibile generare dati di esempio per qualsiasi schema specificato nella Libreria schema. L’oggetto di risposta restituito può quindi essere utilizzato come origine dell’inserimento dei dati.

Consulta la sezione [guida all’endpoint dati di esempio](./sample-data.md) per ulteriori informazioni sull&#39;utilizzo di questo endpoint.

## Registro di controllo

Il Registro di sistema dello schema mantiene un registro di tutte le modifiche apportate a una risorsa (classe, gruppo di campi, tipo di dati o schema) tra diversi aggiornamenti. Puoi recuperare il registro per una particolare risorsa fornendo il relativo `$id` o `meta:altId` nel percorso di una richiesta GET a questo endpoint.

Consulta la sezione [guida all’endpoint del registro di controllo](./audit-log.md) per ulteriori informazioni sull&#39;utilizzo di questo endpoint.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API Schema Registry, leggi la [guida introduttiva](./getting-started.md) e seleziona una delle guide degli endpoint per capire come utilizzare endpoint specifici.
