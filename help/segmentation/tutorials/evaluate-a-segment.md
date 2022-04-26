---
keywords: Experience Platform;home;argomenti popolari;valutazione dei segmenti;servizio di segmentazione;segmentazione;segmentazione;valutazione di un segmento;risultati dei segmenti di accesso;valutazione e segmento di accesso;
solution: Experience Platform
title: Valutare e accedere ai risultati dei segmenti
topic-legacy: tutorial
type: Tutorial
description: Segui questa esercitazione per scoprire come valutare i segmenti e accedere ai risultati dei segmenti utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 9d82065fdf1be087023284f153f1abedb7fdb67b
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# Valutare e accedere ai risultati dei segmenti

Questo documento fornisce un&#39;esercitazione per valutare i segmenti e accedere ai risultati dei segmenti utilizzando [[!DNL Segmentation API]](../api/getting-started.md).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Consente di creare segmenti di pubblico da [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience. Per utilizzare al meglio la segmentazione, assicurati che i tuoi dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Intestazioni richieste

Questa esercitazione richiede anche di aver completato il [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate a [!DNL Platform] API. Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste di POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Valutare un segmento {#evaluate-a-segment}

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutarlo tramite una valutazione programmata o on demand.

[Valutazione programmata](#scheduled-evaluation) (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per l’esecuzione di un processo di esportazione in un momento specifico, mentre [valutazione a richiesta](#on-demand-evaluation) comporta la creazione di un lavoro di segmento per creare il pubblico immediatamente. I passaggi per ciascuno di essi sono descritti di seguito.

Se non hai ancora completato il [creare un segmento utilizzando l’API di segmentazione](./create-a-segment.md) creare un&#39;esercitazione o una definizione di segmento utilizzando [Generatore di segmenti](../ui/overview.md), effettua questa operazione prima di procedere con questa esercitazione.

## Valutazione programmata {#scheduled-evaluation}

Tramite la valutazione pianificata, l’organizzazione IMS può creare una pianificazione ricorrente per eseguire automaticamente i processi di esportazione.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se l&#39;organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] in un unico ambiente sandbox, non potrai utilizzare valutazioni pianificate.

### Creare una pianificazione

Effettuando una richiesta POST al `/config/schedules` endpoint, puoi creare una pianificazione e includere l’ora specifica in cui deve essere attivata la pianificazione.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida agli endpoint programmati](../api/schedules.md#create)

### Abilita pianificazione

Per impostazione predefinita, una pianificazione è inattiva quando viene creata a meno che il `state` è impostata su `active` nel corpo della richiesta create (POST). Puoi abilitare una pianificazione (imposta la `state` a `active`) effettuando una richiesta PATCH al `/config/schedules` e l’ID della pianificazione nel percorso.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida agli endpoint programmati](../api/schedules.md#update-state)

### Aggiornare l’ora di pianificazione

È possibile aggiornare la tempistica della pianificazione effettuando una richiesta di PATCH al `/config/schedules` e l’ID della pianificazione nel percorso.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida agli endpoint programmati](../api/schedules.md#update-schedule)

## Valutazione su richiesta

La valutazione su richiesta consente di creare un processo di segmento per generare un segmento di pubblico ogni volta che lo desideri. A differenza della valutazione pianificata, ciò si verifica solo quando richiesto e non è ricorrente.

### Creare un processo di segmento

Un processo di segmento è un processo asincrono che crea un segmento di pubblico su richiesta. Fa riferimento a una definizione di segmento, nonché a qualsiasi criterio di unione che controlla come [!DNL Real-time Customer Profile] unisce attributi sovrapposti nei frammenti di profilo. Quando un processo di segmento viene completato con successo, puoi raccogliere varie informazioni sul segmento, ad esempio eventuali errori verificatisi durante l’elaborazione e le dimensioni finali del pubblico. Un processo di segmento deve essere eseguito ogni volta che desideri aggiornare il pubblico attualmente idoneo per la definizione del segmento.

Puoi creare un nuovo processo di segmento effettuando una richiesta di POST al `/segment/jobs` punto finale [!DNL Real-time Customer Profile] API.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida all’endpoint dei processi di segmento](../api/segment-jobs.md#create)

### Cerca lo stato del processo del segmento

È possibile utilizzare `id` per eseguire una richiesta di ricerca (GET) per un processo di segmento specifico per visualizzare lo stato corrente del processo.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida all’endpoint dei processi di segmento](../api/segment-jobs.md#get)

## Interpretare i risultati dei segmenti

Quando i processi di segmento vengono eseguiti correttamente, la `segmentMembership` La mappa viene aggiornata per ogni profilo incluso all’interno del segmento. `segmentMembership` memorizza anche eventuali segmenti di pubblico valutati in precedenza acquisiti in [!DNL Platform], consentendo l&#39;integrazione con altre soluzioni come [!DNL Adobe Audience Manager].

L’esempio seguente mostra cosa `segmentMembership` l’attributo è simile a ciascun record di profilo individuale:

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
| `lastQualificationTime` | La marca temporale in cui è stata rilasciata l’asserzione dell’appartenenza al segmento e il profilo è entrato o uscito dal segmento. |
| `status` | Lo stato della partecipazione al segmento come parte della richiesta corrente. Deve essere uguale a uno dei seguenti valori noti: <ul><li>`existing`: L’entità continua a trovarsi nel segmento.</li><li>`realized`: L&#39;entità sta entrando nel segmento.</li><li>`exited`: L&#39;entità sta uscendo dal segmento.</li></ul> |

## Accedere ai risultati dei segmenti

È possibile accedere ai risultati di un processo di segmento in uno dei due modi seguenti: puoi accedere a singoli profili o esportare un intero pubblico in un set di dati.

Le sezioni seguenti descrivono più dettagliatamente queste opzioni.

## Cercare un profilo

Se conosci il profilo specifico a cui desideri accedere, puoi farlo utilizzando il [!DNL Real-time Customer Profile] API. I passaggi completi per accedere ai singoli profili sono disponibili nella sezione [Accedere ai dati del profilo cliente in tempo reale tramite l’API del profilo](../../profile/api/entities.md) esercitazione.

## Esportare un segmento {#export}

Dopo che un processo di segmentazione è stato completato correttamente (il valore di `status` attribute is &quot;SUCCEEDED&quot;), puoi esportare il pubblico in un set di dati a cui è possibile accedere e su cui agisce.

Per esportare il pubblico sono necessari i seguenti passaggi:

- [Creare un set di dati di destinazione](#create-a-target-dataset) - Crea il set di dati per i membri del pubblico.
- [Generare profili di pubblico nel set di dati](#generate-profiles) - Compilare il set di dati con i singoli profili XDM in base ai risultati di un processo di segmento.
- [Monitorare l’avanzamento dell’esportazione](#monitor-export-progress) - Controllare l&#39;avanzamento corrente del processo di esportazione.
- [Leggere i dati sul pubblico](#next-steps) - Recupera i singoli profili XDM risultanti che rappresentano i membri del pubblico.

### Creare un set di dati di destinazione {#create-dataset}

Quando si esporta un pubblico, è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire che l’esportazione abbia esito positivo.

Una delle considerazioni chiave è lo schema su cui si basa il set di dati (`schemaRef.id` nella richiesta di esempio API di seguito). Per esportare un segmento, il set di dati deve essere basato su [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema di unione è uno schema generato dal sistema e di sola lettura che aggrega i campi degli schemi che condividono la stessa classe, in questo caso si tratta della classe Profilo individuale XDM. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, consulta la sezione [Sezione Profilo cliente in tempo reale della guida per gli sviluppatori del registro dello schema](../../xdm/api/getting-started.md).

Esistono due modi per creare il set di dati necessario:

- **Utilizzo delle API:** I passaggi seguenti in questa esercitazione descrivono come creare un set di dati che fa riferimento a [!DNL XDM Individual Profile Union Schema] utilizzando [!DNL Catalog] API.
- **Utilizzo dell’interfaccia utente:** Per utilizzare [!DNL Adobe Experience Platform] per creare un set di dati che faccia riferimento allo schema di unione, segui i passaggi descritti in [Esercitazione sull’interfaccia utente](../ui/overview.md) quindi torna a questa esercitazione per procedere con i passaggi per [generazione di profili di pubblico](#generate-profiles).

Se disponi già di un set di dati compatibile e ne conosci l’ID, puoi procedere direttamente al passaggio per [generazione di profili di pubblico](#generate-profiles).

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La seguente richiesta crea un nuovo set di dati, fornendo parametri di configurazione nel payload.

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
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome descrittivo per il set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui sarà associato il set di dati. |

**Risposta**

Una risposta corretta restituisce un array contenente l’ID univoco generato dal sistema di sola lettura del set di dati appena creato. Per esportare correttamente i membri del pubblico è necessario un ID set di dati configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generare profili per i membri del pubblico {#generate-profiles}

Una volta che disponi di un set di dati persistente nell’unione, puoi creare un processo di esportazione per mantenere i membri del pubblico nel set di dati effettuando una richiesta di POST al gruppo di dati `/export/jobs` punto finale [!DNL Real-time Customer Profile] API e fornisce l’ID del set di dati e le informazioni sul segmento per i segmenti che desideri esportare.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida all’endpoint dei processi di esportazione](../api/export-jobs.md#create)

### Monitorare l’avanzamento dell’esportazione

Come processo di esportazione, puoi monitorarne lo stato effettuando una richiesta di GET al `/export/jobs` l&#39;endpoint e `id` del processo di esportazione nel percorso. Il processo di esportazione viene completato una volta che il `status` restituisce il valore &quot;SUCCEEDED&quot;.

Informazioni più dettagliate sull&#39;utilizzo di questo endpoint sono disponibili nella sezione [guida all’endpoint dei processi di esportazione](../api/export-jobs.md#get)

## Passaggi successivi

Una volta completata correttamente l’esportazione, i dati sono disponibili all’interno della [!DNL Data Lake] in [!DNL Experience Platform]. È quindi possibile utilizzare la [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) per accedere ai dati utilizzando `batchId` associato all’esportazione. A seconda delle dimensioni del segmento, i dati possono essere in blocchi e il batch può essere costituito da più file.

Per istruzioni dettagliate sull’utilizzo del [!DNL Data Access] API per accedere e scaricare file batch, segui la [Esercitazione sull&#39;accesso ai dati](../../data-access/tutorials/dataset-data.md).

Puoi anche accedere ai dati dei segmenti esportati correttamente utilizzando [!DNL Adobe Experience Platform Query Service]. Utilizzando l’interfaccia utente o l’API RESTful, [!DNL Query Service] consente di scrivere, convalidare ed eseguire query sui dati all&#39;interno di [!DNL Data Lake].

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la documentazione su [[!DNL Query Service]](../../query-service/home.md).
