---
solution: Experience Platform
title: Valutare e accedere ai risultati dei segmenti
type: Tutorial
description: Segui questo tutorial per scoprire come valutare le definizioni dei segmenti e accedere ai risultati della segmentazione utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 2%

---

# Valutare e accedere ai risultati della definizione dei segmenti

Questo documento fornisce un tutorial per valutare le definizioni dei segmenti e accedere a questi risultati utilizzando [[!DNL Segmentation API]](../api/getting-started.md).

## Introduzione

Questo tutorial richiede una buona conoscenza dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella creazione di tipi di pubblico. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull’esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Intestazioni richieste

Questo tutorial richiede anche di aver completato l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate alle API [!DNL Platform]. Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste di POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Valutare una definizione di segmento {#evaluate-a-segment}

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutarla tramite valutazione pianificata o su richiesta.

[La valutazione pianificata](#scheduled-evaluation) (nota anche come &#39;segmentazione pianificata&#39;) consente di creare una pianificazione ricorrente per l&#39;esecuzione di un processo di esportazione in un momento specifico, mentre la [valutazione on demand](#on-demand-evaluation) comporta la creazione di un processo di segmentazione per la generazione immediata del pubblico. Di seguito sono descritti i passaggi per ciascuno di essi.

Se non hai ancora completato la [creazione di una definizione di segmento utilizzando l&#39;esercitazione API](./create-a-segment.md) di segmentazione o creato una definizione di segmento utilizzando [Generatore di segmenti](../ui/segment-builder.md), esegui questa operazione prima di procedere con questa esercitazione.

## Valutazione programmata {#scheduled-evaluation}

Tramite la valutazione pianificata, l’organizzazione può creare una pianificazione ricorrente per eseguire automaticamente i processi di esportazione.

>[!NOTE]
>
>È possibile abilitare la valutazione pianificata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se nell&#39;organizzazione sono presenti più di cinque criteri di unione per [!DNL XDM Individual Profile] in un singolo ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

### Creare una pianificazione

Effettuando una richiesta POST all&#39;endpoint `/config/schedules`, è possibile creare una pianificazione e includere l&#39;ora specifica in cui attivare la pianificazione.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella [guida degli endpoint di pianificazione](../api/schedules.md#create)

### Abilitare una pianificazione

Per impostazione predefinita, una pianificazione non è attiva al momento della creazione, a meno che la proprietà `state` non sia impostata su `active` nel corpo della richiesta di creazione (POST). È possibile abilitare una pianificazione (impostare `state` su `active`) effettuando una richiesta PATCH all&#39;endpoint `/config/schedules` e includendo l&#39;ID della pianificazione nel percorso.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella [guida degli endpoint di pianificazione](../api/schedules.md#update-state)

### Aggiornare l’ora di pianificazione

È possibile aggiornare la tempistica della pianificazione effettuando una richiesta PATCH all&#39;endpoint `/config/schedules` e includendo l&#39;ID della pianificazione nel percorso.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella [guida degli endpoint di pianificazione](../api/schedules.md#update-schedule)

## Valutazione a richiesta

La valutazione on-demand consente di creare un processo di segmentazione per generare un pubblico ogni volta che necessario. A differenza della valutazione pianificata, questa si verifica solo quando richiesto e non è ricorrente.

### Creare un processo di segmentazione

Un processo di segmentazione è un processo asincrono che crea un segmento di pubblico su richiesta. Fa riferimento a una definizione di segmento, nonché a eventuali criteri di unione che controllano il modo in cui [!DNL Real-Time Customer Profile] unisce attributi sovrapposti tra i frammenti di profilo. Al termine di un processo di segmentazione, puoi raccogliere varie informazioni sulla definizione del segmento, ad esempio eventuali errori che si sono verificati durante l’elaborazione e le dimensioni finali del pubblico. È necessario eseguire un processo di segmentazione ogni volta che desideri aggiornare il pubblico attualmente qualificato dalla definizione del segmento.

È possibile creare un nuovo processo di segmentazione effettuando una richiesta POST all&#39;endpoint `/segment/jobs` nell&#39;API [!DNL Real-Time Customer Profile].

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella guida dell&#39;endpoint [segment jobs](../api/segment-jobs.md#create)

### Cercare lo stato del processo di segmento

È possibile utilizzare `id` per un processo di segmento specifico per eseguire una richiesta di ricerca (GET) per visualizzare lo stato corrente del processo.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella guida dell&#39;endpoint [segment jobs](../api/segment-jobs.md#get)

## Interpretare i risultati del processo segmento

Quando i processi di segmentazione vengono eseguiti correttamente, la mappa `segmentMembership` viene aggiornata per ogni profilo incluso nella definizione del segmento. `segmentMembership` memorizza anche eventuali tipi di pubblico pre-valutati che vengono acquisiti in [!DNL Platform], consentendo l&#39;integrazione con altre soluzioni come [!DNL Adobe Audience Manager].

Nell&#39;esempio seguente viene illustrato l&#39;aspetto dell&#39;attributo `segmentMembership` per ogni singolo record di profilo:

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
| `lastQualificationTime` | Il timestamp in cui è stata effettuata l’asserzione di appartenenza al segmento e il profilo è entrato o uscito dalla definizione del segmento. |
| `status` | Lo stato di partecipazione della definizione del segmento come parte della richiesta corrente. Deve essere uguale a uno dei seguenti valori noti: <ul><li>`realized`: l&#39;entità è idonea per la definizione del segmento.</li><li>`exited`: l&#39;entità sta uscendo dalla definizione del segmento.</li></ul> |

>[!NOTE]
>
>Qualsiasi appartenenza a un segmento con stato `exited` per più di 30 giorni, in base a `lastQualificationTime`, sarà soggetta a eliminazione.

## Accedere ai risultati del processo di segmentazione

È possibile accedere ai risultati di un processo di segmentazione in uno dei due modi seguenti: accedere a singoli profili o esportare un intero pubblico in un set di dati.

Le sezioni seguenti descrivono queste opzioni in modo più dettagliato.

## Cercare un profilo

Se si conosce il profilo specifico a cui si desidera accedere, è possibile utilizzare l&#39;API [!DNL Real-Time Customer Profile]. I passaggi completi per l&#39;accesso ai singoli profili sono disponibili nell&#39;esercitazione [Accedere ai dati del profilo cliente in tempo reale utilizzando l&#39;API profilo](../../profile/api/entities.md).

## Esportare un segmento {#export}

Dopo il completamento di un processo di segmentazione (il valore dell&#39;attributo `status` è &quot;RIUSCITO&quot;), è possibile esportare il pubblico in un set di dati in cui è possibile accedervi e agire di conseguenza.

Per esportare il pubblico, sono necessari i seguenti passaggi:

- [Crea un set di dati di destinazione](#create-a-target-dataset) - Crea il set di dati per contenere i membri del pubblico.
- [Genera profili di pubblico nel set di dati](#generate-profiles) - Popola il set di dati con profili individuali XDM in base ai risultati di un processo di segmentazione.
- [Monitorare l&#39;avanzamento dell&#39;esportazione](#monitor-export-progress) - Controllare l&#39;avanzamento corrente del processo di esportazione.
- [Leggi dati pubblico](#next-steps) - Recupera i profili individuali XDM risultanti che rappresentano i membri del pubblico.

### Creare un set di dati di destinazione {#create-dataset}

Durante l’esportazione di un pubblico, è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire l’esportazione in modo corretto.

Una delle considerazioni chiave è lo schema su cui si basa il set di dati (`schemaRef.id` nella richiesta di esempio API seguente). Per esportare una definizione di segmento, il set di dati deve essere basato su [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema di unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe, in questo caso la classe XDM Individual Profile. Per ulteriori informazioni sugli schemi di visualizzazione unione, consulta la sezione [Profilo cliente in tempo reale della Guida per gli sviluppatori del registro degli schemi](../../xdm/api/getting-started.md).

Esistono due modi per creare il set di dati necessario:

- **Utilizzo delle API:** I passaggi descritti in questo tutorial descrivono come creare un set di dati che faccia riferimento a [!DNL XDM Individual Profile Union Schema] utilizzando l&#39;API [!DNL Catalog].
- **Utilizzo dell&#39;interfaccia utente:** Per utilizzare l&#39;interfaccia utente [!DNL Adobe Experience Platform] per creare un set di dati che fa riferimento allo schema di unione, seguire i passaggi descritti nell&#39;[esercitazione dell&#39;interfaccia utente](../ui/overview.md), quindi tornare a questa esercitazione per continuare con i passaggi per la [generazione dei profili di pubblico](#generate-profiles).

Se disponi già di un set di dati compatibile e conosci il relativo ID, puoi procedere direttamente al passaggio per [generare profili di pubblico](#generate-profiles).

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

Dopo aver creato un set di dati persistente nell&#39;unione, puoi creare un processo di esportazione per rendere persistenti i membri del pubblico nel set di dati effettuando una richiesta POST all&#39;endpoint `/export/jobs` nell&#39;API [!DNL Real-Time Customer Profile] e fornendo l&#39;ID del set di dati e le informazioni di definizione del segmento per le definizioni dei segmenti che desideri esportare.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella [guida dell&#39;endpoint dei processi di esportazione](../api/export-jobs.md#create)

### Monitorare l’avanzamento dell’esportazione

Durante l&#39;elaborazione di un processo di esportazione, è possibile monitorarne lo stato effettuando una richiesta di GET all&#39;endpoint `/export/jobs` e includendo `id` del processo di esportazione nel percorso. Il processo di esportazione viene completato quando il campo `status` restituisce il valore &quot;SUCCESSEDED&quot;.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella [guida dell&#39;endpoint dei processi di esportazione](../api/export-jobs.md#get)

## Passaggi successivi

Una volta completata l&#39;esportazione, i dati saranno disponibili in [!DNL Data Lake] in [!DNL Experience Platform]. È quindi possibile utilizzare [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) per accedere ai dati utilizzando `batchId` associato all&#39;esportazione. A seconda delle dimensioni della definizione del segmento, i dati possono essere in blocchi e il batch può essere costituito da diversi file.

Per istruzioni dettagliate sull&#39;utilizzo dell&#39;API [!DNL Data Access] per accedere e scaricare i file batch, seguire l&#39;[esercitazione sull&#39;accesso ai dati](../../data-access/tutorials/dataset-data.md).

È inoltre possibile accedere ai dati di definizione del segmento esportati correttamente utilizzando [!DNL Adobe Experience Platform Query Service]. Utilizzando l&#39;interfaccia utente o l&#39;API RESTful, [!DNL Query Service] consente di scrivere, convalidare ed eseguire query sui dati in [!DNL Data Lake].

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la documentazione su [[!DNL Query Service]](../../query-service/home.md).
