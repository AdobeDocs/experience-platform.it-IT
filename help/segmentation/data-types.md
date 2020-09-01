---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type;Segmentation data types;Segmentation;segmentation;Segmentation Service;Segmentation service data types;
solution: Experience Platform
title: Tipi di dati del servizio di segmentazione Adobe Experience Platform
topic: overview
description: Tutti i tipi di dati XDM sono supportati in Segmentation Service. Le regole che costituiscono una definizione di segmento sono contestualizzate dai seguenti tipi di dati.
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Tipi di dati supportati da Adobe Experience Platform [!DNL Segmentation Service]

Tutti i tipi di dati XDM sono supportati all&#39;interno [!DNL Segmentation Service]. Le regole che costituiscono una definizione di segmento sono contestualizzate dai seguenti tipi di dati.

## Dati stringa

Le definizioni dei segmenti utilizzano i dati stringa per definire vincoli non numerici per i tipi di pubblico dei segmenti, ad esempio &quot;nome del paese&quot; o &quot;livello del programma fedeltà&quot;.

I dati stringa sono inclusi nelle definizioni dei segmenti utilizzando istruzioni logiche, complete/esclusive e di confronto. Una volta aggiunto un attributo stringa alla definizione del segmento, è possibile utilizzare istruzioni pertinenti sotto forma di stringa per valutarlo rispetto ad altri campi stringa.

| Tipo di istruzione | Esempi |
| -------------- | -------- |
| Logica | `and`, `or`, `not` |
| Inclusivo/esclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Confronto | `equals`, `does not equal`, `contains`, `starts with` |

## Dati data

I dati data consentono di assegnare contesto basato sull&#39;ora alle definizioni dei segmenti, utilizzando date di inizio/fine specifiche o utilizzando istruzioni relative alla data come mostrato nella tabella seguente. Un&#39;implementazione potrebbe consistere nel creare un pubblico di clienti che hanno interagito con il tuo marchio in *quest&#39;anno* e che è stato attivo anche *negli* ultimi giorni.

| Esempio di campo | Indicazioni relative alla data | Timeline  |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Pertinente al giorno in cui il segmento è stato creato. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Pertinente entro una data settimana/mese. |

## Eventi esperienza

Come schema Adobe Experience Platform, [!DNL XDM ExperienceEvents] registra le interazioni esplicite e implicite dei clienti con le applicazioni [!DNL Platform]integrate, inclusa un&#39;istantanea del sistema al momento dell&#39;interazione. [!DNL ExperienceEvents] sono record di fatti. Sono pertanto un&#39;origine dati disponibile durante la definizione del segmento.

Come illustrato nella tabella seguente, i dati dell&#39;evento vengono rappresentati utilizzando le parole chiave che consentono di definire il comportamento dell&#39;evento e specificare gli attributi dell&#39;evento.

| Parola chiave | Utilizzo di  |
| ------- | --- |
| Includi/Escludi | Descrive il comportamento dell&#39;evento attraverso l&#39;inclusione o l&#39;omissione dei dati. |
| Any/all | Consente di determinare il numero di segmenti idonei. |
| Pulsante &quot;Applica regola di ora&quot; | Incorpora i dati data. |
| Uguale, non uguale, inizia con, non inizia con, termina con, non termina con, contiene, non contiene, non contiene, esiste, non esiste | Incorpora i dati stringa. |

### Condivisione del pubblico

Le audience esterne possono essere utilizzate anche come componenti di una nuova definizione di segmento, aggiungendo le relative regole di attributi al nuovo segmento.

Al momento, solo Adobe Audience Manager è supportato come pubblico esterno, mentre in futuro saranno abilitate ulteriori origini. Per ulteriori informazioni sull&#39;utilizzo dei tipi di pubblico Adobe Audience Manager con Piattaforma, consulta la guida alla condivisione di [audience all&#39;interno della documentazione](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)Adobe Audience Manager.

### Condivisione di segmenti

I segmenti creati in Piattaforma possono essere utilizzati in altri servizi [di base di](https://docs.adobe.com/content/help/it-IT/core-services/interface/experience-cloud.html)Adobe Experience Cloud. Per abilitare questa funzione, è necessario contattare l&#39;architetto della soluzione o il consulente.

## Altri tipi di dati

Oltre ai tipi di dati sopra menzionati, l&#39;elenco dei tipi di dati supportati include anche:

- Uniform Resource Identifier (URI)
- Enum
- Numero
- Long
- Intero
- Breve
- Byte
- Booleano
- Matrice
- Oggetto
- Mappa