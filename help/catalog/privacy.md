---
keywords: Experience Platform;home;argomenti popolari;privacy data lake;identità namespace;privacy;data lake
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel data lake
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere ai propri dati personali, rinunciarvi o cancellarli, come stabilito dalle normative legali e organizzative sulla privacy. Questo documento descrive i concetti essenziali relativi all’elaborazione delle richieste di privacy per i dati dei clienti memorizzati nel data lake.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 1%

---

# Elaborazione delle richieste di privacy nel data lake

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere ai propri dati personali, di rinunciarvi o di eliminarli, in base alle normative legali e organizzative sulla privacy.

Questo documento descrive i concetti essenziali relativi all’elaborazione delle richieste di privacy per i dati dei clienti memorizzati nel data lake.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste di privacy per il data lake in Experience Platform. Se prevedi anche di effettuare richieste di privacy per l&#39;archivio dati Profilo cliente in tempo reale, oltre a questa esercitazione fai riferimento alla guida sull&#39;[elaborazione delle richieste di privacy per il profilo](../profile/privacy.md).
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta la [documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introduzione

Prima di leggere questa guida, è consigliabile avere una buona conoscenza dei seguenti servizi [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../privacy-service/home.md): gestisce le richieste dei clienti di accedere, rinunciare alle vendite o eliminare i propri dati personali nelle applicazioni Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): sistema di registrazione per la posizione e la derivazione dei dati in [!DNL Experience Platform]. Fornisce un’API che può essere utilizzata per aggiornare i metadati del set di dati.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
* [[!DNL Identity Service]](../identity-service/home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati sull&#39;esperienza del cliente collegando le identità tra dispositivi e sistemi.

## Comprendere gli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] esegue il bridging dei dati di identità del cliente tra sistemi e dispositivi. [!DNL Identity Service] utilizza gli spazi dei nomi di identità per fornire contesto ai valori di identità tramite la relazione con il rispettivo sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, come un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] mantiene un archivio di spazi dei nomi di identità definiti a livello globale (standard) e definiti dall&#39;utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle sue esigenze specifiche.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere [panoramica dello spazio dei nomi delle identità](../identity-service/features/namespaces.md).

## Aggiunta di dati di identità ai set di dati

Quando si creano richieste di privacy per il data lake, è necessario fornire valori di identità validi (e i namespace associati) per ogni singolo cliente al fine di individuare i propri dati ed elaborarli di conseguenza. Pertanto, tutti i set di dati soggetti a richieste di privacy devono contenere un descrittore di identità nel relativo schema XDM associato.

>[!NOTE]
>
>Al momento, eventuali set di dati basati su schemi che non supportano i metadati del descrittore di identità (ad esempio set di dati ad hoc) non possono essere elaborati nelle richieste di accesso a dati personali.

Questa sezione illustra i passaggi necessari per aggiungere un descrittore di identità allo schema XDM di un set di dati esistente. Se hai già un set di dati con un descrittore di identità, puoi passare alla [sezione successiva](#nested-maps).

>[!IMPORTANT]
>
>Quando decidi quali campi schema impostare come identità, tieni presente le [limitazioni dell&#39;utilizzo di campi di tipo mappa nidificati](#nested-maps).

Esistono due metodi per aggiungere un descrittore di identità a uno schema di set di dati:

* [Utilizzo dell’interfaccia utente](#identity-ui)
* [Mediante l’API](#identity-api)

### Utilizzo dell’interfaccia utente {#identity-ui}

Nell&#39;interfaccia utente [!DNL Experience Platform]l&#39;area di lavoro **[!UICONTROL Schemi]** consente di modificare gli schemi XDM esistenti. Per aggiungere un descrittore di identità a uno schema, selezionarlo dall&#39;elenco e seguire i passaggi per [impostare un campo schema come campo di identità](../xdm/tutorials/create-schema-ui.md#identity-field) nell&#39;esercitazione [!DNL Schema Editor].

Dopo aver impostato i campi appropriati nello schema come campi di identità, puoi passare alla sezione successiva su [invio di richieste di privacy](#submit).

### Mediante l’API {#identity-api}

>[!NOTE]
>
>Questa sezione presuppone che tu conosca il valore ID URI univoco dello schema XDM del set di dati. Se non si conosce questo valore, è possibile recuperarlo utilizzando l&#39;API [!DNL Catalog Service]. Dopo aver letto la sezione [guida introduttiva](./api/getting-started.md) della guida per gli sviluppatori, segui i passaggi descritti in per [elencare](./api/list-objects.md) o [cercare](./api/look-up-object.md) [!DNL Catalog] oggetti per trovare il set di dati. L&#39;ID schema si trova in `schemaRef.id`
>
>Questa sezione presuppone anche che tu sappia come effettuare chiamate all’API Schema Registry. Per informazioni importanti relative all&#39;utilizzo dell&#39;API, inclusa la conoscenza di `{TENANT_ID}` e del concetto di contenitori, vedere la sezione [guida introduttiva](../xdm/api/getting-started.md) della guida API.

È possibile aggiungere un descrittore di identità allo schema XDM di un set di dati effettuando una richiesta POST all&#39;endpoint `/descriptors` nell&#39;API [!DNL Schema Registry].

**Formato API**

```http
POST /descriptors
```

**Richiesta**

La seguente richiesta definisce un descrittore di identità in un campo &quot;indirizzo e-mail&quot; in uno schema di esempio.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `@type` | Tipo di descrittore da creare. Per i descrittori di identità, il valore deve essere &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | ID URI univoco dello schema XDM del set di dati. |
| `xdm:sourceVersion` | Versione dello schema XDM specificata in `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Percorso del campo schema a cui viene applicato il descrittore. |
| `xdm:namespace` | Uno dei [spazi dei nomi di identità standard](../privacy-service/api/appendix.md#standard-namespaces) riconosciuti da [!DNL Privacy Service] o uno spazio dei nomi personalizzato definito dall&#39;organizzazione. |
| `xdm:property` | &quot;xdm:id&quot; o &quot;xdm:code&quot;, a seconda dello spazio dei nomi utilizzato in `xdm:namespace`. |
| `xdm:isPrimary` | Valore booleano facoltativo. Se è true, indica che il campo è un&#39;identità primaria. Gli schemi possono contenere una sola identità primaria. Se non incluso, viene impostato automaticamente su false. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato.

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
>Questa sezione illustra come formattare le richieste di privacy per il data lake. Si consiglia vivamente di rivedere la documentazione dell&#39;[[!DNL Privacy Service] interfaccia utente](../privacy-service/ui/overview.md) o dell&#39;[[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) per conoscere i passaggi completi per l&#39;invio di un processo per la privacy, incluso il modo corretto di formattare i dati di identità utente inviati nei payload delle richieste.

La sezione seguente illustra come effettuare richieste di privacy per il data lake utilizzando l&#39;interfaccia utente o l&#39;API [!DNL Privacy Service].

>[!IMPORTANT]
>
>Non è possibile garantire la quantità di tempo necessaria per il completamento di una richiesta di accesso a dati personali. Se durante l’elaborazione di una richiesta si verificano modifiche all’interno del data lake, non è possibile garantire nemmeno se tali record vengono elaborati o meno.

### Utilizzo dell’interfaccia utente

Quando crei richieste di lavoro nell&#39;interfaccia utente, assicurati di selezionare **[!UICONTROL AEP Data Lake]** in **[!UICONTROL Prodotti]** per elaborare i processi per i dati memorizzati nel data lake.

![Immagine che mostra il prodotto del data lake selezionato nella finestra di dialogo per la creazione di richieste di accesso a dati personali](./images/privacy/product-value.png)

### Mediante l’API

Quando si creano richieste di processi nell&#39;API, qualsiasi `userIDs` fornito deve utilizzare un `namespace` e un `type` specifici a seconda dell&#39;archivio dati a cui si applicano. Gli ID per il data lake devono utilizzare `unregistered` per il valore `type` e un valore `namespace` che corrisponde a una delle [etichette per la privacy](#privacy-labels) aggiunte ai set di dati applicabili.

Inoltre, l&#39;array `include` del payload della richiesta deve includere i valori del prodotto per i diversi archivi di dati a cui viene effettuata la richiesta. Quando si eseguono richieste al data lake, l&#39;array deve includere il valore `aepDataLake`.

La richiesta seguente crea un nuovo processo di privacy per il data lake, utilizzando lo spazio dei nomi `email_label` non registrato. Include inoltre il valore del prodotto per il data lake nell&#39;array `include`:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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

>[!IMPORTANT]
>
>Platform elabora le richieste di accesso a dati personali in tutte le [sandbox](../sandboxes/home.md) appartenenti alla tua organizzazione. Di conseguenza, qualsiasi intestazione `x-sandbox-name` inclusa nella richiesta viene ignorata dal sistema.

## Elaborazione richiesta di eliminazione

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dal data lake entro sette giorni. Durante tale finestra di sette giorni, i dati vengono eliminati in modo non permanente e non sono quindi accessibili da alcun servizio [!DNL Platform].

Se nella richiesta di accesso a dati personali hai incluso anche `ProfileService` o `identity`, i dati associati verranno gestiti separatamente. Per ulteriori informazioni, vedere la sezione relativa all&#39;elaborazione di [richieste di eliminazione per il profilo](../profile/privacy.md#delete).

## Passaggi successivi

Dopo aver letto questo documento, ti vengono presentati i concetti importanti relativi all’elaborazione delle richieste di accesso a dati personali per il data lake. Si consiglia di continuare a leggere la documentazione fornita in questa guida per comprendere meglio come gestire i dati di identità e creare processi sulla privacy.

Per informazioni sulla procedura di elaborazione delle richieste di accesso a dati personali per l&#39;archivio [!DNL Profile], vedere il documento sull&#39;elaborazione delle richieste di accesso a dati personali per Real-Time Customer Profile](../profile/privacy.md).[

## Appendice

La sezione seguente contiene informazioni aggiuntive per l’elaborazione delle richieste di accesso a dati personali nel data lake.

### Etichettatura dei campi di tipo mappa nidificati {#nested-maps}

È importante notare che esistono due tipi di campi di tipo mappa nidificati che non supportano l’etichettatura della privacy:

* Campo di tipo mappa all’interno di un campo di tipo array
* Un campo di tipo mappa all’interno di un altro campo di tipo mappa

L’elaborazione del processo di privacy per uno dei due esempi precedenti alla fine avrà esito negativo. Per questo motivo, si consiglia di evitare di utilizzare campi di tipo mappa nidificati per memorizzare dati privati dei clienti. Gli ID consumer rilevanti devono essere memorizzati come tipo di dati non mappa nel campo `identityMap` (a sua volta un campo di tipo mappa) per i set di dati basati su record o nel campo `endUserID` per i set di dati basati su serie temporali.
