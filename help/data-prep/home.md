---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv su xdm;mappare csv su xdm;guida interfaccia utente;mappatura;mappatura;preparazione dati;preparazione dati;preparazione dei dati;
solution: Experience Platform
title: Panoramica sulla preparazione dei dati
topic-legacy: overview
description: Questo documento introduce Data Prep in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 3dac1a80e640364f8c0b6b6fd81821499bf889b3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---


# Panoramica sulla preparazione dei dati

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). La preparazione dei dati viene visualizzata come un passaggio &quot;Mappa&quot; nei processi di acquisizione dei dati, incluso il flusso di lavoro di acquisizione CSV. I data engineer possono utilizzare Data Prep per eseguire le seguenti manipolazioni dei dati durante l’acquisizione:

- Definire semplici mappature pass-through per assegnare gli attributi di input agli attributi XDM
- Creazione di campi calcolati per eseguire calcoli in riga che possono essere assegnati agli attributi XDM
- Trasforma i dati applicando funzioni di manipolazione di stringa, numeriche o date
- Costruire gerarchie XDM utilizzando funzioni gerarchiche
- Visualizza in anteprima i dati durante la manipolazione all’interno di Data Prep

Data Prep applica anche diverse convalide di dati intrinseci per garantire che l’integrità dei dati venga mantenuta durante l’acquisizione. Laddove possibile, Data Prep mappa automaticamente gli schemi di dati in arrivo su XDM. I data engineer possono modificare, correggere ed eliminare le mappature suggerite e sostituirle con le mappature appropriate.

>[!NOTE]
>
>A meno che il messaggio risultante non sia XDM valido, eventuali errori di trasformazione in Preparazione dati imposteranno gli attributi su `null`, mentre il resto della riga verrà acquisito. Se la riga restituisce un valore XDM non valido, la riga verrà **not** essere ingeriti. In entrambi i casi, l&#39;errore sarà documentato.

## Mappatura

Una mappatura è un&#39;associazione di un attributo di input o di un campo calcolato a un attributo XDM. Un singolo attributo può essere mappato su più attributi XDM creando mappature individuali.

Per ulteriori informazioni sulle diverse funzioni di mappatura, consulta la sezione [guida alle funzioni di mappatura](./functions.md).

### Campi calcolati

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati agli attributi nello schema di destinazione e ricevere un nome e una descrizione per facilitarne il riferimento.

Per ulteriori informazioni sui campi calcolati, consulta la sezione [guida ai campi calcolati](./functions.md#calculated-fields).

## Set di mappature

Un set di mappature che trasformano uno schema in un altro è noto collettivamente come set di mappature. Viene creato un singolo set di mappatura come parte di ciascun flusso di dati. Un set di mappatura è parte integrante dei flussi di dati e viene creato, modificato e monitorato come parte dei flussi di dati.

Per ulteriori informazioni sui set di mappatura, tra cui come utilizzare i campi all’interno di un set di mappatura, consulta la sezione [guida al set di mappature](./mapping-set.md). Per informazioni su come creare un set di mappatura e utilizzare altre chiamate API relative ai set di mappatura, consulta la sezione del set di mappatura in [guida per sviluppatori](./api/mapping-set.md).

## Gestione del formato dati

Data Prep può gestire in modo affidabile diversi formati di dati acquisiti in Platform. Per ulteriori informazioni su come Data Prep gestisce diversi tipi di dati, consulta la sezione [panoramica sulla gestione del formato dati](./data-handling.md).

## Invia aggiornamenti parziali delle righe utilizzando [!DNL Data Prep]

Streaming degli upsers in [!DNL Data Prep] consente di inviare aggiornamenti parziali delle righe a [!DNL Profile Service] durante la creazione e la creazione di nuovi collegamenti di identità con una singola richiesta API. Per ulteriori informazioni su come eseguire lo streaming degli upsers in [!DNL Data Prep], consulta il documento in [invio di aggiornamenti di riga parziali](./upserts.md).

## Passaggi successivi

Questo documento illustra le nozioni di base sulla preparazione dei dati in Adobe Experience Platform. Per ulteriori informazioni sulle diverse funzioni di mappatura, consulta la sezione [guida alle funzioni di mappatura](./functions.md). Per ulteriori informazioni su come Data Prep gestisce diversi tipi di dati, consulta la sezione [guida alla gestione del formato dati](./data-handling.md#dates). Per informazioni su come utilizzare l’API di preparazione dei dati, leggi la sezione [Guida per gli sviluppatori di Data Prep](api/overview.md).
