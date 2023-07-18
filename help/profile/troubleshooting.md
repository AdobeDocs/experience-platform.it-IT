---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida alla risoluzione dei problemi dei profili cliente in tempo reale
type: Documentation
description: Questo documento fornisce le risposte alle domande più frequenti su Real-Time Customer Profile, nonché una guida alla risoluzione dei problemi relativi agli errori più comuni durante l’utilizzo dei dati del profilo con Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di Real-Time Customer Profile

Questo documento fornisce le risposte alle domande più frequenti su Real-Time Customer Profile, nonché una guida alla risoluzione dei problemi relativi agli errori più comuni. Per domande e risoluzione dei problemi relativi ad altri servizi in Adobe Experience Platform, consulta [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Con [!DNL Real-Time Customer Profile], puoi avere una visione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Questo consente agli addetti al marketing di distribuire esperienze coordinate, coerenti e rilevanti per i clienti su più canali.

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti su Real-Time Customer Profile.

### Quali tipi di dati sono accettati per Real-Time Customer Profile?

Il profilo accetta entrambi **record** e **serie temporali** dati, purché i dati in questione contengano almeno un valore di identità che associa i dati a una singola persona univoca.

Come tutti i servizi di Platform, il profilo richiede che i suoi dati siano strutturati semanticamente in uno schema Experience Data Model (XDM). A sua volta, questo schema deve avere **identità primaria** ed essere abilitati per l’utilizzo nel profilo.

Se non conosci XDM, inizia con [Panoramica di XDM](../xdm/home.md) per ulteriori informazioni. Quindi, consulta la guida utente di XDM per i passaggi su come [imposta campi di identità](../xdm/tutorials/create-schema-ui.md#identity-field) e [abilitare uno schema per il profilo](../xdm/tutorials/create-schema-ui.md#profile).

### Dove vengono memorizzati i dati del profilo?

Real-Time Customer Profile mantiene il proprio archivio dati (denominato &quot;archivio profili&quot;), separato dal Data Lake che contiene altri dati di Platform acquisiti.

### Se ho già acquisito i dati in Platform, posso renderli disponibili nell’archivio Profili?

Se i dati sono stati acquisiti in un set di dati non di profilo, devi acquisirli nuovamente in un set di dati abilitato per il profilo per renderli disponibili nell’archivio Profili. È possibile abilitare un set di dati esistente per il profilo, tuttavia tutti i dati acquisiti prima di tale configurazione non verranno ancora visualizzati nell’archivio dei profili.

Se desideri aggiungere dati precedentemente acquisiti all’archivio Profili, segui la [tutorial sulla configurazione dei set di dati](./tutorials/dataset-configuration.md) per creare un nuovo set di dati o convertire un set di dati esistente da abilitare per Profilo, quindi acquisire nuovamente i dati desiderati in tale set di dati.

### Come posso visualizzare i dati del profilo acquisiti?

Esistono diversi metodi per visualizzare i dati del profilo, a seconda che si utilizzi l’API o l’interfaccia utente.

#### Mediante l’API

Se conosci gli ID delle entità profilo a cui desideri accedere, puoi utilizzare `/entities` (Accesso profilo) nell’API del profilo per cercare tali entità. Consulta la sezione su [entità](./api/entities.md) per ulteriori informazioni, consulta la guida per gli sviluppatori.

Puoi anche utilizzare l’API del servizio di segmentazione di Adobe Experience Platform per accedere ai singoli profili dei clienti idonei per l’iscrizione a un pubblico. Consulta la [Panoramica del servizio di segmentazione](../segmentation/home.md) per ulteriori informazioni.

#### Utilizzo dell’interfaccia utente

Nell’interfaccia utente di Experience Platform, il **[!UICONTROL Sfoglia]** scheda in **[!UICONTROL Profili]** workspace consente di visualizzare il conteggio totale dei profili e di cercare i singoli profili in base al loro valore di identità. Consulta la [Guida utente del profilo](./ui/user-guide.md) per ulteriori informazioni.

Puoi anche visualizzare un elenco dei tipi di pubblico sotto **[!UICONTROL Sfoglia]** scheda in **[!UICONTROL Tipi di pubblico]** Workspace. Dopo aver selezionato un pubblico, viene visualizzato un campione di profili idonei per quel pubblico. Puoi quindi selezionare uno di questi profili elencati per visualizzarne i dettagli. Consulta la [Panoramica sulla segmentazione dell’interfaccia utente](../segmentation/ui/overview.md) per ulteriori informazioni.

## Codici di errore

Di seguito è riportato un elenco di messaggi di errore che possono verificarsi quando si lavora con l’API Profilo cliente in tempo reale. Se l’errore che stai riscontrando non è elencato qui, puoi trovarlo nella sezione generale [Guida alla risoluzione dei problemi di Platform](../landing/troubleshooting.md) invece.

### Impossibile cercare lo schema dell’attributo calcolato per il percorso specificato

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Durante la creazione di un nuovo attributo calcolato, questo errore si verifica quando il sistema non è riuscito a trovare lo schema fornito nel payload della richiesta. Assicurati di aver fornito l’ID tenant corretto nel file `path` e che i valori di `schema.name` è un nome di schema valido.

Se non conosci il tuo ID tenant, puoi recuperarlo seguendo i passaggi descritti in [Guida per gli sviluppatori del registro dello schema](../xdm/api/getting-started.md).

### Esiste già una funzione con lo stesso nome per lo schema specificato o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando l’ `name` è già in uso per lo schema indicato in `schema.name`. Sostituisci il valore con un nome univoco prima di riprovare.

### Lo schema di ritorno dell’espressione non è lo stesso dello schema dell’attributo calcolato nello schema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando l’ `name` è già in uso per lo schema indicato in `schema.name`. Sostituisci il valore con un nome univoco prima di riprovare.

### Richiesta di eliminazione non valida (processo di sistema del profilo)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Questo errore si verifica quando viene fornito un payload non valido per un processo di eliminazione del sistema. Assicurati di fornire un set di dati o un ID batch valido sotto il `dataSetID` o `batchID` proprietà. Consulta la sezione su [creazione di una richiesta di eliminazione](./api/profile-system-jobs.md#create-a-delete-request) Per ulteriori informazioni, consulta la guida per gli sviluppatori di profili.

### Batch non trovato per il set di dati profilo

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

Questo errore si verifica quando non è possibile trovare un batch valido durante il tentativo di creare una richiesta di eliminazione per i dati del profilo. Prima di riprovare, verifica di aver immesso l’ID corretto per un set di dati abilitato per il profilo.

### La destinazione della proiezione non è ancora stata creata

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Questo errore si verifica quando `destinationId` fornito in un `POST /config/projections` richiesta non valida. Prima di riprovare, verifica di aver fornito un ID di destinazione valido. Per creare una nuova destinazione, segui i passaggi descritti in [Guida per gli sviluppatori di profili](./api/edge-projections.md#create-a-destination).

### Tipo di file multimediale non supportato

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Questo errore si verifica quando si invia una richiesta POST o PUT con un’intestazione Content-Type non valida. Verifica di fornire un valore Content-Type valido per l’endpoint in uso.

La maggior parte degli endpoint di profilo accetta &quot;application/json&quot; per l’intestazione Content-Type, con le seguenti eccezioni:

| Endpoint | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
