---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy nel Data Lake

 Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i loro dati personali come delineato dalle normative sulla privacy legali e organizzative.

Questo documento tratta i concetti essenziali relativi all&#39;elaborazione delle richieste di privacy per i dati dei clienti memorizzati nel Data Lake.

## Introduzione

Prima di leggere questa guida, è consigliabile avere una conoscenza approfondita dei seguenti servizi  Experience Platform:

* [Privacy Service](../privacy-service/home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [Servizio](home.md)catalogo: Il sistema di record per la posizione dei dati e la linea di dati all&#39;interno  Experience Platform. Fornisce un&#39;API che può essere utilizzata per aggiornare i metadati del set di dati.
* [Sistema](../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
* [Servizio](../identity-service/home.md)identità: Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

 Adobe Experience Platform Identity Service collega i dati di identità dei clienti tra sistemi e dispositivi. Identity Service utilizza gli spazi dei nomi **di identità** per fornire contesto ai valori di identità collegandoli al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe  Advertising Cloud ID (&quot;AdCloud&quot;) o un  Adobe Target ID (&quot;TNTID&quot;).

Servizio identità mantiene un archivio di spazi dei nomi di identità globali (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi di identità in  Experience Platform, consultate la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)identità.

## Aggiunta di dati di identità ai set di dati

Durante la creazione di richieste di privacy per il Data Lake, è necessario fornire valori di identità validi (e relativi spazi di nomi associati) a ciascun singolo cliente al fine di individuare i propri dati ed elaborarli di conseguenza. Pertanto, tutti i set di dati soggetti a richieste di privacy devono contenere un descrittore **di** identità nello schema XDM associato.

>[!NOTE]
>
>Eventuali set di dati basati su schemi che non supportano i metadati del descrittore di identità (ad esempio, set di dati ad hoc) non possono attualmente essere elaborati nelle richieste di privacy.

Questa sezione descrive i passaggi necessari per aggiungere un descrittore di identità allo schema XDM di un set di dati esistente. Se disponete già di un set di dati con un descrittore di identità, potete passare alla sezione [](#nested-maps)successiva.

>[!IMPORTANT]
>
>Per decidere quali campi dello schema impostare come identità, tenere presente i [limiti dell&#39;utilizzo di campi](#nested-maps)di tipo mappa nidificati.

Esistono due metodi per aggiungere un descrittore di identità a uno schema di set di dati:

* [Utilizzo dell’interfaccia](#identity-ui)
* [Utilizzo dell&#39;API](#identity-api)

### Utilizzo dell’interfaccia {#identity-ui}

Nell’interfaccia utente di  Experience Platform, l’ _[!UICONTROL Schemas]_area di lavoro consente di modificare gli schemi XDM esistenti. Per aggiungere un descrittore di identità a uno schema, selezionare lo schema dall&#39;elenco e seguire i passaggi per[impostare un campo di schema come campo](../xdm/tutorials/create-schema-ui.md#identity-field)di identità nell&#39;esercitazione Editor di schema.

Dopo aver impostato i campi appropriati nello schema come campi di identità, è possibile passare alla sezione successiva per l&#39; [invio delle richieste](#submit)di privacy.

### Utilizzo dell&#39;API {#identity-api}

>[!NOTE]
>
>Questa sezione presuppone che si conosca il valore ID URI univoco dello schema XDM del set di dati. Se non conosci questo valore, puoi recuperarlo utilizzando l&#39;API Catalog Service. Dopo aver letto la sezione [introduttiva](./api/getting-started.md) della guida per gli sviluppatori, segui i passaggi descritti in per [elencare](./api/list-objects.md) o [cercare](./api/look-up-object.md) gli oggetti del catalogo per trovare il set di dati. L&#39;ID dello schema si trova in `schemaRef.id`
>
> Questa sezione include le chiamate all&#39;API del Registro di sistema dello schema. Per informazioni importanti sull’utilizzo dell’API, inclusa la conoscenza `{TENANT_ID}` e il concetto di contenitori, consultate la sezione [introduttiva](../xdm/api/getting-started.md) della guida per gli sviluppatori.

È possibile aggiungere un descrittore di identità allo schema XDM di un dataset effettuando una richiesta POST all&#39; `/descriptors` endpoint nell&#39;API del Registro di sistema dello schema.

**Formato API**

```http
POST /descriptors
```

**Richiesta**

La richiesta seguente definisce un descrittore di identità in un campo &quot;indirizzo e-mail&quot; in uno schema di esempio.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Il tipo di descrittore da creare. Per i descrittori di identità, il valore deve essere &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | ID URI univoco dello schema XDM del set di dati. |
| `xdm:sourceVersion` | La versione dello schema XDM specificata in `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Percorso del campo dello schema a cui viene applicato il descrittore. |
| `xdm:namespace` | Uno degli spazi dei nomi delle identità [standard riconosciuti](../privacy-service/api/appendix.md#standard-namespaces) da Privacy Service o uno spazio dei nomi personalizzato definito dall&#39;organizzazione. |
| `xdm:property` | &quot;xdm:id&quot; o &quot;xdm:code&quot;, a seconda dello spazio dei nomi utilizzato in `xdm:namespace`. |
| `xdm:isPrimary` | Un valore booleano facoltativo. Se true, indica che il campo è un&#39;identità primaria. Gli schemi possono contenere una sola identità primaria. Il valore predefinito è false se non è incluso. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Invio di richieste {#submit}

>[!NOTE]
>
>Questa sezione descrive come formattare le richieste di privacy per il Data Lake. È vivamente consigliato di consultare la documentazione [Privacy Service UI](../privacy-service/ui/overview.md) o API [](../privacy-service/api/getting-started.md) Privacy Service per i passaggi completi su come inviare un processo per la privacy, incluso come formattare correttamente i dati di identità dell&#39;utente inviati nei payload di richiesta.

La sezione seguente illustra come effettuare richieste di privacy per il Data Lake utilizzando l&#39;interfaccia utente o l&#39;API di Privacy Service.

### Utilizzo dell’interfaccia

Durante la creazione di richieste di lavoro nell’interfaccia utente, accertatevi di selezionare **AEP Data Lake** e/o **Profile** in _Products_ , rispettivamente, per elaborare i processi per i dati memorizzati nel Data Lake o nel Real-time Customer Profile.

<img src="images/privacy/product-value.png" width="450"><br>

### Utilizzo dell&#39;API

Quando si creano richieste di processo nell&#39;API, tutte le `userIDs` richieste fornite devono utilizzare un archivio dati specifico `namespace` e `type` a seconda dell&#39;archivio dati a cui si riferiscono. Gli ID per il Data Lake devono utilizzare &quot;non registrato&quot; per il loro `type` valore e un `namespace` valore che corrisponda a una delle etichette [di](#privacy-labels) privacy aggiunte ai set di dati applicabili.

Inoltre, l&#39; `include` array del payload della richiesta deve includere i valori prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste al Data Lake, l&#39;array deve includere il valore &quot;aepDataLake&quot;.

La richiesta seguente crea un nuovo processo di privacy per il Data Lake, utilizzando lo spazio dei nomi &quot;email_label&quot; non registrato. Include inoltre il valore prodotto per il Data Lake nell&#39; `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## Elimina elaborazione richiesta

Quando  Experience Platform riceve una richiesta di eliminazione da Privacy Service, Platform invia ad Privacy Service la conferma che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dal Data Lake entro sette giorni. Durante la finestra di sette giorni, i dati vengono eliminati in modo morbido e pertanto non sono accessibili da alcun servizio Platform.

Nelle release future, Platform invierà una conferma ad Privacy Service dopo che i dati saranno stati fisicamente eliminati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all&#39;elaborazione delle richieste di privacy per il Data Lake. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Consulta il documento sull’elaborazione delle richieste di [privacy per il profilo](../profile/privacy.md) cliente in tempo reale per i passaggi relativi all’elaborazione delle richieste di privacy per l’archivio profili.

## Appendice

La sezione seguente contiene informazioni aggiuntive per l&#39;elaborazione delle richieste di privacy nel Data Lake.

### Etichettare i campi del tipo di mappa nidificati {#nested-maps}

È importante notare che esistono due tipi di campi di tipo mappa nidificati che non supportano l&#39;etichettatura della privacy:

* Campo di tipo mapping all&#39;interno di un campo di tipo matrice
* Campo di tipo mappa all’interno di un altro campo di tipo mappa

L&#39;elaborazione del lavoro sulla privacy per uno dei due esempi di cui sopra avrà un esito negativo. Per questo motivo, si consiglia di evitare di utilizzare campi di tipo mappa nidificati per memorizzare i dati privati dei clienti. Gli ID del consumatore pertinenti devono essere memorizzati come tipo di dati non mappato all&#39;interno del `identityMap` campo (stesso campo del tipo di mappa) per i set di dati basati su record, oppure come `endUserID` campo per i set di dati basati su serie temporali.