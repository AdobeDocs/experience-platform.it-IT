---
keywords: Experience Platform;home;popular topics;segment evaluation
solution: Experience Platform
title: Valutazione di un segmento
topic: tutorial
description: Questo documento fornisce un'esercitazione per valutare i segmenti e accedere ai risultati dei segmenti utilizzando l'API Segmentazione.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 0%

---


# Valutazione e accesso ai risultati dei segmenti

Questo documento fornisce un&#39;esercitazione per la valutazione dei segmenti e l&#39;accesso ai risultati dei segmenti mediante l&#39; [!DNL Segmentation API](../api/getting-started.md).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [!DNL Adobe Experience Platform Segmentation Service](../home.md): Consente di creare segmenti di pubblico dai [!DNL Real-time Customer Profile] dati.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

### Intestazioni necessarie

Questa esercitazione richiede anche di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate alle [!DNL Platform] API. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui si svolgerà l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste di POST, PUT e PATCH richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Valutazione di un segmento

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutare il segmento tramite una valutazione programmata o su richiesta.

[La valutazione](#scheduled-evaluation) pianificata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per l’esecuzione di un processo di esportazione in un momento specifico, mentre la valutazione [](#on-demand-evaluation) su richiesta comporta la creazione di un processo segmento per creare immediatamente l’audience. Di seguito sono descritti i passaggi da seguire per ciascuno di essi.

Se non hai ancora completato la [creazione di un segmento tramite l’esercitazione API](./create-a-segment.md) di segmentazione o hai creato una definizione di segmento con [Segment Builder](../ui/overview.md), effettua questa operazione prima di continuare con questa esercitazione.

## Valutazione programmata {#scheduled-evaluation}

Mediante la valutazione pianificata, l’organizzazione IMS può creare una pianificazione periodica per eseguire automaticamente i processi di esportazione.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se l&#39;organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] un unico ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

### Creare una pianificazione

Eseguendo una richiesta POST all&#39; `/config/schedules` endpoint, potete creare una pianificazione e includere l&#39;ora specifica in cui attivare la pianificazione.

Per informazioni più dettagliate sull&#39;utilizzo di questo endpoint, consultate la guida all&#39;endpoint delle [pianificazioni.](../api/schedules.md#create)

### Attivare una pianificazione

Per impostazione predefinita, una pianificazione è inattiva quando viene creata, a meno che la `state` proprietà non sia impostata `active` nel corpo della richiesta di creazione (POST). Potete abilitare una pianificazione (impostate `state` su `active`) effettuando una richiesta di PATCH all&#39; `/config/schedules` endpoint e includendo l&#39;ID della pianificazione nel percorso.

Per informazioni più dettagliate sull&#39;utilizzo di questo endpoint, consultate la guida all&#39;endpoint delle [pianificazioni.](../api/schedules.md#update-state)

### Aggiornamento dell&#39;ora di pianificazione

È possibile aggiornare i tempi di programmazione eseguendo una richiesta di PATCH all&#39; `/config/schedules` endpoint e includendo l&#39;ID della pianificazione nel percorso.

Per informazioni più dettagliate sull&#39;utilizzo di questo endpoint, consultate la guida all&#39;endpoint delle [pianificazioni.](../api/schedules.md#update-schedule)

## Valutazione su richiesta

La valutazione su richiesta consente di creare un processo di segmento per generare un segmento di pubblico ogni volta che lo desiderate. A differenza della valutazione pianificata, ciò si verificherà solo se richiesto e non ricorrente.

### Creazione di un processo di segmento

Un processo di segmento è un processo asincrono che crea un nuovo segmento di pubblico. Fa riferimento a una definizione di segmento, nonché a qualsiasi criterio di unione che controlli il modo in cui [!DNL Real-time Customer Profile] unisce gli attributi sovrapposti nei frammenti di profilo. Quando un processo del segmento viene completato correttamente, potete raccogliere varie informazioni sul segmento, ad esempio eventuali errori che si sono verificati durante l&#39;elaborazione e le dimensioni finali del pubblico.

Puoi creare un nuovo processo per segmenti effettuando una richiesta di POST all’ `/segment/jobs` endpoint nell’ [!DNL Real-time Customer Profile] API.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella guida all’endpoint dei processi [del segmento](../api/segment-jobs.md#create)


### Cerca stato processo segmento

È possibile utilizzare l&#39; `id` per un processo segmento specifico per eseguire una richiesta di ricerca (GET) al fine di visualizzare lo stato corrente del processo.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella guida all’endpoint dei processi [del segmento](../api/segment-jobs.md#get)

## Interpreta i risultati del segmento

Quando i processi del segmento vengono eseguiti correttamente, la `segmentMembership` mappa viene aggiornata per ogni profilo incluso nel segmento. `segmentMembership` memorizza inoltre tutti i segmenti di pubblico pre-valutati a cui vengono inviati [!DNL Platform], consentendo l&#39;integrazione con altre soluzioni come [!DNL Adobe Audience Manager].

L&#39;esempio seguente mostra l&#39;aspetto `segmentMembership` dell&#39;attributo per ciascun record di profilo:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `lastQualificationTime` | La marca temporale in cui è stata rilasciata l&#39;asserzione dell&#39;appartenenza al segmento e il profilo è entrato o uscito dal segmento. |
| `status` | Stato della partecipazione al segmento come parte della richiesta corrente. Deve essere uguale a uno dei seguenti valori noti: <ul><li>`existing`: L&#39;entità continua a trovarsi nel segmento.</li><li>`realized`: L&#39;entità sta entrando nel segmento.</li><li>`exited`: L&#39;entità sta uscendo dal segmento.</li></ul> |

## Accesso ai risultati del segmento

È possibile accedere ai risultati di un processo segmento in uno dei due modi seguenti: puoi accedere a singoli profili o esportare un&#39;intera audience in un dataset.

Le sezioni seguenti descrivono queste opzioni in modo più dettagliato.

## Cercare un profilo

Se conoscete il profilo specifico a cui desiderate accedere, potete farlo utilizzando l&#39; [!DNL Real-time Customer Profile] API. I passaggi completi per accedere ai singoli profili sono disponibili nei dati [Access Real-time Customer Profile (Profilo cliente in tempo reale) tramite l&#39;esercitazione Profile API](../../profile/api/entities.md) (API profilo).

## Esportare un segmento {#export}

Dopo che un processo di segmentazione è stato completato correttamente (il valore dell&#39; `status` attributo è &quot;SUCCEEDED&quot;), potete esportare il pubblico in un set di dati in cui è possibile accedervi e agire.

Per esportare il pubblico sono necessari i seguenti passaggi:

- [Crea un set di dati](#create-a-target-dataset) di destinazione: crea il set di dati per contenere i membri del pubblico.
- [Genera profili di pubblico nel set di dati](#generate-profiles-for-audience-members) - Compilare il set di dati con i singoli profili XDM in base ai risultati di un processo di segmento.
- [Monitorare l&#39;avanzamento](#monitor-export-progress) dell&#39;esportazione - Verificare l&#39;avanzamento corrente del processo di esportazione.
- [Leggi i dati](#next-steps) sul pubblico - Recupera i singoli profili XDM risultanti che rappresentano i membri del pubblico.

### Creare un dataset di destinazione

Quando si esporta un&#39;audience, è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire il successo dell&#39;esportazione.

Una delle considerazioni chiave è lo schema su cui si basa il dataset (`schemaRef.id` nella richiesta di esempio API di seguito). Per esportare un segmento, il dataset deve essere basato sul [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe, in questo caso si tratta della classe XDM Singolo profilo. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, vedere la sezione Profilo cliente in tempo [reale della guida](../../xdm/api/getting-started.md)per gli sviluppatori del Registro di sistema dello schema.

Esistono due modi per creare il set di dati necessario:

- **Utilizzo delle API:** I passaggi che seguono in questa esercitazione descrivono come creare un set di dati che faccia riferimento a tale oggetto [!DNL XDM Individual Profile Union Schema] utilizzando l&#39; [!DNL Catalog] API.
- **Utilizzo dell’interfaccia utente:** Per utilizzare l&#39;interfaccia [!DNL Adobe Experience Platform] utente per creare un dataset che faccia riferimento allo schema dell&#39;unione, seguire i passaggi dell&#39;esercitazione [dell&#39;](../ui/overview.md) interfaccia utente, quindi tornare a questa esercitazione per procedere con i passaggi necessari per la [generazione dei profili](#generate-xdm-profiles-for-audience-members)dell&#39;audience.

Se disponete già di un set di dati compatibile e ne conoscete l’ID, potete procedere direttamente alla fase di [generazione dei profili](#generate-xdm-profiles-for-audience-members)di audience.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un nuovo dataset, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome descrittivo per il set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui sarà associato il set di dati. |
| `fileDescription.persisted` | Un valore booleano che, se impostato su `true`, consente al dataset di persistere nella visualizzazione unione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID univoco generato dal sistema di sola lettura del set di dati appena creato. Per esportare correttamente i membri dell&#39;audience è necessario un ID dataset configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generazione di profili per i membri dell&#39;audience {#generate-profiles}

Una volta ottenuto un dataset persistente nell&#39;unione, potete creare un processo di esportazione per mantenere i membri dell&#39;audience nel dataset effettuando una richiesta di POST all&#39; `/export/jobs` endpoint nell&#39; [!DNL Real-time Customer Profile] API e fornendo l&#39;ID del set di dati e le informazioni sul segmento per i segmenti che desiderate esportare.

Ulteriori informazioni sull&#39;utilizzo di questo endpoint sono disponibili nella guida all&#39;endpoint dei processi di [esportazione](../api/export-jobs.md#create)

### Monitorare l&#39;avanzamento dell&#39;esportazione

Come processo di esportazione, potete controllarne lo stato effettuando una richiesta di GET all’ `/export/jobs` endpoint e includendo nel percorso `id` il processo di esportazione. Il processo di esportazione viene completato una volta che il `status` campo restituisce il valore &quot;SUCCEEDED&quot;.

Ulteriori informazioni sull&#39;utilizzo di questo endpoint sono disponibili nella guida all&#39;endpoint dei processi di [esportazione](../api/export-jobs.md#get)

## Passaggi successivi

Una volta completata l&#39;esportazione, i dati sono disponibili all&#39;interno del [!DNL Data Lake] modulo [!DNL Experience Platform]. È quindi possibile utilizzare l’icona [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) per accedere ai dati utilizzando l’icona `batchId` associata all’esportazione. A seconda della dimensione del segmento, i dati possono essere in blocchi e il batch può essere composto da diversi file.

Per istruzioni dettagliate su come utilizzare l&#39; [!DNL Data Access] API per accedere e scaricare file batch, segui l&#39;esercitazione [sull&#39;accesso ai](../../data-access/tutorials/dataset-data.md)dati.

Puoi anche accedere ai dati del segmento esportati correttamente utilizzando [!DNL Adobe Experience Platform Query Service]. L’utilizzo dell’interfaccia utente o dell’API RESTful [!DNL Query Service] consente di scrivere, convalidare ed eseguire query sui dati all’interno dell’ [!DNL Data Lake].

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la documentazione in [!DNL Query Service](../../query-service/home.md).
