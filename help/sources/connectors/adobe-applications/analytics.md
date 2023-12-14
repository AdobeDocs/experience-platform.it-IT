---
title: Connettore di origine di Adobe Analytics per i dati della suite di rapporti
description: Questo documento fornisce una panoramica di Analytics e descrive i casi d’uso per i dati di Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 251b00e0f0e063859f8d0a0e188fa805c7bf3f87
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 2%

---

# Connettore di origine di Adobe Analytics per i dati della suite di rapporti

Adobe Experience Platform consente di acquisire dati Adobe Analytics tramite il connettore di origine Analytics. Il [!DNL Analytics] il connettore di origine trasmette i dati raccolti da [!DNL Analytics] alla piattaforma in tempo reale, convertendo i formati SCDS [!DNL Analytics] dati in [!DNL Experience Data Model] (XDM) campi per l’utilizzo da parte di Platform.

Questo documento fornisce una panoramica di [!DNL Analytics] e descrive i casi d’uso per [!DNL Analytics] dati.

## Dati di Adobe Analytics e Analytics

[!DNL Analytics] è un motore potente che ti aiuta a scoprire di più sui tuoi clienti, su come interagiscono con le tue proprietà web, a vedere dove la spesa di marketing digitale è efficace e a identificare aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e [!DNL Analytics] Il connettore di origine consente di sfruttare facilmente questi dati comportamentali avanzati e di arricchire [!DNL Real-Time Customer Profile] in pochi minuti.

![Grafico che illustra il percorso di dati provenienti da diverse applicazioni Adobe, incluso Adobe Analytics.](./images/analytics-data-experience-platform.png)

Ad alto livello, [!DNL Analytics] raccoglie dati da vari canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, vengono applicate le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione per modellare i dati in arrivo. Una volta completata l&#39;elaborazione dei dati non elaborati, questi vengono considerati pronti per essere consumati da [!DNL Real-Time Customer Profile]. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono inseriti in micro-batch e acquisiti in set di dati di Platform per l’utilizzo da parte di [!DNL Query Service]e altre applicazioni di data discovery.

Consulta la [panoramica delle regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=it) per ulteriori informazioni sulle regole di elaborazione.

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un’applicazione da utilizzare per comunicare con i servizi su Experienci Platform.

Il rispetto degli standard XDM consente l’incorporazione uniforme dei dati, semplificandone la distribuzione e la raccolta.

Per ulteriori informazioni su XDM, consulta [Panoramica del sistema XDM](../../../xdm/home.md).

## Come vengono mappati i campi da Adobe Analytics a XDM?

>[!IMPORTANT]
>
>Le trasformazioni della preparazione dati possono aggiungere latenza al flusso di dati complessivo. La latenza aggiuntiva aggiunta varia in base alla complessità della logica di trasformazione.

Quando viene stabilita una connessione di origine per l&#39;importazione [!DNL Analytics] dati in Experienci Platform tramite l’interfaccia utente di Platform, i campi dati vengono automaticamente mappati e acquisiti in [!DNL Real-Time Customer Profile] in pochi minuti. Per istruzioni sulla creazione di una connessione sorgente con [!DNL Analytics] utilizzando l’interfaccia utente di Platform, consulta la sezione [Tutorial sul connettore di origine di Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Per informazioni dettagliate sulla mappatura dei campi tra [!DNL Analytics] e Experience Platform, consulta [Mappatura dei campi in Adobe Analytics](./mapping/analytics.md) guida.

## Qual è la latenza prevista per i dati di Analytics su Platform?

La latenza prevista per i dati di Analytics su Platform è descritta nella tabella seguente. La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l’implementazione di Analytics è configurata con `A4T` la latenza rispetto alla pipeline aumenterà a 5-10 minuti.

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati in [!DNL Real-Time Customer Profile] (A4T **non** abilitato) | &lt; 2 minuti |
| Nuovi dati in [!DNL Real-Time Customer Profile] (A4T **è** abilitato) | fino a 30 minuti |
| Nuovi dati in Data Lake | &lt; 90 minuti |
| Backfill di meno di 10 miliardi di eventi | &lt; 4 settimane |

Il valore predefinito della retrocompilazione di Analytics per le sandbox di produzione è 13 mesi. Per i dati di Analytics nelle sandbox non di produzione, la retrocompilazione è impostata su tre mesi. Il limite di 10 miliardi di eventi menzionato nella tabella precedente è strettamente in relazione alla latenza prevista.

