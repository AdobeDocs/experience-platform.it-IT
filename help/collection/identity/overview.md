---
title: Identità nella raccolta dati
description: Scopri come la raccolta dati utilizza ECID, ID CORE, persistenza di prime parti e identityMap nelle implementazioni web.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identità nella raccolta dati

La raccolta dati di Adobe utilizza i segnali di identità per riconoscere i visitatori di ritorno e fornire un contesto per le diverse esperienze. Quando un visitatore raggiunge il sito, Edge Network genera un Experience Cloud ID (ECID) e lo salva in un cookie di prime parti. Tale ECID è l’identificatore primario del dispositivo utilizzato nelle applicazioni Adobe Experience Cloud ed è la base su cui si basano analisi, personalizzazione e attivazione del pubblico. Nella tua implementazione, puoi accedere all&#39;ECID del visitatore sul lato client tramite il comando [`getIdentity`](/help/collection/js/commands/getidentity.md). A livello di flusso di dati, puoi utilizzare [Preparazione dati per raccolta dati](/help/datastreams/data-prep.md) per mappare l&#39;ECID in un campo XDM personalizzato prima che raggiunga i servizi a valle.

L’ECID identifica un dispositivo, non una persona. Per collegare l&#39;attività a una persona nota, è possibile inviare identificatori aggiuntivi, ad esempio un ID CRM o un&#39;e-mail con hash, insieme all&#39;ECID utilizzando XDM [`identityMap`](./identity-map.md). Adobe consiglia di impostare uno spazio dei nomi a livello di persona come [identità primaria](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) ogni volta che ne è disponibile una.

Oltre all’ECID predefinito, Data Collection supporta segnali di identità aggiuntivi a seconda dell’implementazione:

* **ID dispositivo di prime parti (FPID)**: identificatori di dispositivo generati e gestiti nell&#39;infrastruttura controllata. Edge Network utilizza un FPID per [inizializzare l&#39;ECID](./fpid.md), fornendo una maggiore persistenza dei cookie sulle proprietà possedute quando le restrizioni del browser riducono la durata dei cookie gestiti da Adobe.
* **ID CORE**: un identificatore separato basato su demdex che partecipa ai flussi di lavoro di identità di terze parti quando sono disponibili cookie di terze parti. L&#39;ID CORE è diverso dall&#39;ECID e può essere recuperato tramite [`getIdentity`](/help/collection/js/commands/getidentity.md). Per informazioni dettagliate sulla collaborazione tra contesti di identità di prime e terze parti, vedere [Supporto identità unificata](./unified-identity-support.md).

Se stai eseguendo l&#39;aggiornamento dall&#39;API Visitor o la riconciliazione del comportamento di identità precedente, consulta [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) per eseguire la migrazione dei cookie AMCV esistenti.

## Raccolta di prime e terze parti {#first-party-and-third-party-collection}

Il Web SDK imposta sempre l&#39;identità [cookie](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) (ad esempio `kndctr_` cookie) come cookie di prime parti nel dominio, indipendentemente dall&#39;endpoint che riceve la richiesta di raccolta dati. L’endpoint di raccolta (il dominio a cui l’implementazione invia i dati) è una scelta separata che influisce sul modo in cui browser e criteri di rete gestiscono la richiesta stessa.

**La raccolta di prime parti** indirizza le richieste di raccolta dati tramite un dominio controllato dall&#39;organizzazione (ad esempio, `data.example.com`), utilizzando un CNAME che punta a Adobe Edge Network. Poiché la richiesta rimane nel dominio, è meno probabile che venga bloccata da ad blocker o restrizioni di rete del browser. La raccolta di prime parti è anche un prerequisito per impostare [ID dispositivo di prime parti](./fpid.md) dalla propria infrastruttura server, che è la strategia di identità più durevole disponibile. Adobe consiglia di utilizzare il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) per configurare la raccolta di prime parti per l&#39;implementazione.

**La raccolta di terze parti** invia le richieste direttamente a un [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) di proprietà di Adobe (ad esempio `example.data.adobedc.net`). Anche se i cookie di identità sono ancora impostati come cookie di prima parte sul tuo dominio, la richiesta stessa passa a un dominio di terze parti, che alcuni browser e ad blocker possono limitare.

## Scegli il giusto pattern di identità {#choose-your-path}

* **Rafforzare la persistenza delle identità nelle proprietà possedute**: utilizza [ID dispositivo di prime parti](./fpid.md) quando le restrizioni del browser riducono la durata dei cookie e hai bisogno di una maggiore continuità per l&#39;analisi e la personalizzazione nei siti che controlli.
* **Distribuisci l&#39;identità da un&#39;app al Web per dispositivi mobili**: utilizza [la condivisione di identità da dispositivo mobile a Web](./mobile-to-web.md) quando il visitatore inizia nell&#39;app mobile e continua in una pagina Web Web WebView o mobile.
* **Mantenere l&#39;identità continua nei domini**: utilizza la [condivisione tra domini](./cross-domain-sharing.md) quando i visitatori passano da una proprietà Web di proprietà della tua organizzazione e desideri ottenere rapporti e personalizzazioni coerenti.
* **Combina la persistenza di prime parti con l&#39;attivazione di terze parti**: utilizza il [supporto Unified Identity](./unified-identity-support.md) quando hai bisogno di un&#39;identificazione di prime parti durevole insieme ai flussi di attivazione di terze parti supportati.
* **Invia identificatori a livello di persona**: utilizza [`identityMap`](./identity-map.md) per inviare ID CRM, e-mail con hash e altri identificatori a livello di persona insieme all&#39;ECID in modo che i servizi a valle possano unire l&#39;attività a una persona nota.
* **Comprendere come il consenso influisce sull&#39;identità**: leggere [Consenso e identità](./consent.md) per scoprire come `defaultConsent` e `setConsent` controllano quando Web SDK genera un ECID, imposta i cookie e invia i dati.

Per informazioni su come diagnosticare i problemi di identità, ad esempio l&#39;inflazione dei visitatori, le incoerenze ECID o i problemi FPID, consulta [Risoluzione dei problemi di identità](./troubleshooting.md).
