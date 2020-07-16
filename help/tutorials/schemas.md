---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schemi e descrittori XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Utilizzare gli schemi [!DNL Experience Data Model] (XDM) e i descrittori delle relazioni

Standardizzazione e interoperabilità sono concetti chiave  Adobe Experience Platform. [!DNL Experience Data Model] (XDM), guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all&#39;interno di un&#39;organizzazione e persino di essere condivisibili tra più organizzazioni. Per ulteriori informazioni sugli schemi XDM, consultare la panoramica [](../xdm/home.md)XDM System.

## Creare uno schema utilizzando il Registro di sistema dello schema

Il Registro di sistema dello schema fornisce un&#39;interfaccia utente e RESTful API da cui è possibile visualizzare e gestire tutte le risorse nella  Libreria schema Adobe Experience Platform. La Libreria schema contiene le risorse messe a disposizione da Adobe, [!DNL Experience Platform] partner e fornitori le cui applicazioni vengono utilizzate, nonché le risorse definite e salvate nel Registro di sistema dello schema. Per apprendere come creare schemi per l&#39;organizzazione, seguire le esercitazioni per [creare uno schema utilizzando l&#39;API](../xdm/tutorials/create-schema-api.md) del Registro di sistema dello schema o per [creare uno schema utilizzando l&#39;interfaccia](../xdm/tutorials/create-schema-ui.md)utente dell&#39;Editor di schema.

## Definire una relazione tra due schemi

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante del  Adobe Experience Platform. La definizione di queste relazioni all&#39;interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di acquisire informazioni complesse sui dati dei clienti. Questi descrittori di relazione possono essere definiti utilizzando l&#39;API del Registro di sistema dello schema e l&#39;interfaccia utente dell&#39;Editor schema. Per ulteriori informazioni, consultate le esercitazioni per definire le relazioni tra due schemi [che utilizzano l&#39;API](../xdm/tutorials/relationship-api.md) o [utilizzano l&#39;interfaccia](../xdm/tutorials/relationship-ui.md).

## Creare uno schema ad hoc

In circostanze specifiche, potrebbe essere necessario creare uno schema [!DNL Experience Data Model] (XDM) con campi che vengono denominati separati per l&#39;uso solo da un singolo dataset. Tale schema è denominato &quot;ad hoc&quot;. Gli schemi ad hoc sono utilizzati in vari flussi di lavoro di assimilazione [dei](../ingestion/home.md) dati per [!DNL Experience Platform], inclusi l’assimilazione di file CSV e la creazione di determinati tipi di connessioni [](../sources/home.md)sorgente. La creazione di uno schema ad hoc viene eseguita utilizzando l&#39;API del Registro di sistema dello schema e deve essere utilizzata insieme ad altre [!DNL Experience Platform] esercitazioni che richiedono la creazione di uno schema ad hoc come parte del flusso di lavoro. Per iniziare a creare uno schema ad hoc, vedete l&#39;esercitazione per la [creazione di uno schema ad hoc tramite l&#39;API](../xdm/tutorials/ad-hoc.md).

## Passaggi successivi

Una volta definiti gli schemi per l&#39;organizzazione, è possibile iniziare a creare set di dati in cui è possibile assimilare i dati. Per iniziare, consulta la seguente documentazione:

* [Panoramica sui set di dati](../catalog/datasets/overview.md)
* [Panoramica sull&#39;inserimento dei dati](../ingestion/home.md)