Quando crei un flusso di dati di origine Analytics in una sandbox di produzione, vengono creati due flussi di dati:

* Un flusso di dati che esegue una retrocompilazione di 13 mesi dei dati storici della suite di rapporti nel data lake. Questo flusso di dati termina quando la retrocompilazione è completa.
* Un flusso di dati che invia dati live al data lake e a [!DNL Real-Time Customer Profile]. Questo flusso di dati viene eseguito in modo continuo.

>[!NOTE]
>
>I dati di backfill di Analytics non vengono acquisiti in [!DNL Profile] e quindi non viene contabilizzato nei profili di licenza.

## Identificatori primari in [!DNL Analytics] dati

Ogni hit da [!DNL Analytics] il connettore di origine contiene un identificatore primario che dipende dall’esistenza di un ECID o un AAID. Se è presente un ECID, questo viene designato come identificatore primario. Se è presente un AAID, questo viene designato come primario.

La tabella seguente fornisce ulteriori informazioni sui campi di identità nel [!DNL Analytics] dati.

| Campo identità | Descrizione |
| --- | --- |
| AAID | L’AAID è l’identificatore primario del dispositivo in Adobe Analytics ed è garantita la sua esistenza in ogni evento trasmesso attraverso [!DNL Analytics] sorgente. L’AAID è talvolta indicato come *ID legacy di Analytics* o come `s_vi` ID cookie. Nonostante ciò, viene creato un AAID anche se `s_vi` cookie non presente. L’AAID è rappresentato dalla `post_visid_high` e `post_visid_low` colonne in [[!DNL Analytics] feed di dati](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=it). In un dato evento, il campo AAID contiene una singola identità che può corrispondere a uno dei diversi tipi descritti nel [ordine delle operazioni per [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: all’interno di un’intera suite di rapporti, un AAID può contenere diversi tipi in tutti gli eventi. |
| ECID | L’ECID (ID Experience Cloud) è un campo separato dell’identificatore del dispositivo, che viene popolato in Adobe Analytics quando [!DNL Analytics] viene implementato utilizzando il servizio Experience Cloud Identity. L’ECID viene talvolta indicato anche come MCID (ID Marketing Cloud). Se su un evento esiste un ECID, l’AAID può essere basato su ECID a seconda che Analytics [periodo di tolleranza](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) è configurato. L’ECID è rappresentato dalla `mcvisid` nei feed dati di Analytics. Per ulteriori informazioni su ECID, consulta [Panoramica di ECID](../../../identity-service/ecid.md). Per informazioni sul funzionamento di ECID con [!DNL Analytics], consulta il documento su [Richieste Analytics e Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | AACUSTOMID è un campo separato dell’identificatore che viene popolato in Adobe Analytics in base all’utilizzo del `s.VisitorID` variabile in [!DNL Analytics] implementazione. AACUSTOMID è rappresentato da `cust_visid` colonna in [[!DNL Analytics] feed di dati](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=it). Se AACUSTOMID è presente, AAID sarà basato su AACUSTOMID perché AACUSTOMID surclassa tutti gli altri identificatori come definito da [ordine delle operazioni per [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Come [!DNL Analytics] source tratta le identità

Il [!DNL Analytics] L’origine trasmette queste identità ad Experienci Platform nel modulo XDM come:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Questi campi non sono contrassegnati come identità. Invece, le stesse identità vengono copiate in XDM `identityMap` come coppie chiave-valore:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Nella mappa di identità, se ECID è presente, viene contrassegnato come identità primaria dell’evento. In questo caso, AAID può essere basato su ECID a causa della [Periodo di tolleranza per il servizio Identity](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). In caso contrario, AAID è contrassegnato come identità primaria dell’evento. AACUSTOMID non viene mai contrassegnato come ID primario dell’evento. Tuttavia, se AACUSTOMID è presente, AAID è basato su AACUSTOMID a causa dell’ordine Experience Cloud delle operazioni.

>[!NOTE]
>
>Puoi utilizzare la preparazione dati per filtrare le identità secondarie provenienti da Analytics, come AAID e AACUSTOMID. Se escluse, queste identità non verranno acquisite nel profilo se sono disponibili nei dati Analytics in arrivo. I dati non filtrati continueranno a essere caricati nel data lake.
