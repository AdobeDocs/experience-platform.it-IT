---
keywords: Experience Platform;api di destinazione;attivazione ad hoc;attivare segmenti ad hoc
solution: Experience Platform
title: (Beta) Attivare i segmenti di pubblico tramite l’API di attivazione ad hoc Experience Platform
description: Questo articolo illustra il flusso di lavoro end-to-end per l’attivazione dei segmenti tramite l’API di attivazione ad hoc, inclusi i processi di segmentazione che avvengono prima dell’attivazione.
topic-legacy: tutorial
type: Tutorial
source-git-commit: d5b383ec4e9f6e2f05a0e5834e3998789a67ce32
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 2%

---


# (Beta) Attivare i segmenti di pubblico tramite l’API di attivazione ad hoc Experience Platform

>[!IMPORTANT]
>
>La [!DNL ad-hoc activation API] in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

L’API di attivazione ad hoc consente agli addetti al marketing di attivare programmaticamente i segmenti di pubblico nelle destinazioni, in modo rapido ed efficiente, in situazioni in cui è richiesta l’attivazione immediata.

Il diagramma seguente illustra il flusso di lavoro end-to-end per l’attivazione dei segmenti tramite l’API di attivazione ad-hoc, inclusi i processi di segmentazione che si svolgono in Platform ogni 24 ore.

