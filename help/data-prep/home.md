---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv a xdm;mappare csv a xdm;guida interfaccia utente;mapper;mappare;preparazione dati;preparazione dati;preparazione dati;
solution: Experience Platform
title: Panoramica sulla preparazione dati
description: Questo documento introduce la preparazione dati in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---


# Panoramica sulla preparazione dati

La preparazione dati consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). La preparazione dati viene visualizzata come un passaggio &quot;Mappa&quot; nei processi di acquisizione dati, incluso il flusso di lavoro di acquisizione CSV. I data engineer possono utilizzare la preparazione dati per eseguire le seguenti manipolazioni di dati durante l’acquisizione:

- Definire semplici mappature pass-through per assegnare attributi di input agli attributi XDM
- Creare campi calcolati per eseguire calcoli su righe che possono essere assegnati ad attributi XDM
- Trasforma i dati applicando funzioni di manipolazione stringa, numerica o data
- Creare gerarchie XDM utilizzando funzioni gerarchiche
- Visualizzare l’anteprima dei dati così come vengono manipolati nella preparazione dati

La preparazione dati applica anche diverse convalide di dati intrinseche per garantire che l’integrità dei dati venga mantenuta durante l’acquisizione. Laddove possibile, la preparazione dati mappa automaticamente gli schemi di dati in arrivo su XDM. I data engineer possono modificare, correggere ed eliminare le mappature suggerite e sostituirle con le mappature appropriate.

>[!NOTE]
>
>A meno che il messaggio risultante non sia un XDM valido, eventuali errori di trasformazione nella preparazione dati determineranno l&#39;impostazione di tali attributi su `null`, mentre il resto della riga verrà acquisito. Se la riga viene risolta in XDM non valido, la riga **non** verrà acquisita. In entrambi i casi, l’errore verrà documentato.

## Mappatura

Un mapping è un&#39;associazione di un attributo di input o di un campo calcolato a un attributo XDM. Un singolo attributo può essere mappato a più attributi XDM creando singoli mapping.

Per ulteriori informazioni sulle diverse funzioni di mappatura, leggere la [guida alle funzioni di mappatura](./functions.md).

### Campi calcolati

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati ad attributi nello schema di destinazione e ricevere un nome e una descrizione per consentire un riferimento più semplice. I campi calcolati hanno una lunghezza massima di 4096 caratteri.

Per ulteriori informazioni sui campi calcolati, leggere la [guida dei campi calcolati](./functions.md#calculated-fields).

### Esci dai caratteri speciali {#escape-special-characters}

È possibile eliminare i caratteri speciali in un campo utilizzando `${...}`. Tuttavia, i file JSON che contengono campi con un punto (`.`) non sono supportati da questo meccanismo. Quando si interagisce con le gerarchie, se un attributo figlio ha un punto (`.`), è necessario utilizzare una barra rovesciata (`\`) per eliminare i caratteri speciali. Ad esempio, `address` è un oggetto che contiene l&#39;attributo `street.name`, che può quindi essere indicato come `address.street\.name` invece di `address.street.name`.

## Set di mappatura

Un set di mappature che trasforma uno schema in un altro è collettivamente noto come set di mappatura. Un singolo set di mappatura viene creato come parte di ogni flusso di dati. Un set di mappatura è parte integrante dei flussi di dati e viene creato, modificato e monitorato come parte dei flussi di dati.

Per ulteriori informazioni sui set di mappatura, tra cui come utilizzare i campi all&#39;interno di un set di mappatura, leggere la [guida del set di mappatura](./mapping-set.md). Per informazioni su come creare un set di mappatura e utilizzare altre chiamate API relative ai set di mappatura, consulta la sezione sui set di mappatura nella [guida per gli sviluppatori](./api/mapping-set.md).

## Gestione del formato dei dati

La preparazione dati può gestire in modo affidabile diversi formati di dati acquisiti in Platform. Per ulteriori informazioni su come la preparazione dati gestisce diversi tipi di dati, leggere la [panoramica sulla gestione del formato dati](./data-handling.md).

## Invia aggiornamenti riga parziali tramite [!DNL Data Prep]

Gli upsert di streaming in [!DNL Data Prep] consentono di inviare aggiornamenti di riga parziali ai dati [!DNL Profile Service], creando e stabilendo nuovi collegamenti di identità con una singola richiesta API. Per ulteriori informazioni su come eseguire lo streaming degli aggiornamenti a monte in [!DNL Data Prep], consulta il documento in [invio di aggiornamenti di riga parziali](./upserts.md).

## Controllo dell&#39;accesso basato su attributi in [!DNL Data Prep]

Il controllo dell’accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi.

Il controllo dell&#39;accesso basato su attributi consente di mappare solo gli attributi a cui hai accesso. Gli attributi ai quali non hai accesso non possono essere utilizzati nelle mappature pass-through e nei campi calcolati. Di conseguenza, se non hai accesso a un campo obbligatorio, non puoi salvare correttamente una mappatura. Inoltre, non è possibile mappare oggetti o array di oggetti se non si ha accesso a nessuno degli attributi figlio. Tuttavia, è possibile mappare singolarmente altri elementi all&#39;interno dell&#39;oggetto o dell&#39;array di oggetti.

Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi basato su attributi](../access-control/abac/overview.md).

## Passaggi successivi

Questo documento illustra le nozioni di base sulla preparazione dati in Adobe Experience Platform. Per ulteriori informazioni sulle diverse funzioni di mappatura, leggere la [guida alle funzioni di mappatura](./functions.md). Per ulteriori informazioni su come la preparazione dati gestisce diversi tipi di dati, leggere la [guida alla gestione del formato dei dati](./data-handling.md#dates). Per informazioni su come utilizzare l&#39;API di preparazione dati, leggere la [Guida per gli sviluppatori di preparazione dati](api/overview.md).
