---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv su xdm;mappare csv su xdm;guida interfaccia utente;mappatura;mappatura;preparazione dati;preparazione dati;preparazione dei dati;
solution: Experience Platform
title: Panoramica sulla preparazione dei dati
description: Questo documento introduce Data Prep in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '788'
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

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati agli attributi nello schema di destinazione e ricevere un nome e una descrizione per facilitarne il riferimento. I campi calcolati hanno una lunghezza massima di 4096 caratteri.

Per ulteriori informazioni sui campi calcolati, consulta la sezione [guida ai campi calcolati](./functions.md#calculated-fields).

### Caratteri speciali di escape {#escape-special-characters}

È possibile applicare un escape ai caratteri speciali in un campo utilizzando `${...}`. Tuttavia, i file JSON che contengono campi con un punto (`.`) non sono supportate da questo meccanismo. Quando interagisci con le gerarchie, se un attributo figlio ha un punto (`.`), è necessario utilizzare una barra rovesciata (`\`) per evitare i caratteri speciali. Ad esempio: `address` è un oggetto che contiene l&#39;attributo `street.name`, che può essere successivamente indicato come `address.street\.name` anziché `address.street.name`.

## Set di mappature

Un set di mappature che trasformano uno schema in un altro è noto collettivamente come set di mappature. Viene creato un singolo set di mappatura come parte di ciascun flusso di dati. Un set di mappatura è parte integrante dei flussi di dati e viene creato, modificato e monitorato come parte dei flussi di dati.

Per ulteriori informazioni sui set di mappatura, tra cui come utilizzare i campi all’interno di un set di mappatura, consulta la sezione [guida al set di mappature](./mapping-set.md). Per informazioni su come creare un set di mappatura e utilizzare altre chiamate API relative ai set di mappatura, consulta la sezione del set di mappatura in [guida per sviluppatori](./api/mapping-set.md).

## Gestione del formato dati

Data Prep può gestire in modo affidabile diversi formati di dati acquisiti in Platform. Per ulteriori informazioni su come Data Prep gestisce diversi tipi di dati, consulta la sezione [panoramica sulla gestione del formato dati](./data-handling.md).

## Invia aggiornamenti parziali delle righe utilizzando [!DNL Data Prep]

Streaming degli upsers in [!DNL Data Prep] consente di inviare aggiornamenti parziali delle righe a [!DNL Profile Service] durante la creazione e la creazione di nuovi collegamenti di identità con una singola richiesta API. Per ulteriori informazioni su come eseguire lo streaming degli upsers in [!DNL Data Prep], consulta il documento in [invio di aggiornamenti di riga parziali](./upserts.md).

## Controllo dell&#39;accesso basato su attributi in [!DNL Data Prep]

Il controllo dell&#39;accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi.

Il controllo dell&#39;accesso basato su attributi consente di mappare solo gli attributi a cui hai accesso. Gli attributi a cui non hai accesso non possono essere utilizzati nelle mappature pass-through e nei campi calcolati. Pertanto, se non si dispone dell&#39;accesso a un campo obbligatorio, non è possibile salvare correttamente una mappatura. Inoltre, non è possibile eseguire il mapping di oggetti o array di oggetti se non si dispone dell&#39;accesso a uno degli attributi figlio. Tuttavia, è possibile eseguire il mapping di altri elementi all&#39;interno dell&#39;array di oggetti o dell&#39;oggetto singolarmente.

Consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](../access-control/abac/overview.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento illustra le nozioni di base sulla preparazione dei dati in Adobe Experience Platform. Per ulteriori informazioni sulle diverse funzioni di mappatura, consulta la sezione [guida alle funzioni di mappatura](./functions.md). Per ulteriori informazioni su come Data Prep gestisce diversi tipi di dati, consulta la sezione [guida alla gestione del formato dati](./data-handling.md#dates). Per informazioni su come utilizzare l’API di preparazione dei dati, leggi la sezione [Guida per gli sviluppatori di Data Prep](api/overview.md).
