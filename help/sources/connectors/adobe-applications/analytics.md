---
title: Connettore Source di Adobe Analytics per i dati della suite di rapporti
description: Questo documento fornisce una panoramica di Analytics e descrive i casi d’uso per i dati di Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d56a37c5b1c5768b3f6811be9d30d45628fdabca
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# Connettore di origine di Adobe Analytics per i dati della suite di rapporti

Adobe Experience Platform consente di acquisire dati Adobe Analytics tramite il connettore di origine Analytics. Il connettore di origine [!DNL Analytics] trasmette in tempo reale i dati raccolti da [!DNL Analytics] a Platform, convertendo i dati [!DNL Analytics] in formato SCDS in campi [!DNL Experience Data Model] (XDM) da utilizzare in Platform.

Questo documento fornisce una panoramica di [!DNL Analytics] e descrive i casi d&#39;uso per i dati di [!DNL Analytics].

## Dati di Adobe Analytics e Analytics

[!DNL Analytics] è un motore potente che ti aiuta a conoscere meglio i tuoi clienti, il modo in cui interagiscono con le tue proprietà web, a vedere dove le tue spese di marketing digitale sono efficaci e a identificare le aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e il connettore di origine [!DNL Analytics] consente di accedere facilmente a questi dati comportamentali avanzati e arricchire [!DNL Real-Time Customer Profile] in pochi minuti.

![Grafico che illustra il percorso di dati provenienti da diverse applicazioni Adobe, incluso Adobe Analytics.](./images/analytics-data-experience-platform.png)

Ad alto livello, [!DNL Analytics] raccoglie dati da vari canali digitali e da più data center in tutto il mondo. Una volta raccolti i dati, vengono applicate le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione per modellare i dati in arrivo. Una volta completata l&#39;elaborazione dei dati non elaborati, questi verranno considerati pronti per essere utilizzati da [!DNL Real-Time Customer Profile]. In un processo parallelo a quello sopra descritto, gli stessi dati elaborati vengono salvati in micro-batch e acquisiti in set di dati Platform per l&#39;utilizzo da parte di [!DNL Query Service] e altre applicazioni di data discovery.

Per ulteriori informazioni sulle regole di elaborazione, vedere la [panoramica delle regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=it).

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un’applicazione da utilizzare per comunicare con i servizi su Experience Platform.

Il rispetto degli standard XDM consente l’incorporazione uniforme dei dati, semplificandone la distribuzione e la raccolta.

Per ulteriori informazioni su XDM, consulta la [panoramica del sistema XDM](../../../xdm/home.md).

## Come vengono mappati i campi da Adobe Analytics a XDM?

>[!IMPORTANT]
>
>Le trasformazioni della preparazione dati possono aggiungere latenza al flusso di dati complessivo. La latenza aggiuntiva aggiunta varia in base alla complessità della logica di trasformazione.

Quando viene stabilita una connessione di origine per l&#39;Experience Platform di dati [!DNL Analytics] tramite l&#39;interfaccia utente di Platform, i campi dati vengono automaticamente mappati e acquisiti in [!DNL Real-Time Customer Profile] in pochi minuti. Per istruzioni sulla creazione di una connessione di origine con [!DNL Analytics] tramite l&#39;interfaccia utente di Platform, consulta l&#39;[esercitazione sul connettore di origine di Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Per informazioni dettagliate sulla mappatura dei campi tra [!DNL Analytics] e Experience Platform, consulta la [guida alla mappatura dei campi di Adobe Analytics](./mapping/analytics.md).

## Qual è la latenza prevista per i dati di Analytics su Platform?

