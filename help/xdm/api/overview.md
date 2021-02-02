---
keywords: ' Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;schema Registro di sistema;schema;'
solution: Experience Platform
title: Guida per lo sviluppo API del Registro di sistema dello schema
description: 'L''API del Registro di sistema dello schema consente di gestire in modo programmatico tutti gli schemi e le relative risorse XDM disponibili all''interno  Experience Platform. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 44a727f6ce4c2b90aa010379583c7c4d3ebd011c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Schema Registry] Guida per gli sviluppatori di API

[!DNL Schema Registry] viene utilizzato per accedere alla libreria Schema all&#39;interno di Adobe Experience Platform, fornendo un&#39;interfaccia utente e RESTful API da cui sono accessibili tutte le risorse libreria disponibili.

L&#39;API del Registro di sistema dello schema fornisce diversi endpoint che consentono di gestire in modo programmatico tutti gli schemi e le risorse XDM (Experience Data Model) correlate disponibili all&#39;interno della piattaforma. Ciò include quelli definiti da  Adobe, [!DNL Experience Platform] partner e fornitori le cui applicazioni vengono utilizzate.

Tali punti finali sono descritti di seguito. Per informazioni dettagliate, visitate le singole guide degli endpoint e fate riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

>[!IMPORTANT]
>
>XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati esperienza cliente acquisiti. Prima di lavorare con l&#39;API del Registro di sistema dello schema, si consiglia vivamente di consultare la [documentazione ufficiale dello schema JSON](https://json-schema.org/) per una migliore comprensione di questa tecnologia sottostante.

Per visualizzare tutti gli endpoint e le operazioni CRUD disponibili, visitare il [Riferimento API del Registro di sistema dello schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schemi

Gli schemi XDM rappresentano e convalidano la struttura e il formato dei dati acquisiti in Platform. Uno schema è composto da una classe e da zero o più mixin. Potete creare, visualizzare, modificare ed eliminare gli schemi utilizzando l&#39;endpoint `/schemas`. Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, vedere la [guida dell&#39;endpoint degli schemi](./schemas.md).

Per una guida dettagliata su come creare uno schema completo nell&#39;API del Registro di sistema dello schema, compresa la creazione e l&#39;aggiunta di mixin e tipi di dati, vedere l&#39; [esercitazione sulla creazione dello schema API](../tutorials/create-schema-api.md).

## Comportamenti

I comportamenti definiscono la natura dei dati che uno schema descrive. Ogni classe XDM deve fare riferimento a un comportamento specifico che tutti gli schemi che utilizzano tale classe erediteranno. Per informazioni su come visualizzare i comportamenti disponibili nell&#39;API, vedere la [guida dell&#39;endpoint di comportamento](./behaviors.md).

## Classi

Una classe definisce la struttura di base delle proprietà comuni che devono contenere tutti gli schemi basati su tale classe e determina quali mixin possono essere utilizzati in tali schemi. Ogni classe deve essere associata a un comportamento esistente. Per informazioni sull&#39;utilizzo delle classi nell&#39;API, vedere la guida [endpoint delle classi](./classes.md).

## Mixin

I mix sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo postale o un ambiente browser Web. Le mixine devono essere incluse come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). Per informazioni sull&#39;utilizzo dei mixin nelle API, vedere la [guida dell&#39;endpoint dei mixin](./mixins.md).

## Tipi di dati

I tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei mixin allo stesso modo dei campi letterali di base, con la differenza chiave che i tipi di dati possono definire più sottocampi. Anche se simili ai mixin in quanto consentono l&#39;uso coerente di una struttura multi-campo, i tipi di dati sono più flessibili perché possono essere inclusi ovunque nella struttura dello schema, mentre i mixin possono essere aggiunti solo a livello principale. Per ulteriori informazioni sull&#39;utilizzo dei tipi di dati nell&#39;API, vedere la [guida dell&#39;endpoint ](./data-types.md).

## Descrittori

I descrittori sono insiemi di metadati assegnati a campi specifici all&#39;interno di uno schema, che forniscono vari dettagli contestuali, tra cui il modo in cui tali campi (e lo schema stesso) sono correlati ad altri schemi. A ogni schema possono essere applicate una o più entità descrittore e vi sono diversi tipi di descrittori diversi per scopi diversi. Per ulteriori informazioni sull&#39;utilizzo dei descrittori nell&#39;API, consultate la [guida dell&#39;endpoint dei descrittori](./descriptors.md) e una panoramica dei diversi tipi di descrittori e dei relativi casi di utilizzo.

## Unioni

La piattaforma consente di comporre gli schemi per casi di utilizzo particolari, ma consente anche di comporre una &quot;unione&quot; di schemi appartenenti a una classe specifica. Uno schema unione aggrega i campi di tutti gli schemi che condividono la stessa classe in un&#39;unica rappresentazione. Abilitando uno schema da utilizzare con [Profilo cliente in tempo reale](../../profile/home.md), tale schema viene incluso nell&#39;unione per la classe specifica. Di conseguenza, gli schemi di unione non possono essere modificati direttamente e possono essere modificati solo includendo o escludendo schemi da utilizzare in Profile.

Per informazioni su come visualizzare le unioni nell&#39;API del Registro di sistema dello schema, vedere la [guida dell&#39;endpoint delle unioni](./unions.md).

## Esporta/Importa

L&#39;API del Registro di sistema dello schema consente di trasferire e condividere risorse XDM tra le sandbox e le organizzazioni IMS. Per qualsiasi schema, mixin o tipo di dati, puoi generare un payload di esportazione contenente la struttura della risorsa e tutte le risorse dipendenti. Questo payload può quindi essere utilizzato per importare la risorsa in una sandbox di destinazione e in un&#39;organizzazione IMS.

Per ulteriori informazioni sull&#39;utilizzo di questi endpoint, vedere la guida [export/import endpoint](./export-import.md).

## Dati di esempio

È possibile generare dati di esempio per qualsiasi schema specificato nella Libreria schema. L&#39;oggetto response restituito può quindi essere utilizzato come origine di inserimento dei dati.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, vedere la [guida dell&#39;endpoint di dati di esempio](./sample-data.md).

## Registro di controllo

Il Registro di sistema dello schema mantiene un registro di tutte le modifiche apportate a una risorsa (classe, mixin, tipo di dati o schema) tra diversi aggiornamenti. È possibile recuperare il registro di una risorsa specifica fornendo il relativo `$id` o `meta:altId` nel percorso di una richiesta di GET a questo endpoint.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, vedere la [guida dell&#39;endpoint del registro di controllo](./audit-log.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API del Registro di sistema dello schema, leggi la [guida introduttiva](./getting-started.md), quindi seleziona una delle guide dell&#39;endpoint per apprendere come utilizzare endpoint specifici.