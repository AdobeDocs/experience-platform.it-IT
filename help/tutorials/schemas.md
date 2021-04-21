---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Schemi e descrittori XDM
topic-legacy: tutorial
type: Tutorial
description: La standardizzazione e l'interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), basato su un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience. Gli schemi sono il modo standard per descrivere i dati in Experience Platform, consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all’interno di un’organizzazione e persino di essere condivisibili tra più organizzazioni.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Utilizzare gli schemi [!DNL Experience Data Model] (XDM) e i descrittori di relazione

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all’interno di un’organizzazione e persino di essere condivisibili tra più organizzazioni. Per ulteriori informazioni sugli schemi XDM, inizia leggendo la [Panoramica del sistema XDM](../xdm/home.md).

## Creare uno schema utilizzando il Registro di sistema dello schema

Il Registro di sistema dello schema fornisce un’interfaccia utente e un’API RESTful da cui è possibile visualizzare e gestire tutte le risorse nella Libreria schema di Adobe Experience Platform. La Libreria schema contiene le risorse rese disponibili dall&#39;Adobe, dai partner [!DNL Experience Platform] e dai fornitori le cui applicazioni vengono utilizzate, nonché le risorse definite e salvate nel Registro di sistema dello schema. Per scoprire come creare schemi per la tua organizzazione, segui le esercitazioni per [creare uno schema utilizzando l&#39;API del Registro di sistema dello schema](../xdm/tutorials/create-schema-api.md) o [creare uno schema utilizzando l&#39;interfaccia utente dell&#39;Editor schema](../xdm/tutorials/create-schema-ui.md).

## Definire una relazione tra due schemi

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante di Adobe Experience Platform. La definizione di queste relazioni all’interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di ottenere informazioni complesse sui dati dei clienti. Questi descrittori di relazione possono essere definiti utilizzando l&#39;API del Registro di sistema dello schema e l&#39;interfaccia utente dell&#39;Editor schema. Per ulteriori informazioni, consulta le esercitazioni per definire le relazioni tra due schemi [utilizzando l’API](../xdm/tutorials/relationship-api.md) o [utilizzando l’interfaccia utente](../xdm/tutorials/relationship-ui.md).

## Creare uno schema ad hoc

In circostanze specifiche, potrebbe essere necessario creare uno schema [!DNL Experience Data Model] (XDM) con campi che vengono spazi dei nomi per l’utilizzo solo da un singolo set di dati. Questo è denominato schema &quot;ad hoc&quot;. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro [inserimento dati](../ingestion/home.md) per [!DNL Experience Platform], inclusi l’acquisizione di file CSV e la creazione di alcuni tipi di connessioni sorgente [](../sources/home.md). La creazione di uno schema ad-hoc viene eseguita utilizzando l’API del Registro di sistema dello schema e deve essere utilizzata insieme ad altre esercitazioni [!DNL Experience Platform] che richiedono la creazione di uno schema ad-hoc come parte del flusso di lavoro. Per iniziare a creare uno schema ad-hoc, consulta l’esercitazione per [creare uno schema ad-hoc utilizzando l’API](../xdm/tutorials/ad-hoc.md).

## Passaggi successivi

Una volta definiti gli schemi per la tua organizzazione, puoi iniziare a creare set di dati in cui è possibile acquisire i dati. Per iniziare, consulta la seguente documentazione:

* [Panoramica dei set di dati](../catalog/datasets/overview.md)
* [Panoramica sull’acquisizione dei dati](../ingestion/home.md)
