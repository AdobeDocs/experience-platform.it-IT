---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;registro schema;registro schema;
solution: Experience Platform
title: Guida all’API del Registro di sistema dello schema
description: L’API del Registro di sistema dello schema consente agli sviluppatori di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) all’interno di Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: c2ca679e046f59d05e2d12ca83bc1b2496b2288f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 5%

---

# Guida dell’API di [!DNL Schema Registry]

L’ [!DNL Schema Registry] viene utilizzato per accedere alla libreria dello schema in Adobe Experience Platform, fornendo un’interfaccia utente e un’API RESTful da cui sono accessibili tutte le risorse della libreria disponibili.

L’API del Registro di sistema dello schema fornisce diversi endpoint che ti consentono di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) disponibili all’interno di Platform. Ciò include quelli definiti da Adobe, [!DNL Experience Platform] partner e fornitori le cui applicazioni utilizzi.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell&#39;endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

>[!IMPORTANT]
>
>XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati sulla customer experience acquisiti. Prima di utilizzare l&#39;API del Registro di sistema dello schema, si consiglia vivamente di consultare la [documentazione ufficiale dello schema JSON](https://json-schema.org/) per una migliore comprensione di questa tecnologia di base.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [riferimento API del Registro di sistema dello schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schemi

Gli schemi XDM rappresentano e convalidano la struttura e il formato dei dati acquisiti in Platform. Uno schema è composto da una classe e da zero o più gruppi di campi dello schema. Puoi creare, visualizzare, modificare ed eliminare gli schemi utilizzando l’endpoint `/schemas`. Per informazioni su come utilizzare questo endpoint, consulta la [guida all’endpoint degli schemi](./schemas.md).

Per una guida dettagliata su come creare uno schema completo nell’API del Registro di sistema dello schema, inclusa la creazione e l’aggiunta di gruppi di campi e tipi di dati, consulta l’ [esercitazione sulla creazione dello schema API](../tutorials/create-schema-api.md).

## Comportamenti

I comportamenti definiscono la natura dei dati descritti da uno schema. Ogni classe XDM deve fare riferimento a un comportamento specifico che tutti gli schemi che utilizzano tale classe erediteranno. Per informazioni su come visualizzare i comportamenti disponibili nell’API, consulta la [guida dell’endpoint per i comportamenti](./behaviors.md) .

## Classi

Una classe definisce la struttura di base delle proprietà comuni che devono contenere tutti gli schemi basati su tale classe e determina quali gruppi di campi sono idonei per essere utilizzati in tali schemi. Ogni classe deve essere associata a un comportamento esistente. Per informazioni dettagliate sulle operazioni con le classi nell&#39;API, consulta la [guida endpoint classi](./classes.md) .

## Gruppi di campi

I gruppi di campi sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo di posta o un ambiente browser web. I gruppi di campi sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). Per informazioni su come lavorare con i gruppi di campi nell’API, consulta la [guida endpoint dei gruppi di campi](./field-groups.md) .

## Tipi di dati

I tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei gruppi di campi allo stesso modo dei campi letterali di base, con una differenza chiave che consiste nel fatto che i tipi di dati possono definire più campi secondari. Sebbene siano simili ai gruppi di campi in quanto consentono un uso coerente di una struttura a più campi, i tipi di dati sono più flessibili perché possono essere inclusi in qualsiasi punto della struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo a livello principale. Per ulteriori informazioni sulle operazioni con i tipi di dati nell&#39;API, consulta la [guida endpoint per i tipi di dati](./data-types.md) .

## Descrittori

I descrittori sono set di metadati assegnati a campi specifici all’interno di uno schema, che forniscono vari dettagli contestuali, tra cui il modo in cui tali campi (e lo schema stesso) sono correlati ad altri schemi. A ogni schema può essere applicata una o più entità descrittore e sono disponibili diversi tipi di descrittori per scopi diversi. Per ulteriori informazioni sulle operazioni con i descrittori nell&#39;API, consulta la [guida all&#39;endpoint dei descrittori](./descriptors.md) e una panoramica dei diversi tipi di descrittori e dei relativi casi d&#39;uso.

## Unioni

Platform consente di comporre schemi per casi d’uso particolari, ma consente anche di comporre un’&quot;unione&quot; di schemi appartenenti a una classe specifica. Uno schema di unione aggrega i campi di tutti gli schemi che condividono la stessa classe in un’unica rappresentazione. Attivando uno schema da utilizzare con [Profilo cliente in tempo reale](../../profile/home.md), tale schema viene incluso nell&#39;unione per la relativa classe. Di conseguenza, gli schemi di unione non possono essere modificati direttamente e possono essere interessati solo dall’inclusione o dall’esclusione di schemi da utilizzare in Profilo.

Per informazioni su come visualizzare i sindacati nell&#39;API del Registro di sistema dello schema, consulta la [guida all&#39;endpoint dei sindacati](./unions.md).

## Esporta/Importa

L’API del Registro di sistema dello schema consente di trasferire e condividere risorse XDM tra sandbox e organizzazioni IMS. Per qualsiasi schema, gruppo di campi o tipo di dati, puoi generare un payload di esportazione contenente la struttura della risorsa e le risorse dipendenti. Questo payload può quindi essere utilizzato per importare la risorsa in una sandbox di destinazione e in un’organizzazione IMS.

Per ulteriori informazioni sull’utilizzo di questi endpoint, consulta la [guida all’esportazione/importazione](./export-import.md) .

## Dati di esempio

È possibile generare dati di esempio per qualsiasi schema specificato nella Libreria schema. L’oggetto di risposta restituito può quindi essere utilizzato come origine dell’inserimento dei dati.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la [guida per l&#39;endpoint di dati di esempio](./sample-data.md) .

## Registro di controllo

Il Registro di sistema dello schema mantiene un registro di tutte le modifiche apportate a una risorsa (classe, gruppo di campi, tipo di dati o schema) tra diversi aggiornamenti. Puoi recuperare il registro per una particolare risorsa fornendo il relativo `$id` o `meta:altId` nel percorso di una richiesta di GET a questo endpoint.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la [guida dell’endpoint del registro di controllo](./audit-log.md) .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API Schema Registry, leggi la [guida introduttiva](./getting-started.md) e seleziona una delle guide degli endpoint per capire come utilizzare endpoint specifici.
