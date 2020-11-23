---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guida per lo sviluppo API del Registro di sistema dello schema
description: 'L''API del Registro di sistema dello schema consente di gestire in modo programmatico tutti gli schemi e le relative risorse XDM disponibili all''interno  Experience Platform. '
topic: developer guide
translation-type: tm+mt
source-git-commit: d0e5865fddcf2592e9b6d8d4b2747bdceee6bda7
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# [!DNL Schema Registry] Guida per gli sviluppatori di API

Viene [!DNL Schema Registry] utilizzato per accedere alla libreria Schema all&#39;interno di Adobe Experience Platform, fornendo un&#39;interfaccia utente e un&#39;API RESTful da cui sono accessibili tutte le risorse libreria disponibili.

L&#39;API del Registro di sistema dello schema fornisce diversi endpoint che consentono di gestire in modo programmatico tutti gli schemi e le risorse XDM (Experience Data Model) correlate disponibili all&#39;interno della piattaforma. Ciò include quelli definiti da  Adobe, [!DNL Experience Platform] partner e fornitori le cui applicazioni vengono utilizzate.

Tali punti finali sono descritti di seguito. Per informazioni dettagliate, consultate le singole guide degli endpoint e la guida [](./getting-started.md) introduttiva per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

>[!IMPORTANT]
>
>XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati esperienza cliente acquisiti. Prima di utilizzare l&#39;API del Registro di sistema dello schema, si consiglia vivamente di consultare la documentazione [](https://json-schema.org/) ufficiale dello schema JSON per una migliore comprensione di questa tecnologia sottostante.

Per visualizzare tutti gli endpoint e le operazioni CRUD disponibili, visitare il riferimento [API del Registro di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)schema.

## Schemi

Gli schemi XDM rappresentano e convalidano la struttura e il formato dei dati acquisiti in Platform. Uno schema è composto da una classe e da zero o più mixin. Potete creare, visualizzare, modificare ed eliminare gli schemi utilizzando l’ `/schemas` endpoint. Per informazioni sull&#39;utilizzo di questo endpoint, consultate la guida [all&#39;endpoint](./schemas.md)degli schemi.

Per una guida dettagliata su come creare uno schema completo nell&#39;API del Registro di sistema dello schema, compresa la creazione e l&#39;aggiunta di mixin e tipi di dati, vedere l&#39;esercitazione [sulla creazione dello schema](../tutorials/create-schema-api.md)API.

## Classi

Le classi definiscono gli aspetti comportamentali dei dati che uno schema conterrà (record o serie temporali). Inoltre, una classe determina la struttura di base delle proprietà comuni che devono contenere tutti gli schemi basati su tale classe. La classe di uno schema determina quali mixin possono essere utilizzati in tale schema. Per informazioni dettagliate sull&#39;utilizzo delle classi nell&#39;API, consultate la guida [all&#39;endpoint delle](./classes.md) classi.

## Mixin

I mix sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo postale o un ambiente browser Web. Le mixine devono essere incluse come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). Consultate la guida [all&#39;endpoint dei](./mixins.md) mixin per apprendere come lavorare con i mixin nell&#39;API.

## Tipi di dati

I tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei mixin allo stesso modo dei campi letterali di base, con la differenza chiave che i tipi di dati possono definire più sottocampi. Anche se simili ai mixin in quanto consentono l&#39;uso coerente di una struttura multi-campo, i tipi di dati sono più flessibili perché possono essere inclusi ovunque nella struttura dello schema, mentre i mixin possono essere aggiunti solo a livello principale. Per ulteriori informazioni sull&#39;utilizzo dei tipi di dati nell&#39;API, consulta la guida [all&#39;endpoint dei tipi di](./data-types.md) dati.

## Descrittori

I descrittori sono insiemi di metadati a cui sono assegnati campi specifici all&#39;interno di uno schema, che forniscono vari dettagli contestuali, tra cui il modo in cui tali campi (e lo schema stesso) sono correlati ad altri schemi. A ogni schema possono essere applicate una o più entità descrittore e vi sono diversi tipi di descrittori diversi per scopi diversi. Per ulteriori informazioni sull&#39;utilizzo dei descrittori nell&#39;API, consultate la guida [all&#39;endpoint dei](./descriptors.md) descrittori e una panoramica dei diversi tipi di descrittori e dei relativi casi di utilizzo.

## Unioni

La piattaforma consente di comporre gli schemi per casi di utilizzo particolari, ma consente anche di comporre una &quot;unione&quot; di schemi appartenenti a una classe specifica. Uno schema unione aggrega i campi di tutti gli schemi che condividono la stessa classe in un&#39;unica rappresentazione. Abilitando uno schema da utilizzare con il profilo [cliente in tempo](../../profile/home.md)reale, tale schema viene incluso nell&#39;unione per la relativa classe. Di conseguenza, gli schemi di unione non possono essere modificati direttamente e possono essere modificati solo includendo o escludendo schemi da utilizzare in Profile.

Per informazioni su come visualizzare le unioni nell&#39;API del Registro di sistema dello schema, vedere la guida [all&#39;endpoint delle](./unions.md)unioni.

## Esporta/Importa

L&#39;API del Registro di sistema dello schema consente di trasferire e condividere risorse XDM tra le sandbox e le organizzazioni IMS. Per qualsiasi schema, mixin o tipo di dati, puoi generare un payload di esportazione contenente la struttura della risorsa e tutte le risorse dipendenti. Questo payload può quindi essere utilizzato per importare la risorsa in una sandbox di destinazione e in un&#39;organizzazione IMS.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consultate il riferimento [API del Registro di sistema dello](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schema.

## Dati di esempio

È possibile generare dati di esempio per qualsiasi schema specificato nella Libreria schema. L&#39;oggetto response restituito può quindi essere utilizzato come origine di inserimento dei dati.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consultate il riferimento [API del Registro di sistema dello](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schema.

## Registro di controllo

Il Registro di sistema dello schema mantiene un registro di tutte le modifiche apportate a una risorsa (classe, mixin, tipo di dati o schema) tra diversi aggiornamenti. È possibile recuperare il registro per una risorsa specifica fornendo il relativo `$id` o `meta:altId` nel percorso di una richiesta di GET a questo endpoint.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consultate il riferimento [API del Registro di sistema dello](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schema.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API del Registro di sistema dello schema, leggi la guida [](./getting-started.md) introduttiva e seleziona una delle guide dell&#39;endpoint per apprendere come utilizzare endpoint specifici.