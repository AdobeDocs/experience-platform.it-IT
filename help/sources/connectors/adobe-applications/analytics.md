---
keywords: Experience Platform;home;argomenti popolari;Connettore origine Analytics;analytics;Analytics;AAID;
title: Connettore sorgente Adobe Analytics per i dati della suite di rapporti
description: Questo documento fornisce una panoramica di Analytics e descrive i casi d’uso per i dati di Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d94bbbd34b116f10098624d565c1ae285fc0461e
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 6%

---

# Connettore sorgente Adobe Analytics per i dati della suite di rapporti

Adobe Experience Platform consente di acquisire i dati di Adobe Analytics tramite il connettore di origine di Analytics. La [!DNL Analytics] dati del connettore di origine raccolti da [!DNL Analytics] su Platform in tempo reale, conversione in formato SCDS [!DNL Analytics] dati [!DNL Experience Data Model] (XDM) campi da utilizzare in Platform.

Questo documento fornisce una panoramica di [!DNL Analytics] e descrive i casi d&#39;uso per [!DNL Analytics] dati.

## Dati di Adobe Analytics e Analytics

[!DNL Analytics] è un motore potente che ti aiuta a scoprire di più sui tuoi clienti, su come interagiscono con le tue proprietà web, su dove le tue spese di marketing digitale sono efficaci e individua le aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e [!DNL Analytics] il connettore di origine ti consente di sfruttare facilmente questi ricchi dati comportamentali e di arricchire il [!DNL Real-time Customer Profile] in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad alto livello, [!DNL Analytics] raccoglie dati da diversi canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, vengono applicate le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione per modellare i dati in arrivo. Una volta che i dati grezzi hanno superato questa elaborazione leggera, vengono considerati pronti per il consumo da [!DNL Real-time Customer Profile]. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono micro-batch e acquisiti in set di dati Platform per consumo da [!DNL Data Science Workspace], [!DNL Query Service]e altre applicazioni di data discovery.

Consulta la sezione [panoramica delle regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) per ulteriori informazioni sulle regole di elaborazione.

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi su Experience Platform.

Il rispetto degli standard XDM consente l&#39;integrazione uniforme dei dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, consulta la sezione [Panoramica del sistema XDM](../../../xdm/home.md).

## Come vengono mappati i campi da Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l&#39;importazione [!DNL Analytics] dati in Experience Platform tramite l’interfaccia utente di Platform, i campi dati vengono mappati automaticamente e acquisiti in [!DNL Real-time Customer Profile] in pochi minuti. Per istruzioni su come creare una connessione sorgente con [!DNL Analytics] utilizzando l’interfaccia utente di Platform, consulta [Esercitazione sul connettore sorgente di Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Per informazioni dettagliate sulla mappatura dei campi eseguita tra [!DNL Analytics] e, ad Experience Platform, vedi la [Mappatura dei campi Adobe Analytics](./mapping/analytics.md) guida.

## Qual è la latenza prevista per i dati di Analytics su Platform?

La latenza prevista per i dati di Analytics su Platform è descritta nella tabella seguente. La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l’implementazione di Analytics è configurata con `A4T` la latenza alla pipeline aumenterà a 5-10 minuti.

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati in [!DNL Real-time Customer Profile] (A4T **not** abilitato) | &lt; 2 minuti |
| Nuovi dati in [!DNL Real-time Customer Profile] (A4T **è** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 90 minuti |
| Recupero di meno di 10 miliardi di eventi | &lt; 4 settimane |

Per impostazione predefinita, Analytics esegue il backfills a 13 mesi. Il limite di 10 miliardi di eventi menzionato nella tabella precedente è strettamente in relazione alla latenza attesa.

>[!NOTE]
>
>I dati di backfill di Analytics non vengono acquisiti in [!DNL Profile] e quindi non viene contabilizzata nei profili di licenza.

## Identificatori principali in [!DNL Analytics] dati

Ogni hit da [!DNL Analytics] il connettore di origine contiene un identificatore principale che dipende dall’esistenza di un ECID o di un AAID. Se è presente un ECID, questo viene designato come identificatore principale. Se è presente un AAID, l’AAID è indicato come primario.

La tabella seguente fornisce ulteriori informazioni sui campi di identità nel [!DNL Analytics] dati.

| Campo identità | Descrizione |
| --- | --- |
| AAID | L’AAID è l’identificatore del dispositivo principale in Adobe Analytics ed è garantito che esista su ogni evento che viene passato attraverso il [!DNL Analytics] sorgente. L’AAID viene a volte indicato come *ID Analytics legacy* o come `s_vi` ID cookie. Tuttavia, viene creato un AAID anche se il `s_vi` cookie non presente. L’AAID è rappresentato dal `post_visid_high` e `post_visid_low` colonne in [[!DNL Analytics] feed dati](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=it). Su un dato evento, il campo AAID contiene una singola identità che può essere uno dei diversi tipi descritti nel [ordine delle operazioni [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: All’interno di un’intera suite di rapporti, un AAID può contenere diversi tipi di eventi. |
| ECID | L’ECID (ID Experience Cloud) è un campo di identificazione del dispositivo separato, che viene popolato in Adobe Analytics quando [!DNL Analytics] viene implementato utilizzando il servizio Experience Cloud Identity. L’ECID viene talvolta indicato anche come MCID (ID Marketing Cloud). Se un ECID esiste su un evento, l’AAID può essere basato su ECID a seconda che Analytics [periodo di tolleranza](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) è configurato. L’ECID è rappresentato dal `mcvisid` nei feed di dati di Analytics. Per ulteriori informazioni su ECID, consulta la sezione [Panoramica ECID](../../../identity-service/ecid.md). Per informazioni su come funziona ECID con [!DNL Analytics], consulta il documento in [Richieste Analytics ed Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=it). |
| AACUSTOMID | L&#39;AACUSTOMID è un campo di identificazione separato che viene popolato in Adobe Analytics in base all&#39;uso del `s.VisitorID` nella variabile [!DNL Analytics] implementazione. L&#39;AACUSTOMID è rappresentato dal `cust_visid` colonna in [[!DNL Analytics] feed dati](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Se l&#39;AACUSTOMID è presente, l&#39;AAID sarà basato sull&#39;AACUSTOMID perché l&#39;AACUSTOMID trumpa tutti gli altri identificatori come definito dal [ordine delle operazioni [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Come funziona [!DNL Analytics] la fonte tratta le identità

La [!DNL Analytics] source trasmette queste identità ad Experience Platform in formato XDM come:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Questi campi non sono contrassegnati come identità. Invece, le stesse identità vengono copiate in XDM `identityMap` come coppie chiave-valore:

* `{ “key”: “AAID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “ECID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “AACUSTOMID”, “value”: [ { “id”: “<identity>”, “primary”: false } ] }`

Nella mappa di identità, se ECID è presente, viene contrassegnato come identità principale per l’evento. In questo caso, AAID può essere basato su ECID a causa della [Periodo di tolleranza per il servizio Identity](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). In caso contrario, AAID è contrassegnato come identità primaria dell’evento. AACUSTOMID non viene mai contrassegnato come ID primario dell’evento. Tuttavia, se AACUSTOMID è presente, AAID si basa su AACUSTOMID a causa dell’ordine Experience Cloud delle operazioni.