![attivazione ad hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>L’attivazione ad hoc del pubblico è supportata solo da [destinazioni batch basate su file](../destination-types.md#file-based).

## Casi di utilizzo {#use-cases}

### Vendite o promozioni Flash

Un rivenditore online sta preparando una vendita flash limitata e desidera avvisare i clienti con un breve preavviso. Tramite l’API di attivazione ad hoc Experience Platform, il team marketing può esportare segmenti di pubblico su richiesta e inviare rapidamente e-mail promozionali alla base clienti.


### Eventi attuali o novità

Un hotel si aspetta il tempo inclemente nei giorni successivi, e la squadra vuole informare rapidamente gli ospiti in arrivo, in modo che possano pianificare di conseguenza. Il team marketing può utilizzare l’API di attivazione ad hoc Experience Platform per esportare segmenti di pubblico su richiesta e avvisare gli ospiti.

### Test di integrazione

I responsabili IT possono utilizzare l’API di attivazione ad hoc di Experience Platform per esportare segmenti di pubblico su richiesta, in modo da testare la loro integrazione personalizzata con Adobe Experience Platform e assicurarsi che tutto funzioni correttamente.


## Guardrail {#guardrails}

Quando utilizzi l’API di attivazione ad-hoc, ricorda le seguenti protezioni.

* Ogni processo di attivazione ad-hoc può attivare fino a 20 segmenti. Se si tenta di attivare più di 20 segmenti per processo, il processo non riuscirà.
* I processi di attivazione ad hoc non possono essere eseguiti in parallelo con quelli pianificati [processi di esportazione dei segmenti](../../segmentation/api/export-jobs.md). Prima di eseguire un processo di attivazione ad hoc, assicurati che il processo di esportazione del segmento pianificato sia stato completato. Vedi [monitoraggio del flusso di dati di destinazione](../../dataflows/ui/monitor-destinations.md) per informazioni su come monitorare lo stato dei flussi di attivazione. Ad esempio, se il flusso di dati di attivazione mostra una **[!UICONTROL Elaborazione]** attendi che termini prima di eseguire il processo di attivazione ad-hoc.
* Non eseguire più di un processo di attivazione ad hoc simultaneo per segmento.

## Considerazioni sulla segmentazione {#segmentation-considerations}

Adobe Experience Platform esegue processi di segmentazione pianificati una volta ogni 24 ore. L’API di attivazione ad-hoc viene eseguita in base ai risultati di segmentazione più recenti.

## Passaggio 1: Prerequisiti {#prerequisites}

Prima di poter effettuare chiamate alle API di Adobe Experience Platform, verifica di soddisfare i seguenti prerequisiti:

* Hai un account organizzazione IMS con accesso a Adobe Experience Platform.
* Il tuo account Experience Platform ha `developer` e `user` ruoli abilitati per il profilo di prodotto API di Adobe Experience Platform. Contatta il tuo [Admin Console](../../access-control/home.md) amministratore per abilitare questi ruoli per il tuo account.
* Lei ha un Adobe ID. Se non disponi di un Adobe ID, passa alla pagina [Console per sviluppatori di Adobe](https://developer.adobe.com/console) e crea un nuovo account.

## Passaggio 2: Raccogli credenziali {#credentials}

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Le risorse in Experience Platform possono essere isolate in sandbox virtuali specifiche. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui avrà luogo l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la sezione [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Passaggio 3: Creare un flusso di attivazione nell’interfaccia utente di Platform {#activation-flow}

Prima di poter attivare i segmenti tramite l’API di attivazione ad hoc, devi prima disporre di un flusso di attivazione configurato nell’interfaccia utente di Platform per la destinazione selezionata.

Ciò include l&#39;accesso al flusso di lavoro di attivazione, la selezione dei segmenti, la configurazione di una pianificazione e l&#39;attivazione di tali segmenti.

Per istruzioni dettagliate su come configurare un flusso di attivazione per le destinazioni batch, consulta la seguente esercitazione: [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../ui/activate-batch-profile-destinations.md).

## Passaggio 4: Ottieni l&#39;ID più recente del processo di esportazione del segmento {#segment-export-id}

Dopo aver configurato un flusso di attivazione per la destinazione batch, i processi di segmentazione pianificati iniziano automaticamente ogni 24 ore.

Prima di poter eseguire il processo di attivazione ad hoc, devi ottenere l’ID dell’ultimo processo di esportazione del segmento. Devi trasmettere questo ID nella richiesta del processo di attivazione ad hoc.

Segui le istruzioni descritte [qui](../../segmentation/api/export-jobs.md#retrieve-list) per recuperare un elenco di tutti i processi di esportazione del segmento.

Nella risposta , cerca il primo record che include la proprietà schema seguente.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

L&#39;ID del processo di esportazione del segmento è nel `id` , come illustrato di seguito.

![ID processo di esportazione del segmento](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Passaggio 5: Esegui il processo di attivazione ad hoc {#activation-job}

Adobe Experience Platform esegue processi di segmentazione pianificati una volta ogni 24 ore. L’API di attivazione ad-hoc viene eseguita in base ai risultati di segmentazione più recenti.

Prima di eseguire un processo di attivazione ad hoc, assicurati che il processo di esportazione dei segmenti pianificato per i segmenti sia stato completato. Vedi [monitoraggio del flusso di dati di destinazione](../../dataflows/ui/monitor-destinations.md) per informazioni su come monitorare lo stato dei flussi di attivazione. Ad esempio, se il flusso di dati di attivazione mostra una **[!UICONTROL Elaborazione]** attendi che termini prima di eseguire il processo di attivazione ad-hoc.

Una volta completato il processo di esportazione del segmento, puoi attivare l’attivazione.

>[!WARNING]
>
>Puoi attivare un massimo di 50 segmenti per processo di attivazione ad hoc. Se si tenta di attivare più segmenti, il processo non riuscirà.

### Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportId":[
      "exportId1"
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | ID delle istanze di destinazione in cui desideri attivare i segmenti di pubblico. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | ID dei segmenti di pubblico che desideri attivare nella destinazione selezionata. |
| <ul><li>`exportId1`</li></ul> | L&#39;ID restituito nella risposta del [esportazione di segmenti](../../segmentation/api/export-jobs.md#retrieve-list) lavoro. Vedi [Passaggio 4: Ottieni l&#39;ID più recente del processo di esportazione del segmento](#segment-export-id) per istruzioni su come trovare questo ID. |

### Risposta

Una risposta corretta restituisce lo stato HTTP 200.

```shell
{
   "code":"DEST-ADH-200",
   "message":"Adhoc run triggered successfully",
   "statusURLs":[
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-1",
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-2"
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `code` | Il codice di risposta API. Viene restituita una chiamata corretta `DEST-ADH-200` (codice di stato 200), mentre un formato non corretto restituisce `DEST-ADH-400` (codice di stato 400). |
| `message` | Messaggio di errore o di successo restituito dall’API. |
| `statusURLs` | URL di stato del flusso di attivazione. Puoi tenere traccia dell’avanzamento del flusso utilizzando [API del servizio di flusso](../../sources/tutorials/api/monitor.md). |


## Gestione degli errori API

Gli endpoint API SDK di destinazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [errori di intestazione della richiesta](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) nella guida alla risoluzione dei problemi di Platform.