La latenza prevista per i dati di Analytics su Platform è descritta nella tabella seguente. La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l&#39;implementazione di Analytics è configurata con `A4T`, la latenza per la pipeline aumenterà a 5-10 minuti.

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati in [!DNL Real-Time Customer Profile] (A4T **non** abilitato) | &lt; 2 minuti |
| Nuovi dati in [!DNL Real-Time Customer Profile] (A4T **è** abilitato) | fino a 30 minuti |
| Nuovi dati in Data Lake | &lt; 2,25 ore |
| Nuovi dati per il Customer Journey Analytics senza [unione](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 ore |
| Nuovi dati da inserire nel Customer Journey Analytics con l’unione | &lt; 7 ore |
| Backfill di meno di 10 miliardi di eventi | &lt; 4 settimane |

Per ulteriori informazioni sulle latenze del Customer Journey Analytics, vedere: [Guardrail del Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Il valore predefinito della retrocompilazione di Analytics per le sandbox di produzione è 13 mesi. Per i dati di Analytics nelle sandbox non di produzione, la retrocompilazione è impostata su tre mesi. Il limite di 10 miliardi di eventi menzionato nella tabella precedente è strettamente in relazione alla latenza prevista.

Quando crei un flusso di dati di origine Analytics in una sandbox di produzione, vengono creati due flussi di dati:

* Un flusso di dati che esegue una retrocompilazione di 13 mesi dei dati storici della suite di rapporti nel data lake. Questo flusso di dati termina quando la retrocompilazione è completa.
* Flusso di dati che invia dati live al data lake e a [!DNL Real-Time Customer Profile]. Questo flusso di dati viene eseguito in modo continuo.

>[!NOTE]
>
>I dati di backfill di Analytics non vengono acquisiti in [!DNL Profile] e pertanto non vengono considerati nei profili di licenza.

## Identificatori primari nei dati [!DNL Analytics]

Ogni hit del connettore di origine [!DNL Analytics] contiene un identificatore primario che dipende dall&#39;esistenza di un ECID o un AAID. Se è presente un ECID, questo viene designato come identificatore primario. Se è presente un AAID, questo viene designato come primario.

La tabella seguente fornisce ulteriori informazioni sui campi di identità nei dati [!DNL Analytics].

| Campo identità | Descrizione |
| --- | --- |
| AAID | AAID è l&#39;identificatore del dispositivo principale in Adobe Analytics ed è garantita la sua esistenza in ogni evento trasmesso tramite l&#39;origine [!DNL Analytics]. AAID viene talvolta indicato come *ID legacy di Analytics* o come ID cookie `s_vi`. Nonostante ciò, viene creato un AAID anche se il cookie `s_vi` non è presente. AAID è rappresentato dalle colonne `post_visid_high` e `post_visid_low` in [[!DNL Analytics] feed di dati](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). In un dato evento, il campo AAID contiene una singola identità che può essere uno dei diversi tipi descritti nell&#39;[ordine delle operazioni per [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: all&#39;interno di un&#39;intera suite di rapporti, un AAID può contenere diversi tipi tra gli eventi. |
| ECID | L&#39;ECID (ID Experience Cloud) è un campo separato dell&#39;identificatore del dispositivo, che viene popolato in Adobe Analytics quando [!DNL Analytics] viene implementato utilizzando il servizio Experience Cloud Identity. L’ECID viene talvolta indicato anche come MCID (ID Marketing Cloud). Se su un evento esiste un ECID, l&#39;AAID può essere basato su ECID a seconda che il [periodo di tolleranza](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) di Analytics sia configurato o meno. ECID è rappresentato da `mcvisid` nei feed dati di Analytics. Per ulteriori informazioni su ECID, consulta la [panoramica ECID](../../../identity-service/features/ecid.md). Per informazioni sul funzionamento di ECID con [!DNL Analytics], consulta il documento su [Analytics e richieste Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | AACUSTOMID è un campo separato dell&#39;identificatore che viene popolato in Adobe Analytics in base all&#39;utilizzo della variabile `s.VisitorID` nell&#39;implementazione [!DNL Analytics]. AACUSTOMID è rappresentato dalla colonna `cust_visid` in [[!DNL Analytics] feed di dati](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Se AACUSTOMID è presente, AAID sarà basato su AACUSTOMID perché AACUSTOMID supera tutti gli altri identificatori come definito dall&#39;[ordine delle operazioni per [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Trattamento delle identità da parte dell&#39;origine [!DNL Analytics]

L&#39;origine [!DNL Analytics] trasmette queste identità all&#39;Experience Platform nel modulo XDM come:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Questi campi non sono contrassegnati come identità. Le stesse identità (se presenti nell&#39;evento) vengono invece copiate in `identityMap` di XDM come coppie chiave-valore:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Quando l&#39;identità o le identità vengono copiate in `identityMap`, anche `endUserIDs._experience.mcid.namespace.code` viene impostato sullo stesso evento:

* Se AAID è presente, `endUserIDs._experience.aaid.namespace.code` è impostato su &quot;AAID&quot;.
* Se ECID è presente, `endUserIDs._experience.mcid.namespace.code` è impostato su &quot;ECID&quot;.
* Se AACUSTOMID è presente, `endUserIDs._experience.aacustomid.namespace.code` è impostato su &quot;AACUSTOMID&quot;.

Nella mappa di identità, se ECID è presente, viene contrassegnato come identità primaria dell’evento. In questo caso, AAID può essere basato su ECID a causa del [periodo di tolleranza del servizio Identity](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). In caso contrario, AAID è contrassegnato come identità primaria dell’evento. AACUSTOMID non viene mai contrassegnato come ID primario dell’evento. Tuttavia, se AACUSTOMID è presente, AAID è basato su AACUSTOMID a causa dell’ordine Experience Cloud delle operazioni.

>[!NOTE]
>
>Puoi utilizzare la preparazione dati per filtrare le identità secondarie provenienti da Analytics, come AAID e AACUSTOMID. Se escluse, queste identità non verranno acquisite nel profilo se sono disponibili nei dati Analytics in arrivo. I dati non filtrati continueranno a essere caricati nel data lake.
