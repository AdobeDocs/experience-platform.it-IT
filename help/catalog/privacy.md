---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy in [!DNL Data Lake]

 Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i loro dati personali come delineato dalle normative sulla privacy legali e organizzative.

Questo documento tratta i concetti essenziali relativi all&#39;elaborazione delle richieste di privacy per i dati dei clienti memorizzati in [!DNL Data Lake].

## Introduzione

Prima di leggere la presente guida è consigliabile conoscere i seguenti [!DNL Experience Platform] servizi:

* [!DNL Privacy Service](../privacy-service/home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [!DNL Catalog Service](home.md): Il sistema di record per la posizione dei dati e la linea [!DNL Experience Platform]. Fornisce un&#39;API che può essere utilizzata per aggiornare i metadati del set di dati.
* [!DNL Experience Data Model (XDM) System](../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
* [!DNL Identity Service](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

 Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza **[!UICONTROL identity namespaces]** per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un ID Adobe Advertising Cloud (&quot;AdCloud&quot;) o un ID Adobe Target  (&quot;TNTID&quot;).

[!DNL Identity Service] gestisce un archivio di spazi dei nomi di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)delle identità.

## Aggiunta di dati di identità ai set di dati

Durante la creazione di richieste di privacy per i [!DNL Data Lake]clienti, è necessario fornire valori di identità validi (e relativi spazi di nomi associati) per ciascun cliente al fine di individuare i propri dati ed elaborarli di conseguenza. Pertanto, tutti i set di dati soggetti a richieste di privacy devono contenere un elemento **[!UICONTROL identity descriptor]** nello schema XDM associato.

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

Nell&#39;interfaccia [!DNL Experience Platform ]utente, l&#39; _[!UICONTROL Schemas]_area di lavoro consente di modificare gli schemi XDM esistenti. Per aggiungere un descrittore di identità a uno schema, selezionare lo schema dall&#39;elenco e seguire i passaggi per[impostare un campo di schema come campo](../xdm/tutorials/create-schema-ui.md#identity-field)di identità nell&#39;[!DNL Schema Editor]esercitazione.

Dopo aver impostato i campi appropriati nello schema come campi di identità, è possibile passare alla sezione successiva per l&#39; [invio delle richieste](#submit)di privacy.

### Utilizzo dell&#39;API {#identity-api}

>[!NOTE]
>
>Questa sezione presuppone che si conosca il valore ID URI univoco dello schema XDM del set di dati. Se non conosci questo valore, puoi recuperarlo utilizzando l&#39; [!DNL Catalog Service] API. Dopo aver letto la sezione [introduttiva](./api/getting-started.md) della guida per gli sviluppatori, segui i passaggi descritti in per [elencare](./api/list-objects.md) o [cercare](./api/look-up-object.md) [!DNL Catalog] gli oggetti per trovare il set di dati. L&#39;ID dello schema si trova in `schemaRef.id`
>
> Questa sezione include le chiamate all&#39;API del Registro di sistema dello schema. Per informazioni importanti sull’utilizzo dell’API, inclusa la conoscenza `{TENANT_ID}` e il concetto di contenitori, consultate la sezione [introduttiva](../xdm/api/getting-started.md) della guida per gli sviluppatori.

È possibile aggiungere un descrittore di identità allo schema XDM di un dataset effettuando una richiesta di POST all&#39; `/descriptors` endpoint nell&#39; [!DNL Schema Registry] API.

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
| `xdm:namespace` | Uno dei namespace di identità [standard riconosciuti](../privacy-service/api/appendix.md#standard-namespaces) da [!DNL Privacy Service]o uno spazio nomi personalizzato definito dall&#39;organizzazione. |
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
>In questa sezione viene illustrato come formattare le richieste di privacy per l’ [!DNL Data Lake]. È vivamente consigliato di consultare la [!DNL Privacy Service UI](../privacy-service/ui/overview.md) o la [!DNL Privacy Service API](../privacy-service/api/getting-started.md) documentazione per i passaggi completi su come inviare un processo per la privacy, incluso come formattare correttamente i dati di identità dell&#39;utente inviati nei payload della richiesta.

Nella sezione seguente viene illustrato come effettuare richieste di privacy per [!DNL Data Lake] l’utente tramite l’ [!DNL Privacy Service] interfaccia utente o l’API.

### Utilizzo dell’interfaccia

Quando create richieste di processo nell’interfaccia utente, accertatevi di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profile]** in _[!UICONTROL Products]_per elaborare i processi per i dati memorizzati, rispettivamente, nel[!DNL Data Lake]o[!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

### Utilizzo dell&#39;API

Quando si creano richieste di processo nell&#39;API, tutte le `userIDs` richieste fornite devono utilizzare un archivio dati specifico `namespace` e `type` a seconda dell&#39;archivio dati a cui si riferiscono. Gli ID per il [!DNL Data Lake] server devono utilizzare &quot;non registrato&quot; per il relativo `type` valore e un `namespace` valore che corrisponda a una delle etichette [di](#privacy-labels) privacy aggiunte ai set di dati applicabili.

Inoltre, l&#39; `include` array del payload della richiesta deve includere i valori prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste al [!DNL Data Lake], l&#39;array deve includere il valore `aepDataLake`.

La richiesta seguente crea un nuovo processo per la privacy per l&#39;utente, utilizzando lo spazio dei nomi &quot;email_label&quot; non registrato. [!DNL Data Lake] Include inoltre il valore del prodotto per l&#39;array [!DNL Data Lake] `include` in questione:

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

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dall&#39;archivio [!DNL Data Lake] entro sette giorni. Durante quella finestra di sette giorni, i dati vengono eliminati in modo morbido e quindi non sono accessibili da alcun [!DNL Platform] servizio.

Nelle release future, [!DNL Platform] invierà una conferma a [!DNL Privacy Service] seguito dell&#39;eliminazione fisica dei dati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all&#39;elaborazione delle richieste di privacy per il [!DNL Data Lake]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di [privacy per il profilo](../profile/privacy.md) cliente in tempo reale, consulta il documento sull&#39;elaborazione delle richieste di privacy per lo [!DNL Profile] store.

## Appendice

La sezione seguente contiene informazioni aggiuntive per l’elaborazione delle richieste di privacy in [!DNL Data Lake].

### Etichettare i campi del tipo di mappa nidificati {#nested-maps}

È importante notare che esistono due tipi di campi di tipo mappa nidificati che non supportano l&#39;etichettatura della privacy:

* Campo di tipo mapping all&#39;interno di un campo di tipo matrice
* Campo di tipo mappa all’interno di un altro campo di tipo mappa

L&#39;elaborazione del lavoro sulla privacy per uno dei due esempi di cui sopra avrà un esito negativo. Per questo motivo, si consiglia di evitare di utilizzare campi di tipo mappa nidificati per memorizzare i dati privati dei clienti. Gli ID del consumatore pertinenti devono essere memorizzati come tipo di dati non mappato all&#39;interno del `identityMap` campo (stesso campo del tipo di mappa) per i set di dati basati su record, oppure come `endUserID` campo per i set di dati basati su serie temporali.