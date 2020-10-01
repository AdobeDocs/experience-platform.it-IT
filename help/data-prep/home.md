---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: Funzioni di mappatura
topic: overview
description: In questo documento vengono introdotti i predefiniti dati in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Preparazione dati

Data Prep consente agli ingegneri di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). Prep dati viene visualizzato come un passaggio &quot;Mappa&quot; nei processi di inserimento dei dati, compreso il flusso di lavoro di inserimento CSV. Gli ingegneri dei dati possono utilizzare Data Prep per eseguire le seguenti operazioni di manipolazione dei dati durante l&#39;assimilazione:

- Definizione di mappature passthrough semplici per assegnare gli attributi di input agli attributi XDM
- Creazione di campi calcolati per eseguire calcoli in riga che possono essere assegnati agli attributi XDM
- Trasformare i dati applicando funzioni stringa, numeriche o di manipolazione della data
- Costruire gerarchie XDM utilizzando funzioni gerarchiche
- Visualizzare l&#39;anteprima dei dati così come vengono modificati nell&#39;API dati

Prep dati applica anche diverse convalide intrinseche per garantire che l&#39;integrità dei dati venga mantenuta durante l&#39;assimilazione. Laddove possibile, in Prep dati gli schemi di dati in entrata vengono mappati automaticamente su XDM. Gli ingegneri dei dati possono modificare, correggere ed eliminare le mappature suggerite e sostituirle con le mappature appropriate.

## Mapping

Un mapping è un&#39;associazione di un attributo di input o di un campo calcolato a un attributo XDM. Un singolo attributo può essere mappato a più attributi XDM creando mappature individuali.

Per ulteriori informazioni sulle diverse funzioni di mappatura, consulta la guida [alle funzioni di](./functions.md)mappatura.

## Set di mapping

Un set di mappature che trasforma uno schema in un altro è noto come insieme di mapping. Viene creato un singolo set di mapping come parte di ciascun flusso di dati. Un set di mappature è parte integrante dei flussi di dati e viene creato, modificato e monitorato come parte dei flussi di dati.

## Passaggi successivi

In questo documento sono state illustrate le nozioni di base su Data Prep in Adobe Experience Platform. Per ulteriori informazioni sulle diverse funzioni di mappatura, consulta la guida [alle funzioni di](./functions.md)mappatura. Per ulteriori informazioni sulle diverse stringhe data/ora, consultare la guida [alle stringhe](./dates.md)data.