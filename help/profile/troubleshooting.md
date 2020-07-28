---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida alla risoluzione dei problemi in tempo reale sul profilo cliente
topic: guide
translation-type: tm+mt
source-git-commit: 94fd6ee324b35acb7ef1185f7851d76d76f3e91c
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi in tempo reale sul profilo cliente

Questo documento contiene le risposte alle domande frequenti sul profilo cliente in tempo reale e una guida alla risoluzione dei problemi per individuare gli errori più comuni. Per domande e risoluzione dei problemi relativi ad altri servizi nel  Adobe Experience Platform, consultare la guida [alla risoluzione dei problemi del](../landing/troubleshooting.md)Experience Platform.

Profilo cliente in tempo reale è un archivio di entità di ricerca generico che unisce i dati da varie risorse di dati aziendali e fornisce l&#39;accesso a tali dati sotto forma di profili cliente individuali ed eventi serie temporali correlati. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali.

## Domande frequenti

Segue un elenco di risposte alle domande frequenti sul profilo cliente in tempo reale.

### Quali tipi di dati vengono accettati per il profilo cliente in tempo reale?

Il profilo accetta sia i dati **record** che quelli delle serie **** temporali, purché i dati in questione contengano almeno un valore di identità che associa i dati a una singola persona univoca.

Come tutti i servizi Platform, Profile richiede che i suoi dati siano strutturati in modo semantico in uno schema Experience Data Model (XDM). A sua volta, questo schema deve avere un&#39;identità **** primaria definita ed essere abilitato per l&#39;uso in Profile.

Se non avete familiarità con XDM, iniziate con la panoramica [](../xdm/home.md) XDM per ulteriori informazioni. Quindi, vedere la guida utente XDM per i passaggi su come [impostare i campi](../xdm/tutorials/create-schema-ui.md#identity-field) di identità e [abilitare uno schema per il profilo](../xdm/tutorials/create-schema-ui.md#profile).

### Dove sono memorizzati i dati del profilo?

Il profilo cliente in tempo reale mantiene il proprio archivio dati (denominato &quot;Profile Store&quot;), separato dal Data Lake che contiene altri dati Platform acquisiti.

### Se ho già acquisito dati in Platform, posso renderli disponibili nello store Profilo?

Se i dati sono stati inseriti in un set di dati non di profilo, è necessario riacquisirli in un set di dati abilitato per il profilo per renderlo disponibile nello store del profilo. È possibile abilitare un set di dati esistente per il profilo, tuttavia tutti i dati acquisiti prima di tale configurazione non verranno ancora visualizzati nello store del profilo.

Se si desidera aggiungere dati precedentemente acquisiti allo store Profilo, seguire l&#39;esercitazione [di configurazione del](./tutorials/dataset-configuration.md) dataset per creare un nuovo set di dati o convertire un set di dati esistente da abilitare per il profilo, quindi ripetere l&#39;acquisizione dei dati desiderati in tale set di dati.

### Come posso visualizzare i miei dati del profilo assimilato?

Esistono diversi metodi per visualizzare i dati del profilo, a seconda che si utilizzi l&#39;API o l&#39;interfaccia utente.

#### Utilizzo dell&#39;API

Se conoscete gli ID delle entità profilo a cui desiderate accedere, potete utilizzare l&#39;endpoint `/entities` (accesso profilo) nell&#39;API del profilo per cercare tali entità. Per ulteriori informazioni, consulta la sezione [Entità](./api/entities.md) nella guida per gli sviluppatori.

Puoi anche utilizzare l&#39;API  Adobe Experience Platform Segmentation Service per accedere ai profili individuali dei clienti idonei per un&#39;iscrizione a un segmento. Per ulteriori informazioni, consulta la panoramica [del servizio di](../segmentation/home.md) segmentazione.

#### Utilizzo dell’interfaccia

Nell’interfaccia utente del Experience Platform , la **[!UICONTROL Browse]** scheda nell’area di lavoro **[!UICONTROL Profiles]** consente di visualizzare il conteggio totale dei profili e di cercare i singoli profili in base al relativo valore di identità. Per ulteriori informazioni, consulta la guida [utente](./ui/user-guide.md) Profilo.

Puoi anche visualizzare un elenco dei segmenti nella **[!UICONTROL Browse]** scheda dell’ **[!UICONTROL Segments]** area di lavoro. Dopo aver selezionato un segmento, viene visualizzato un esempio di profili idonei per tale segmento. Potete quindi selezionare uno di questi profili elencati per visualizzarne i dettagli. Per ulteriori informazioni, consulta la panoramica [dell’interfaccia utente di](../segmentation/ui/overview.md) segmentazione.

## Codici di errore

Di seguito è riportato un elenco di messaggi di errore che potrebbero verificarsi durante l&#39;utilizzo dell&#39;API Profilo cliente in tempo reale. Se l&#39;errore riscontrato non è elencato, è possibile che tale errore si trovi nella guida [generale alla risoluzione dei problemi di](../landing/troubleshooting.md) Platform.

### Impossibile cercare lo schema dell&#39;attributo calcolato per il percorso fornito

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando il sistema non riesce a trovare lo schema fornito nel payload della richiesta. Assicurarsi di aver fornito l&#39;ID tenant corretto nella `path` proprietà del payload e che i valori di `schema.name` è un nome di schema valido.

Se non si conosce l&#39;ID tenant, è possibile recuperarlo seguendo la procedura indicata nella guida [per gli sviluppatori del Registro di](../xdm/api/getting-started.md)schema.

### La funzione con lo stesso nome esiste già per lo schema specificato o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando la `name` proprietà fornita è già utilizzata per lo schema indicato in `schema.name`. Prima di riprovare, sostituite il valore con un nome univoco.

### Lo schema restituito dell&#39;espressione non è uguale allo schema dell&#39;attributo calcolato nello schema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando la `name` proprietà fornita è già utilizzata per lo schema indicato in `schema.name`. Prima di riprovare, sostituite il valore con un nome univoco.

### Richiesta di eliminazione non valida (processo del sistema del profilo)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Questo errore si verifica quando viene fornito un payload non valido per un processo di eliminazione del sistema. Assicurarsi di fornire un set di dati o un ID batch valido, rispettivamente, sotto la `dataSetID` proprietà o `batchID` proprietà del payload. Per ulteriori informazioni, consulta la sezione sulla [creazione di una richiesta](./api/profile-system-jobs.md#create-a-delete-request) di eliminazione nella guida per gli sviluppatori di profili.

### Batch non trovato per il set di dati del profilo

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Questo errore si verifica quando non è stato possibile trovare un batch valido quando si tentava di creare una richiesta di eliminazione per i dati del profilo. Prima di riprovare, verificate di aver immesso l’ID corretto per un set di dati abilitato per il profilo.

### La destinazione di proiezione non è ancora stata creata

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Questo errore si verifica quando il contenuto `destinationId` fornito in una `POST /config/projections` richiesta non è valido. Prima di riprovare, verificate di aver fornito un ID di destinazione valido. Per creare una nuova destinazione, segui i passaggi descritti nella guida [allo sviluppatore di](./api/edge-projections.md#create-a-destination)profili.

### Tipo di supporto non supportato

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Questo errore si verifica quando si invia una richiesta di POST o PUT con un&#39;intestazione Content-Type non valida. Verificate di fornire un valore Content-Type valido per l&#39;endpoint in uso.

La maggior parte degli endpoint profilo accetta &quot;application/json&quot; per la propria intestazione Content-Type, con le seguenti eccezioni:

| Endpoint | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |