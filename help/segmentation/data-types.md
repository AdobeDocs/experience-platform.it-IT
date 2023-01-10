---
keywords: Experience Platform;home;argomenti popolari;tipo di dati;tipi di dati;tipi di dati;tipo di dati;tipi di dati di segmentazione;segmentazione;segmentazione;servizio di segmentazione;tipi di dati di servizio di segmentazione;
solution: Experience Platform
title: Tipi di dati supportati nel servizio di segmentazione
description: Tutti i tipi di dati Experience Data Model (XDM) sono supportati in Adobe Segmentation Service. Le regole che costituiscono una definizione di segmento vengono contestualizzate dai seguenti tipi di dati.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Tipi di dati supportati in Segmentation Service

Tutti i tipi di dati Experience Data Model (XDM) sono supportati in Adobe Experience Platform Segmentation Service. Le regole che costituiscono una definizione di segmento vengono contestualizzate dai seguenti tipi di dati.

## Dati stringa

Le definizioni dei segmenti utilizzano i dati stringa per definire vincoli non numerici per i tipi di pubblico dei segmenti, ad esempio &quot;nome del paese&quot; o &quot;livello del programma fedeltà&quot;.

I dati stringa sono inclusi nelle definizioni dei segmenti utilizzando istruzioni logiche, inclusive/esclusive e di confronto. Una volta aggiunto un attributo stringa alla definizione del segmento, puoi utilizzare istruzioni relative alle stringhe per valutarlo rispetto ad altri campi stringa.

| Tipo di istruzione | Esempi |
| -------------- | -------- |
| Logica | `and`, `or`, `not` |
| Inclusivo/esclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Confronto | `equals`, `does not equal`, `contains`, `starts with` |

## Dati data

I dati data consentono di assegnare un contesto basato sull’ora alle definizioni dei segmenti, utilizzando date di inizio/fine specifiche o istruzioni relative alla data come mostrato nella tabella seguente. Un’implementazione potrebbe creare un pubblico di clienti che hanno interagito con il tuo marchio in qualsiasi momento *quest&#39;anno* ed è stato attivo *entro* negli ultimi giorni.

| Campo di esempio | Dichiarazioni relative alla data | Timeline  |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Pertinente al giorno in cui il segmento è stato generato. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Pertinente entro una data settimana/mese. |

## Eventi esperienza

Come schema Adobe Experience Platform, [!DNL XDM ExperienceEvents] registrare interazioni esplicite e implicite con i clienti [!DNL Platform]-applicazioni integrate, compresa una copia istantanea del sistema al momento dell&#39;interazione. [!DNL ExperienceEvents] sono registrazioni dei fatti. Di conseguenza, sono un’origine dati disponibile durante la definizione del segmento.

Come illustrato nella tabella seguente, i dati evento vengono sottoposti a rendering utilizzando parole chiave che consentono di perfezionare il comportamento dell’evento e specificare gli attributi dell’evento.

| Parola chiave | Utilizzo di  |
| ------- | --- |
| Includere/escludere | Descrive il comportamento dell’evento attraverso l’inclusione o l’omissione dei dati. |
| Any/all | Consente di determinare il numero di segmenti qualificati. |
| Pulsante di attivazione/disattivazione &quot;Applica regola di tempo&quot; | Incorpora i dati relativi alla data. |
| Uguale, non uguale, inizia con, non inizia con, termina con, non termina con, contiene, non contiene, esiste, non esiste | Incorpora i dati stringa. |

### Condivisione del pubblico

I tipi di pubblico esterni possono essere utilizzati anche come componenti di una nuova definizione di segmento, aggiungendo le relative regole di attributo al nuovo segmento.

Attualmente, solo Adobe Audience Manager è supportato come pubblico esterno, con origini aggiuntive abilitate in futuro. Per ulteriori informazioni sull’utilizzo dei tipi di pubblico di Adobe Audience Manager con Platform, consulta [guida alla condivisione del pubblico nella documentazione di Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Condivisione dei segmenti

I segmenti creati in Platform possono essere utilizzati in altri [Servizi di base Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=it). Per abilitare questa funzione, è necessario contattare l&#39;architetto della soluzione o il consulente.

## Altri tipi di dati

Oltre ai tipi di dati sopra menzionati, l’elenco dei tipi di dati supportati include anche:

- Identificatore uniforme delle risorse (URI)
- Enum
- Numero
- Lunga
- Intero
- Breve
- Byte
- Booleano
- Array
- Oggetto
- Mappa
