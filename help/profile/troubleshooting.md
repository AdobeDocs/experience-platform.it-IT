---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida alla risoluzione dei problemi dei profili cliente in tempo reale
type: Documentation
description: Questo documento fornisce le risposte alle domande frequenti sul Profilo cliente in tempo reale e una guida alla risoluzione dei problemi relativi agli errori comuni durante l’utilizzo dei dati del profilo con Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi del profilo cliente in tempo reale

Questo documento fornisce le risposte alle domande più frequenti sul Profilo del cliente in tempo reale, nonché una guida alla risoluzione dei problemi per gli errori comuni. Per domande e risoluzione dei problemi relativi ad altri servizi in Adobe Experience Platform, fai riferimento alla [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Con [!DNL Real-Time Customer Profile], puoi visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Questo consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e rilevanti per i clienti su più canali.

## Domande frequenti

Di seguito è riportato un elenco delle risposte alle domande più frequenti sul Profilo del cliente in tempo reale.

### Quali tipi di dati sono accettati per il Profilo cliente in tempo reale?

Il profilo accetta entrambe **record** e **serie temporale** purché i dati in questione contengano almeno un valore di identità che associa i dati a una singola persona univoca.

Come tutti i servizi Platform, Profile richiede che i suoi dati siano strutturati semanticamente in uno schema Experience Data Model (XDM). A sua volta, questo schema deve avere un **identità principale** è stato definito e deve essere abilitato per l’utilizzo in Profilo.

Se non conosci XDM, inizia con [Panoramica di XDM](../xdm/home.md) per saperne di più. Quindi, consulta la guida utente di XDM per i passaggi su come [imposta campi di identità](../xdm/tutorials/create-schema-ui.md#identity-field) e [abilitare uno schema per il profilo](../xdm/tutorials/create-schema-ui.md#profile).

### Dove sono memorizzati i dati del profilo?

Profilo cliente in tempo reale mantiene il proprio archivio dati (denominato &quot;archivio profili&quot;), separato dal Data Lake che contiene altri dati della piattaforma acquisiti.

### Se ho già acquisito dati in Platform, posso renderli disponibili nell’archivio profili?

Se i dati sono stati acquisiti in un set di dati non di profilo, devi riacquisire tali dati in un set di dati abilitato per il profilo per renderli disponibili nell’archivio profili. È possibile abilitare un set di dati esistente per il profilo, tuttavia tutti i dati acquisiti prima di tale configurazione non verranno ancora visualizzati nell’archivio profili.

Se desideri aggiungere dati precedentemente acquisiti all’archivio profili, segui la [esercitazione sulla configurazione del set di dati](./tutorials/dataset-configuration.md) per creare un nuovo set di dati o convertire un set di dati esistente da abilitare per il profilo, quindi riacquisire i dati desiderati in tale set di dati.

### Come posso visualizzare i dati del profilo acquisito?

Esistono diversi metodi per visualizzare i dati del profilo, a seconda che tu utilizzi l’API o l’interfaccia utente.

#### Mediante l’API

Se conosci gli ID delle entità profilo a cui desideri accedere, puoi utilizzare la funzione `/entities` (Accesso profilo) endpoint nell’API del profilo per cercare tali entità. Vedi la sezione su [entità](./api/entities.md) nella guida per gli sviluppatori per ulteriori informazioni.

Puoi inoltre utilizzare l’API del servizio di segmentazione di Adobe Experience Platform per accedere ai singoli profili dei clienti idonei per un’iscrizione a un segmento. Consulta la sezione [Panoramica del servizio di segmentazione](../segmentation/home.md) per ulteriori informazioni.

#### Utilizzo dell’interfaccia

Nell’interfaccia utente di Experience Platform, la funzione **[!UICONTROL Sfoglia]** nella scheda **[!UICONTROL Profili]** workspace consente di visualizzare il conteggio totale dei profili e di cercare singoli profili in base al loro valore di identità. Consulta la sezione [Guida utente profilo](./ui/user-guide.md) per ulteriori informazioni.

Puoi anche visualizzare un elenco dei segmenti nella sezione **[!UICONTROL Sfoglia]** nella scheda **[!UICONTROL Segmenti]** workspace. Dopo aver selezionato un segmento, viene visualizzato un esempio di profili qualificati per quel segmento. Puoi quindi selezionare uno qualsiasi di questi profili elencati per visualizzarne i dettagli. Consulta la sezione [Panoramica dell’interfaccia utente di segmentazione](../segmentation/ui/overview.md) per ulteriori informazioni.

## Codici di errore

Di seguito è riportato un elenco di messaggi di errore che potresti incontrare quando lavori con l’API del profilo cliente in tempo reale. Se l&#39;errore che si verifica non è presente in questa pagina, è possibile trovarlo in generale [Guida alla risoluzione dei problemi di Platform](../landing/troubleshooting.md) invece.

### Impossibile cercare lo schema dell&#39;attributo calcolato per il percorso fornito

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Durante la creazione di un nuovo attributo calcolato, questo errore si verifica quando il sistema non è riuscito a trovare lo schema fornito nel payload della richiesta. Verifica di aver fornito l’ID tenant corretto nel payload `path` e che i valori di `schema.name` è un nome di schema valido.

Se non conosci il tuo ID tenant, puoi recuperarlo seguendo i passaggi descritti nella sezione [Guida per gli sviluppatori del Registro di sistema dello schema](../xdm/api/getting-started.md).

### La funzione con lo stesso nome esiste già per lo schema specificato o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando il `name` proprietà già utilizzata per lo schema indicato in `schema.name`. Sostituisci il valore con un nome univoco prima di riprovare.

### Lo schema restituito dell&#39;espressione non è lo schema dell&#39;attributo calcolato nello schema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Quando si crea un nuovo attributo calcolato, questo errore si verifica quando il `name` proprietà già utilizzata per lo schema indicato in `schema.name`. Sostituisci il valore con un nome univoco prima di riprovare.

### Richiesta di eliminazione non valida (processo di sistema del profilo)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Questo errore si verifica quando viene fornito un payload non valido per un processo di eliminazione del sistema. Assicurati di fornire un set di dati o un ID batch valido sotto il payload `dataSetID` o `batchID` proprietà, rispettivamente. Vedi la sezione su [creazione di una richiesta di cancellazione](./api/profile-system-jobs.md#create-a-delete-request) per ulteriori informazioni, consulta la guida per gli sviluppatori di profili .

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

Questo errore si verifica quando non è stato possibile trovare un batch valido durante il tentativo di creare una richiesta di cancellazione per i dati del profilo. Prima di riprovare, verifica di aver immesso l’ID corretto per un set di dati abilitato per il profilo.

### La destinazione di proiezione non è ancora stata creata

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Questo errore si verifica quando `destinationId` a `POST /config/projections` richiesta non valida. Prima di riprovare, verifica di aver fornito un ID di destinazione valido. Per creare una nuova destinazione, segui i passaggi descritti nel [Guida per gli sviluppatori di profili](./api/edge-projections.md#create-a-destination).

### Tipo di supporto non supportato

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Questo errore si verifica quando si invia una richiesta POST o PUT con un&#39;intestazione Content-Type non valida. Verificare di aver fornito un valore Content-Type valido per l&#39;endpoint utilizzato.

La maggior parte degli endpoint profilo accetta &quot;application/json&quot; per la loro intestazione Content-Type, con le seguenti eccezioni:

| Endpoint | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
