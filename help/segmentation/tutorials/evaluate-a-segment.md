---
keywords: Experience Platform;home;argomenti popolari;valutazione segmento;Segmentation Service;segmentation;segmentation;evaluate a segment;access segment results;evaluate and access segment; (Segmentazione;segmentazione;valutare un segmento;accedere ai risultati del segmento;valutare e accedere al segmento;
solution: Experience Platform
title: Valutare e accedere ai risultati dei segmenti
type: Tutorial
description: Segui questa esercitazione per scoprire come valutare i segmenti e accedere ai risultati dei segmenti utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Valutare e accedere ai risultati dei segmenti

Questo documento fornisce un’esercitazione per valutare i segmenti e accedere ai risultati dei segmenti utilizzando [[!DNL Segmentation API]](../api/getting-started.md).

## Introduzione

Questo tutorial richiede una buona conoscenza delle varie [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare segmenti di pubblico da [!DNL Real-Time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale Platform organizza i dati sull’esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Intestazioni richieste

Questo tutorial richiede anche di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate a [!DNL Platform] API. Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste di POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Valutare un segmento {#evaluate-a-segment}

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutarlo tramite valutazione pianificata o su richiesta.

[Valutazione programmata](#scheduled-evaluation) (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione ricorrente per l’esecuzione di un processo di esportazione in un momento specifico, mentre [valutazione on-demand](#on-demand-evaluation) implica la creazione di un processo di segmentazione per generare immediatamente il pubblico. Di seguito sono descritti i passaggi per ciascuno di essi.

Se non hai ancora completato [creare un segmento utilizzando l’API di segmentazione](./create-a-segment.md) esercitazione o ha creato una definizione di segmento utilizzando [Generatore di segmenti](../ui/overview.md), esegui questa operazione prima di procedere con questa esercitazione.

## Valutazione programmata {#scheduled-evaluation}

Tramite la valutazione pianificata, l’organizzazione può creare una pianificazione ricorrente per eseguire automaticamente i processi di esportazione.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se nell’organizzazione sono presenti più di cinque criteri di unione per [!DNL XDM Individual Profile] in un singolo ambiente sandbox non puoi utilizzare la valutazione pianificata.

### Creare una pianificazione

Effettuando una richiesta POST al `/config/schedules` endpoint, puoi creare una pianificazione e includere l’ora specifica in cui attivare la pianificazione.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;schedule&quot;](../api/schedules.md#create)

### Abilitare una pianificazione

Per impostazione predefinita, una pianificazione non è attiva al momento della creazione, a meno che `state` proprietà impostata su `active` nel corpo della richiesta create (POST). È possibile abilitare una pianificazione (impostare `state` a `active`) inoltrando una richiesta PATCH al `/config/schedules` e l&#39;ID della pianificazione nel percorso.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;schedule&quot;](../api/schedules.md#update-state)

### Aggiornare l’ora di pianificazione

È possibile aggiornare la pianificazione effettuando una richiesta PATCH al `/config/schedules` e l&#39;ID della pianificazione nel percorso.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;schedule&quot;](../api/schedules.md#update-schedule)

## Valutazione a richiesta

La valutazione su richiesta consente di creare un processo di segmentazione per generare un segmento di pubblico ogni volta che necessario. A differenza della valutazione pianificata, questa si verifica solo quando richiesto e non è ricorrente.

### Creare un processo di segmentazione

Un processo di segmentazione è un processo asincrono che crea un segmento di pubblico su richiesta. Fa riferimento a una definizione di segmento, nonché a eventuali criteri di unione che controllano come [!DNL Real-Time Customer Profile] unisce attributi sovrapposti tra i frammenti di profilo. Al termine di un processo di segmentazione, puoi raccogliere varie informazioni sul segmento, ad esempio eventuali errori che si sono verificati durante l’elaborazione e le dimensioni finali del pubblico. È necessario eseguire un processo di segmentazione ogni volta che desideri aggiornare il pubblico attualmente idoneo per la definizione del segmento.

Per creare un nuovo processo di segmentazione, devi effettuare una richiesta POST al `/segment/jobs` endpoint nella [!DNL Real-Time Customer Profile] API.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;segment jobs&quot;](../api/segment-jobs.md#create)

### Cercare lo stato del processo di segmento

È possibile utilizzare `id` per un processo di segmento specifico per eseguire una richiesta di ricerca (GET) per visualizzare lo stato corrente del processo.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;segment jobs&quot;](../api/segment-jobs.md#get)

## Interpretare i risultati dei segmenti

Quando i processi di segmentazione vengono eseguiti correttamente, il `segmentMembership` La mappa viene aggiornata per ogni profilo incluso nel segmento. `segmentMembership` memorizza anche eventuali segmenti di pubblico pre-valutati che vengono acquisiti in [!DNL Platform], consentendo l&#39;integrazione con altre soluzioni come [!DNL Adobe Audience Manager].

Nell&#39;esempio seguente viene illustrato il `segmentMembership` per ogni singolo record di profilo:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | La marca temporale in cui è stata effettuata l’asserzione di appartenenza al segmento e il profilo è entrato o uscito dal segmento. |
| `status` | Lo stato di partecipazione al segmento come parte della richiesta corrente. Deve essere uguale a uno dei seguenti valori noti: <ul><li>`realized`: entità qualificata per il segmento.</li><li>`exited`: uscita dell’entità dal segmento.</li></ul> |

>[!NOTE]
>
>Qualsiasi appartenenza a un segmento presente in `exited` per più di 30 giorni, in base al `lastQualificationTime`, sarà soggetto a cancellazione.

## Accedere ai risultati dei segmenti

È possibile accedere ai risultati di un processo di segmentazione in uno dei due modi seguenti: accedere a singoli profili o esportare un intero pubblico in un set di dati.

Le sezioni seguenti descrivono queste opzioni in modo più dettagliato.

## Cercare un profilo

Se conosci il profilo specifico a cui desideri accedere, utilizza [!DNL Real-Time Customer Profile] API. I passaggi completi per accedere ai singoli profili sono disponibili nella sezione [Accedere ai dati del profilo cliente in tempo reale utilizzando l’API del profilo](../../profile/api/entities.md) esercitazione.

## Esportare un segmento {#export}

Dopo il completamento di un processo di segmentazione (il valore della `status` è &quot;RIUSCITO&quot;), puoi esportare il pubblico in un set di dati in cui è possibile accedervi e agire di conseguenza.

Per esportare il pubblico, sono necessari i seguenti passaggi:

- [Creare un set di dati di destinazione](#create-a-target-dataset) : crea il set di dati per includere i membri del pubblico.
- [Generare profili di pubblico nel set di dati](#generate-profiles) : popola il set di dati con i singoli profili XDM in base ai risultati di un processo di segmentazione.
- [Monitorare l’avanzamento dell’esportazione](#monitor-export-progress) - Controllare l&#39;avanzamento corrente del processo di esportazione.
- [Lettura dei dati sul pubblico](#next-steps) : recupera i profili individuali XDM risultanti che rappresentano i membri del pubblico.

### Creare un set di dati di destinazione {#create-dataset}

Durante l’esportazione di un pubblico, è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire l’esportazione in modo corretto.

Una delle considerazioni chiave è lo schema su cui si basa il set di dati (`schemaRef.id` nella richiesta di esempio API (di seguito). Per esportare un segmento, il set di dati deve essere basato su [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema di unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe, in questo caso la classe XDM Individual Profile. Per ulteriori informazioni sugli schemi di visualizzazione unione, consulta la [Sezione Profilo cliente in tempo reale della guida per gli sviluppatori del registro dello schema](../../xdm/api/getting-started.md).

Esistono due modi per creare il set di dati necessario:

- **Utilizzo delle API:** I passaggi seguenti in questa esercitazione descrivono come creare un set di dati che faccia riferimento a [!DNL XDM Individual Profile Union Schema] utilizzando [!DNL Catalog] API.
- **Utilizzo dell’interfaccia utente:** Per utilizzare [!DNL Adobe Experience Platform] per creare un set di dati che faccia riferimento allo schema di unione, segui i passaggi descritti in [Esercitazione sull’interfaccia utente](../ui/overview.md) e quindi tornare a questo tutorial per procedere con i passaggi per [generazione di profili di pubblico](#generate-profiles).

Se disponi già di un set di dati compatibile e conosci il relativo ID, puoi procedere direttamente al passaggio per [generazione di profili di pubblico](#generate-profiles).

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un nuovo set di dati, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome descrittivo del set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui verrà associato il set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID univoco di sola lettura generato dal sistema per il set di dati appena creato. Per esportare correttamente i membri del pubblico è necessario un ID set di dati configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generare profili per i membri del pubblico {#generate-profiles}

Una volta che hai un set di dati persistente nell’unione, puoi creare un processo di esportazione per rendere persistenti i membri del pubblico nel set di dati effettuando una richiesta POST al `/export/jobs` endpoint nella [!DNL Real-Time Customer Profile] e fornendo l’ID del set di dati e le informazioni sul segmento per i segmenti che desideri esportare.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;export jobs&quot;](../api/export-jobs.md#create)

### Monitorare l’avanzamento dell’esportazione

Durante l’elaborazione di un processo di esportazione, puoi monitorarne lo stato effettuando una richiesta GET al `/export/jobs` e che include `id` del processo di esportazione nel percorso. Il processo di esportazione viene completato una volta che `status` restituisce il valore &quot;SUCCESSEDED&quot;.

Informazioni più dettagliate sull’utilizzo di questo endpoint sono disponibili nella sezione [guida dell’endpoint &quot;export jobs&quot;](../api/export-jobs.md#get)

## Passaggi successivi

Una volta completata correttamente l’esportazione, i dati sono disponibili all’interno di [!DNL Data Lake] in [!DNL Experience Platform]. È quindi possibile utilizzare [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) per accedere ai dati utilizzando `batchId` associato all’esportazione. A seconda delle dimensioni del segmento, i dati possono essere in blocchi e il batch può essere costituito da diversi file.

Per istruzioni dettagliate su come utilizzare il [!DNL Data Access] API per accedere e scaricare i file batch, seguire la [Tutorial sull’accesso ai dati](../../data-access/tutorials/dataset-data.md).

Puoi anche accedere ai dati dei segmenti esportati correttamente utilizzando [!DNL Adobe Experience Platform Query Service]. Utilizzando l’interfaccia utente o l’API RESTful, [!DNL Query Service] consente di scrivere, convalidare ed eseguire query sui dati all&#39;interno di [!DNL Data Lake].

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la documentazione su [[!DNL Query Service]](../../query-service/home.md).
