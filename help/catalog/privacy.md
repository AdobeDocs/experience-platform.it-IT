---
keywords: ' Experience Platform;home;argomenti popolari;data lago privacy;spazi dei nomi di identità;privacy;data lago'
solution: Experience Platform
title: Privacy Request Processing in Data Lake
topic: overview
description: ' Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i propri dati personali, come indicato dalle normative sulla privacy legali e organizzative. Questo documento tratta i concetti essenziali relativi all''elaborazione delle richieste di privacy per i dati dei clienti memorizzati nel Data Lake.'
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy in [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i propri dati personali, come indicato dalle normative sulla privacy legali e organizzative.

Questo documento tratta i concetti essenziali relativi all&#39;elaborazione delle richieste di privacy per i dati dei clienti memorizzati in [!DNL Data Lake].

## Introduzione

Prima di leggere la presente guida è consigliabile conoscere correttamente i seguenti servizi [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): Il sistema di record per la posizione dei dati e la linea  [!DNL Experience Platform]. Fornisce un&#39;API che può essere utilizzata per aggiornare i metadati del set di dati.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza gli spazi dei nomi di identità per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o  Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] gestisce un archivio di spazi dei nomi di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere la [panoramica dello spazio dei nomi delle identità](../identity-service/namespaces.md).

## Aggiunta di dati di identità ai set di dati

Durante la creazione di richieste di privacy per [!DNL Data Lake], è necessario fornire valori di identità validi (e relativi spazi di nomi associati) a ciascun singolo cliente al fine di individuare i propri dati ed elaborarli di conseguenza. Pertanto, tutti i set di dati soggetti a richieste di privacy devono contenere un descrittore di identità nello schema XDM associato.

>[!NOTE]
>
>Eventuali set di dati basati su schemi che non supportano i metadati del descrittore di identità (ad esempio, set di dati ad hoc) non possono attualmente essere elaborati nelle richieste di privacy.

Questa sezione descrive i passaggi necessari per aggiungere un descrittore di identità allo schema XDM di un set di dati esistente. Se disponete già di un set di dati con un descrittore di identità, potete passare alla sezione [successiva](#nested-maps).

>[!IMPORTANT]
>
>Per decidere quali campi dello schema impostare come identità, tenere presente le [limitazioni dell&#39;utilizzo di campi del tipo di mappa nidificati](#nested-maps).

Esistono due metodi per aggiungere un descrittore di identità a uno schema di set di dati:

* [Utilizzo dell’interfaccia](#identity-ui)
* [Utilizzo dell&#39;API](#identity-api)

### Utilizzo dell&#39;interfaccia {#identity-ui}

Nell&#39;interfaccia [!DNL Experience Platform ]utente, l&#39;area di lavoro **[!UICONTROL Schemas]** consente di modificare gli schemi XDM esistenti. Per aggiungere un descrittore di identità a uno schema, selezionare lo schema dall&#39;elenco e seguire i passaggi per [impostare un campo di schema come campo di identità](../xdm/tutorials/create-schema-ui.md#identity-field) nell&#39;esercitazione [!DNL Schema Editor].

Dopo aver impostato i campi appropriati nello schema come campi di identità, è possibile passare alla sezione successiva in [invio delle richieste di privacy](#submit).

### Utilizzo dell&#39;API {#identity-api}

>[!NOTE]
>
>Questa sezione presuppone che si conosca il valore ID URI univoco dello schema XDM del set di dati. Se non conosci questo valore, puoi recuperarlo utilizzando l&#39;API [!DNL Catalog Service]. Dopo aver letto la sezione [guida introduttiva](./api/getting-started.md) della guida per gli sviluppatori, seguire i passaggi descritti in per [elencare](./api/list-objects.md) o [cercare gli oggetti ](./api/look-up-object.md) [!DNL Catalog] per trovare il set di dati. L&#39;ID dello schema si trova in `schemaRef.id`
>
> Questa sezione include le chiamate all&#39;API del Registro di sistema dello schema. Per informazioni importanti sull&#39;utilizzo dell&#39;API, inclusa la conoscenza di `{TENANT_ID}` e del concetto di contenitori, consultate la sezione [guida introduttiva](../xdm/api/getting-started.md) della guida per gli sviluppatori.

È possibile aggiungere un descrittore di identità allo schema XDM di un dataset effettuando una richiesta di POST all&#39;endpoint `/descriptors` nell&#39;API [!DNL Schema Registry].

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
| `xdm:namespace` | Uno degli [spazi dei nomi di identità standard](../privacy-service/api/appendix.md#standard-namespaces) riconosciuti da [!DNL Privacy Service] oppure uno spazio dei nomi personalizzato definito dall&#39;organizzazione. |
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
>Questa sezione descrive come formattare le richieste di privacy per [!DNL Data Lake]. È vivamente consigliato di consultare la documentazione [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) o [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) per i passaggi completi su come inviare un processo di privacy, incluso come formattare correttamente i dati di identità dell&#39;utente inviati nei payload della richiesta.

La sezione seguente illustra come effettuare richieste di privacy per [!DNL Data Lake] utilizzando l&#39;interfaccia utente o l&#39;API [!DNL Privacy Service].

>[!IMPORTANT]
>
>Il tempo necessario per completare una richiesta di privacy non può essere garantito. Se si verificano modifiche all&#39;interno del Data Lake mentre una richiesta è ancora in elaborazione, non è possibile garantire l&#39;elaborazione di tali record.

### Utilizzo dell’interfaccia

Durante la creazione di richieste di processo nell&#39;interfaccia utente, assicurarsi di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profile]** in **[!UICONTROL Products]** al fine di elaborare i processi per i dati memorizzati rispettivamente in [!DNL Data Lake] o [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

### Utilizzo dell&#39;API

Durante la creazione di richieste di processo nell&#39;API, qualsiasi `userIDs` fornito deve utilizzare `namespace` e `type` specifici a seconda dell&#39;archivio dati a cui si applicano. Gli ID per il [!DNL Data Lake] devono utilizzare &quot;non registrato&quot; per il relativo valore `type` e un valore `namespace` che corrisponda a uno delle [etichette per la privacy](#privacy-labels) aggiunte ai set di dati applicabili.

Inoltre, l&#39;array `include` del payload della richiesta deve includere i valori del prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste a [!DNL Data Lake], l&#39;array deve includere il valore `aepDataLake`.

La richiesta seguente crea un nuovo processo per la privacy per [!DNL Data Lake], utilizzando lo spazio dei nomi &quot;email_label&quot; non registrato. Include inoltre il valore del prodotto per [!DNL Data Lake] nell&#39;array `include`:

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

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dal [!DNL Data Lake] entro sette giorni. Durante quella finestra di sette giorni, i dati vengono eliminati in modo morbido e pertanto non sono accessibili da alcun servizio [!DNL Platform].

Nelle release future, [!DNL Platform] invierà una conferma a [!DNL Privacy Service] dopo che i dati saranno stati fisicamente eliminati.

## Passaggi successivi

Leggendo questo documento, è stato introdotto l&#39;importante concetto relativo all&#39;elaborazione delle richieste di privacy per il [!DNL Data Lake]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di privacy per lo store [!DNL Profile], vedere il documento sull&#39;elaborazione delle richieste di privacy per il profilo cliente in tempo reale](../profile/privacy.md).[

## Appendice

La sezione seguente contiene informazioni aggiuntive per l&#39;elaborazione delle richieste di privacy in [!DNL Data Lake].

### Etichettare i campi del tipo di mappa nidificati {#nested-maps}

È importante notare che esistono due tipi di campi di tipo mappa nidificati che non supportano l&#39;etichettatura della privacy:

* Campo di tipo mapping all&#39;interno di un campo di tipo matrice
* Campo di tipo mappa all’interno di un altro campo di tipo mappa

L&#39;elaborazione del lavoro sulla privacy per uno dei due esempi di cui sopra avrà un esito negativo. Per questo motivo, si consiglia di evitare di utilizzare campi di tipo mappa nidificati per memorizzare i dati privati dei clienti. Gli ID del consumatore pertinenti devono essere memorizzati come tipo di dati non mappato all&#39;interno del campo `identityMap` (stesso campo del tipo di mappa) per i set di dati basati su record, oppure nel campo `endUserID` per i set di dati basati su serie temporali.