---
solution: Experience Platform
title: Tipi di dati supportati nel servizio di segmentazione
description: Tutti i tipi di dati Experience Data Model (XDM) sono supportati all’interno del servizio di segmentazione Adobe. Le regole che costituiscono una definizione di segmento sono contestualizzate dai seguenti tipi di dati.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---

# Tipi di dati supportati nel servizio di segmentazione

Tutti i tipi di dati Experience Data Model (XDM) sono supportati nel servizio di segmentazione di Adobe Experience Platform. Le regole che costituiscono una definizione di segmento sono contestualizzate dai seguenti tipi di dati.

## Dati stringa

Le definizioni dei segmenti utilizzano i dati stringa per definire vincoli non numerici per i tipi di pubblico, ad esempio &quot;nome del paese&quot; o &quot;livello del programma fedeltà&quot;.

I dati stringa vengono inclusi nelle definizioni dei segmenti utilizzando istruzioni logiche, inclusive/esclusive e di confronto. Una volta aggiunto un attributo stringa alla definizione del segmento, puoi utilizzare istruzioni relative alle stringhe per valutarlo rispetto ad altri campi stringa.

| Tipo di istruzione | Esempi |
| -------------- | -------- |
| Logico | `and`, `or`, `not` |
| Inclusivo/esclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Confronto | `equals`, `does not equal`, `contains`, `starts with` |

## Dati data

I dati sulla data consentono di assegnare un contesto basato sul tempo alle definizioni dei segmenti, utilizzando date di inizio/fine specifiche o istruzioni relative alla data come mostrato nella tabella seguente. Un’implementazione potrebbe consistere nella creazione di un pubblico di clienti che hanno interagito con il tuo marchio in qualsiasi momento *quest&#39;anno* ed è stato anche attivo *entro* ultimi giorni.

| Campo di esempio | Dichiarazioni relative alla data | Timeline |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Rilevante per il giorno in cui è stata generata la definizione del segmento. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Rilevante entro una data settimana/mese. |

## Eventi esperienza

Come schema Adobe Experience Platform, [!DNL XDM ExperienceEvents] registrare le interazioni esplicite e implicite dei clienti con [!DNL Platform]- applicazioni integrate, inclusa un&#39;istantanea del sistema al momento dell&#39;interazione. [!DNL ExperienceEvents] sono documenti fattuali. Di conseguenza, sono un’origine dati disponibile durante la definizione del segmento.

Come mostrato nella tabella seguente, i dati dell’evento vengono riprodotti utilizzando parole chiave che aiutano a perfezionare il comportamento dell’evento e a specificare gli attributi dell’evento.

| Parola chiave | Utilizzo di  |
| ------- | --- |
| Includere/escludere | Descrive il comportamento dell’evento attraverso l’inclusione o l’omissione di dati. |
| Qualsiasi/tutti | Consente di determinare il numero di definizioni di segmenti qualificate. |
| Pulsante di attivazione/disattivazione &quot;Applica regola temporale&quot; | Incorpora i dati della data. |
| È uguale a, non è uguale a, inizia con, non inizia con, termina con, non termina con, contiene, non contiene, esiste, non esiste | Incorpora i dati stringa. |

### Condivisione del pubblico

I tipi di pubblico esterni possono essere utilizzati anche come componenti di una nuova definizione di segmento, aggiungendo le relative regole di attributo alle nuove definizioni di segmento.

Attualmente, solo Adobe Audience Manager è supportato come pubblico esterno, con fonti aggiuntive abilitate in futuro. Ulteriori informazioni sull’utilizzo dei tipi di pubblico di Adobe Audience Manager con Platform sono disponibili nella sezione [guida alla condivisione del pubblico nella documentazione di Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Condivisione della definizione del segmento

Le definizioni dei segmenti create in Platform possono essere utilizzate in altre [Servizi di base di Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=it). Per abilitare questa funzione, contatta l’architetto della soluzione o il consulente.

## Altri tipi di dati

Oltre ai tipi di dati menzionati in precedenza, l’elenco dei tipi di dati supportati include anche:

- Identificatore risorsa uniforme (URI)
- Enum
- Numero
- Lungo
- Intero
- Breve
- Byte
- Booleano
- Array
- Oggetto
- Mappa
