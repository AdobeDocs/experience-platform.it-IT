---
keywords: Experience Platform;api di destinazione;attivazione ad hoc;attivare segmenti ad hoc
solution: Experience Platform
title: Attivare i segmenti di pubblico in destinazioni batch tramite l’API di attivazione ad hoc
description: Questo articolo illustra il flusso di lavoro end-to-end per l’attivazione di segmenti di pubblico tramite l’API di attivazione ad hoc, inclusi i processi di segmentazione che si verificano prima dell’attivazione.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# Attivare i segmenti di pubblico on-demand nelle destinazioni batch tramite l’API di attivazione ad hoc

>[!IMPORTANT]
>
>Dopo aver completato la fase Beta, [!DNL ad-hoc activation API] è ora generalmente disponibile (GA) per tutti i clienti Experience Platform. Nella versione GA, l’API è stata aggiornata alla versione 2. Passaggio 4 ([Ottenere l’ID del processo di esportazione del segmento più recente](#segment-export-id)) non è più richiesto, in quanto l’API non richiede più l’ID di esportazione.
>
>Consulta [Eseguire il processo di attivazione ad hoc](#activation-job) più avanti in questo tutorial per ulteriori informazioni.

## Panoramica {#overview}

L’API di attivazione ad hoc consente agli addetti al marketing di attivare in modo programmatico i segmenti di pubblico nelle destinazioni, in modo rapido ed efficiente, per le situazioni in cui è richiesta l’attivazione immediata.

Utilizza l’API di attivazione ad hoc per esportare file completi nel sistema di ricezione dei file desiderato. L’attivazione ad hoc del pubblico è supportata solo da [destinazioni basate su file batch](../destination-types.md#file-based).

Il diagramma seguente illustra il flusso di lavoro end-to-end per l’attivazione dei segmenti tramite l’API di attivazione ad-hoc, inclusi i processi di segmentazione che si svolgono in Platform ogni 24 ore.

![ad-hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## Casi d’uso {#use-cases}

### Vendite o promozioni Flash

Un rivenditore online sta preparando una vendita flash limitata e desidera avvisare i clienti con un breve preavviso. Tramite l’API di attivazione ad hoc di Experience Platform, il team marketing può esportare i segmenti on-demand e inviare rapidamente e-mail promozionali alla base clienti.

### Attualità o ultime notizie

Un hotel si aspetta un tempo inclemente nei giorni successivi e il team vuole informare rapidamente gli ospiti in arrivo, in modo che possano pianificare di conseguenza. Il team marketing può utilizzare l’API di attivazione ad hoc di Experience Platform per esportare i segmenti su richiesta e avvisare gli ospiti.

### Test di integrazione

I responsabili IT possono utilizzare l’API di attivazione ad hoc di Experience Platform per esportare i segmenti su richiesta, in modo da testare la loro integrazione personalizzata con Adobe Experience Platform e garantire il corretto funzionamento di tutto.

## Guardrail {#guardrails}

Quando utilizzi l’API di attivazione ad hoc, tieni presenti le seguenti protezioni.

* Attualmente, ogni processo di attivazione ad hoc può attivare fino a 80 segmenti. Se si tenta di attivare più di 80 segmenti per processo, il processo non riesce. Questo comportamento è soggetto a modifiche nelle versioni future.
* I processi di attivazione ad hoc non possono essere eseguiti in parallelo con i processi pianificati [processi di esportazione del segmento](../../segmentation/api/export-jobs.md). Prima di eseguire un processo di attivazione ad hoc, accertati che il processo di esportazione del segmento pianificato sia stato completato. Consulta [monitoraggio del flusso di dati di destinazione](../../dataflows/ui/monitor-destinations.md) per informazioni su come monitorare lo stato dei flussi di attivazione. Ad esempio, se il flusso di dati di attivazione mostra **[!UICONTROL Elaborazione]** stato, attendi il termine prima di eseguire il processo di attivazione ad hoc.
* Non eseguire più di un processo di attivazione ad hoc simultaneo per segmento.

## Considerazioni sulla segmentazione {#segmentation-considerations}

Adobe Experience Platform esegue processi di segmentazione pianificati una volta ogni 24 ore. L’API di attivazione ad hoc viene eseguita in base ai risultati di segmentazione più recenti.

## Passaggio 1: Prerequisiti {#prerequisites}

Prima di poter effettuare chiamate alle API di Adobe Experience Platform, assicurati di soddisfare i seguenti prerequisiti:

* Hai un account organizzazione con accesso a Adobe Experience Platform.
* Il tuo account di Experience Platform ha `developer` e `user` ruoli abilitati per il profilo di prodotto API Adobe Experience Platform. Contatta il tuo [Admin Console](../../access-control/home.md) per abilitare questi ruoli per il tuo account.
* Hai un Adobe ID. Se non disponi di un Adobe ID, vai al [Console Adobe Developer](https://developer.adobe.com/console) e crea un nuovo account.

## Passaggio 2: raccogliere le credenziali {#credentials}

Per effettuare chiamate alle API di Platform, devi prima completare la sezione [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse di Experience Platform possono essere isolate in specifiche sandbox virtuali. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui verrà eseguita l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la sezione [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Passaggio 3: creare un flusso di attivazione nell’interfaccia utente di Platform {#activation-flow}

Prima di poter attivare i segmenti tramite l’API di attivazione ad hoc, è necessario aver configurato un flusso di attivazione nell’interfaccia utente di Platform, per la destinazione scelta.

Ciò include l’accesso al flusso di lavoro di attivazione, la selezione dei segmenti, la configurazione di una pianificazione e l’attivazione. Puoi utilizzare l’interfaccia o l’API per creare un flusso di attivazione:

* [Utilizza l’interfaccia utente di Platform per creare un flusso di attivazione per le destinazioni di esportazione del profilo batch](../ui/activate-batch-profile-destinations.md)
* [Utilizza l’API del servizio Flusso per connettersi alle destinazioni di esportazione dei profili batch e attivare i dati](../api/connect-activate-batch-destinations.md)

## Passaggio 4: ottieni l’ID del processo di esportazione del segmento più recente (non richiesto nella versione v2) {#segment-export-id}

>[!IMPORTANT]
>
>Nella versione 2 dell’API di attivazione ad hoc, non è necessario ottenere l’ID del processo di esportazione del segmento più recente. Puoi saltare questo passaggio e passare a quello successivo.

Dopo aver configurato un flusso di attivazione per la destinazione batch, i processi di segmentazione pianificati iniziano a essere eseguiti automaticamente ogni 24 ore.

Prima di poter eseguire il processo di attivazione ad hoc, è necessario ottenere l’ID del processo di esportazione del segmento più recente. Devi passare questo ID nella richiesta del processo di attivazione ad hoc.

Seguire le istruzioni descritte [qui](../../segmentation/api/export-jobs.md#retrieve-list) per recuperare un elenco di tutti i processi di esportazione del segmento.

Nella risposta, cerca il primo record che include la proprietà dello schema seguente.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

L’ID del processo di esportazione del segmento è nel `id` come mostrato di seguito.

![ID processo esportazione segmento](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Passaggio 5: eseguire il processo di attivazione ad hoc {#activation-job}

Adobe Experience Platform esegue processi di segmentazione pianificati una volta ogni 24 ore. L’API di attivazione ad hoc viene eseguita in base ai risultati di segmentazione più recenti.

>[!IMPORTANT]
>
>Nota il seguente vincolo relativo all’attivazione una tantum: prima di eseguire un processo di attivazione ad hoc, assicurati che siano trascorsi almeno 20 minuti dal momento in cui il segmento è stato attivato per la prima volta in base alla pianificazione impostata in [Passaggio 3: creare un flusso di attivazione nell’interfaccia utente di Platform](#activation-flow).

Prima di eseguire un processo di attivazione ad hoc, accertati che il processo di esportazione dei segmenti pianificato per i segmenti sia stato completato. Consulta [monitoraggio del flusso di dati di destinazione](../../dataflows/ui/monitor-destinations.md) per informazioni su come monitorare lo stato dei flussi di attivazione. Ad esempio, se il flusso di dati di attivazione mostra **[!UICONTROL Elaborazione]** stato, attendi il termine prima di eseguire il processo di attivazione ad hoc per esportare un file completo.

Una volta completato il processo di esportazione del segmento, puoi attivare l’attivazione.

>[!NOTE]
>
>Attualmente, ogni processo di attivazione ad hoc può attivare fino a 80 segmenti. Se si tenta di attivare più di 80 segmenti per processo, il processo non riesce. Questo comportamento è soggetto a modifiche nelle versioni future.

### Richiesta {#request}

>[!IMPORTANT]
>
>È obbligatorio includere `Accept: application/vnd.adobe.adhoc.activation+json; version=2` nella richiesta per utilizzare la v2 dell’API di attivazione ad hoc.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Gli ID delle istanze di destinazione a cui desideri attivare i segmenti. Puoi ottenere questi ID dall’interfaccia utente di Platform, passando a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e facendo clic sulla riga di destinazione desiderata per visualizzare l’ID di destinazione nella barra a destra. Per ulteriori informazioni, leggere [documentazione di destination workspace](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Gli ID dei segmenti che desideri attivare nella destinazione selezionata. |

{style="table-layout:auto"}

### Richiesta con ID esportazione (da rendere obsoleto) {#request-deprecated}

>[!IMPORTANT]
>
>**Tipo di richiesta obsoleto**. Questo tipo di esempio descrive il tipo di richiesta per l’API versione 1. Nella versione 2 dell’API di attivazione ad hoc, non è necessario includere l’ID del processo di esportazione del segmento più recente.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
   "exportIds":[
      "exportId1"
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Gli ID delle istanze di destinazione a cui desideri attivare i segmenti. Puoi ottenere questi ID dall’interfaccia utente di Platform, passando a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e facendo clic sulla riga di destinazione desiderata per visualizzare l’ID di destinazione nella barra a destra. Per ulteriori informazioni, leggere [documentazione di destination workspace](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Gli ID dei segmenti che desideri attivare nella destinazione selezionata. |
| <ul><li>`exportId1`</li></ul> | L&#39;ID restituito nella risposta del [esportazione di segmenti](../../segmentation/api/export-jobs.md#retrieve-list) lavoro. Consulta [Passaggio 4: ottieni l’ID del processo di esportazione del segmento più recente](#segment-export-id) per istruzioni su come trovare questo ID. |

{style="table-layout:auto"}

### Risposta {#response}

Una risposta corretta restituisce lo stato HTTP 200.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segment` | ID del segmento attivato. |
| `order` | ID della destinazione in cui è stato attivato il segmento. |
| `statusURL` | URL dello stato del flusso di attivazione. Puoi tenere traccia dell’avanzamento del flusso utilizzando [API del servizio Flusso](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

### Codici di errore API e messaggi specifici per l’API di attivazione ad hoc {#specific-error-messages}

Quando utilizzi l’API di attivazione ad hoc, puoi incontrare messaggi di errore specifici per questo endpoint API. Rivedi la tabella per capire come gestirli quando vengono visualizzati.

| Messaggio di errore | Risoluzione |
|---------|----------|
| Esecuzione già in corso per il segmento `segment ID` per ordine `dataflow ID` con id esecuzione `flow run ID` | Questo messaggio di errore indica che per un segmento è attualmente in corso un flusso di attivazione ad hoc. Attendere il completamento del processo prima di riattivarlo. |
| Segmenti `<segment name>` non fanno parte di questo flusso di dati o non rientrano nell’intervallo di pianificazione. | Questo messaggio di errore indica che i segmenti selezionati per l’attivazione non sono mappati al flusso di dati o che la pianificazione di attivazione impostata per i segmenti è scaduta o non è ancora iniziata. Controlla se il segmento è effettivamente mappato al flusso di dati e verifica che la pianificazione di attivazione del segmento si sovrapponga alla data attuale. |

## Informazioni correlate {#related-information}

* [Connettersi alle destinazioni batch e attivare i dati utilizzando l’API del servizio Flusso](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experience Platform](/help/destinations/ui/export-file-now.md)