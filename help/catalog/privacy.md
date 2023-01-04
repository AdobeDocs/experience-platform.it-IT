---
keywords: Experience Platform;home;argomenti popolari;privacy data lake;spazi dei nomi di identità;privacy;data lake
solution: Experience Platform
title: Elaborazione delle richieste di privacy in Data Lake
topic-legacy: overview
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o all’eliminazione dei propri dati personali come delineato dalle normative legali e organizzative sulla privacy. Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste sulla privacy per i dati dei clienti archiviati nel data lake.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---

# Elaborazione della richiesta di accesso a dati nel lago dati

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti per accedere, rinunciare alla vendita o cancellare i loro dati personali come delineato dalle normative legali e organizzative sulla privacy.

Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste sulla privacy per i dati dei clienti archiviati nel data lake.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste di privacy per il data lake, ad Experience Platform. Se prevedi anche di effettuare richieste di privacy per l’archivio dati Profilo cliente in tempo reale, consulta la guida su [elaborazione della richiesta di accesso a dati personali per il profilo](../profile/privacy.md) oltre a questa esercitazione.
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta [Documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introduzione

Si consiglia di avere una comprensione operativa dei seguenti elementi [!DNL Experience Platform] servizi prima di leggere questa guida:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestisce le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o all’eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): Il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di [!DNL Experience Platform]. Fornisce un’API che può essere utilizzata per aggiornare i metadati del set di dati.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza spazi dei nomi di identità per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] mantiene un archivio di namespace di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; ed &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedi [panoramica dello spazio dei nomi identità](../identity-service/namespaces.md).

## Aggiunta di dati di identità ai set di dati

Durante la creazione di richieste di privacy per il data lake, è necessario fornire valori di identità validi (e i relativi namespace associati) per ogni singolo cliente al fine di individuare i propri dati ed elaborarli di conseguenza. Pertanto, tutti i set di dati soggetti a richieste di privacy devono contenere un descrittore di identità nello schema XDM associato.

>[!NOTE]
>
>Eventuali set di dati basati su schemi che non supportano i metadati del descrittore di identità (come i set di dati ad hoc) attualmente non possono essere elaborati nelle richieste di privacy.

Questa sezione descrive i passaggi necessari per aggiungere un descrittore di identità allo schema XDM di un set di dati esistente. Se disponi già di un set di dati con un descrittore di identità, puoi passare alla [sezione successiva](#nested-maps).

>[!IMPORTANT]
>
>Quando decidi quali campi dello schema impostare come identità, ricorda [limitazioni dell’utilizzo di campi di tipo mappa nidificati](#nested-maps).

Esistono due metodi per aggiungere un descrittore di identità a uno schema di set di dati:

* [Utilizzo dell’interfaccia](#identity-ui)
* [Mediante l’API](#identity-api)

### Utilizzo dell’interfaccia {#identity-ui}

In [!DNL Experience Platform ]interfaccia utente, **[!UICONTROL Schemi]** workspace consente di modificare gli schemi XDM esistenti. Per aggiungere un descrittore di identità a uno schema, selezionalo dall’elenco e segui i passaggi descritti per [impostazione di un campo schema come campo di identità](../xdm/tutorials/create-schema-ui.md#identity-field) in [!DNL Schema Editor] esercitazione.

Dopo aver impostato come campi di identità i campi appropriati all&#39;interno dello schema, puoi passare alla sezione successiva in [invio di richieste di privacy](#submit).

### Mediante l’API {#identity-api}

>[!NOTE]
>
>Questa sezione presuppone che tu conosca il valore ID URI univoco dello schema XDM del set di dati. Se non conosci questo valore, puoi recuperarlo utilizzando il [!DNL Catalog Service] API. Dopo aver letto [guida introduttiva](./api/getting-started.md) nella sezione della guida per gli sviluppatori, segui i passaggi descritti in per [elenco](./api/list-objects.md) o [cercare](./api/look-up-object.md) [!DNL Catalog] oggetti per trovare il set di dati. L&#39;ID dello schema si trova in `schemaRef.id`
>
>Questa sezione presuppone anche che tu sappia come effettuare chiamate all&#39;API del Registro di sistema dello schema. Per informazioni importanti sull’utilizzo dell’API, inclusa la conoscenza del `{TENANT_ID}` e il concetto di contenitori, vedi [guida introduttiva](../xdm/api/getting-started.md) della guida API.

Puoi aggiungere un descrittore di identità allo schema XDM di un set di dati effettuando una richiesta di POST al gruppo `/descriptors` punto finale [!DNL Schema Registry] API.

**Formato API**

```http
POST /descriptors
```

**Richiesta**

La richiesta seguente definisce un descrittore di identità su un campo &quot;Indirizzo e-mail&quot; in uno schema di esempio.

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
| `@type` | Il tipo di descrittore da creare. Per i descrittori di identità, il valore deve essere &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | ID URI univoco dello schema XDM del set di dati. |
| `xdm:sourceVersion` | Versione dello schema XDM specificato in `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Percorso del campo dello schema a cui viene applicato il descrittore. |
| `xdm:namespace` | Uno dei [spazi dei nomi delle identità standard](../privacy-service/api/appendix.md#standard-namespaces) riconosciuti [!DNL Privacy Service]o uno spazio dei nomi personalizzato definito dall’organizzazione. |
| `xdm:property` | &quot;xdm:id&quot; o &quot;xdm:code&quot;, a seconda dello spazio dei nomi utilizzato in `xdm:namespace`. |
| `xdm:isPrimary` | Un valore booleano facoltativo. Se true, indica che il campo è un’identità principale. Gli schemi possono contenere una sola identità principale. Predefinito su false se non incluso. |

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
>Questa sezione descrive come formattare le richieste di privacy per il data lake. Si consiglia vivamente di rivedere il [[!DNL Privacy Service] Interfaccia](../privacy-service/ui/overview.md) o [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) documentazione completa sui passaggi per l’invio di un processo relativo alla privacy, inclusa la modalità di formattazione corretta dei dati di identità utente inviati nei payload della richiesta.

La sezione seguente illustra come effettuare richieste di privacy per il data lake utilizzando [!DNL Privacy Service] Interfaccia utente o API.

>[!IMPORTANT]
>
>Il tempo necessario per completare una richiesta di accesso a dati personali non può essere garantito. Se si verificano modifiche all’interno del data lake durante l’elaborazione di una richiesta, non è possibile garantire l’elaborazione di tali record.

### Utilizzo dell’interfaccia

Quando crei richieste di lavoro nell’interfaccia utente, assicurati di selezionare **[!UICONTROL AEP Data Lake]** sotto **[!UICONTROL Prodotti]** al fine di elaborare i processi per i dati memorizzati nel lago dati.

![Immagine che mostra il prodotto data lake selezionato nella finestra di dialogo di creazione della richiesta di privacy](./images/privacy/product-value.png)

### Mediante l’API

Quando crei richieste di lavoro nell’API, qualsiasi `userIDs` che devono utilizzare un `namespace` e `type` a seconda dell’archivio dati a cui si applicano. Gli ID per il data lake devono utilizzare `unregistered` per i `type` e un `namespace` che corrisponde a uno dei valori [etichette privacy](#privacy-labels) che sono stati aggiunti ai set di dati applicabili.

Inoltre, il `include` la matrice del payload della richiesta deve includere i valori di prodotto per i diversi archivi di dati in cui viene effettuata la richiesta. Quando si effettuano richieste al data lake, la matrice deve includere il valore `aepDataLake`.

La seguente richiesta crea un nuovo processo di privacy per il data lake, utilizzando il `email_label` spazio dei nomi. Include inoltre il valore del prodotto per il data lake nel `include` array:

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
>Platform elabora le richieste di privacy in tutti [sandbox](../sandboxes/home.md) appartenente alla tua organizzazione. Di conseguenza, qualsiasi `x-sandbox-name` l’intestazione inclusa nella richiesta viene ignorata dal sistema.

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di cancellazione da [!DNL Privacy Service], [!DNL Platform] invia conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dal data lake entro sette giorni. Durante la finestra di sette giorni, i dati vengono cancellati in modo morbido e non sono quindi accessibili da nessuno [!DNL Platform] servizio.

Se hai incluso anche `ProfileService` o `identity` nella richiesta di accesso a dati personali, i dati associati vengono gestiti separatamente. Vedi la sezione su [elimina l’elaborazione della richiesta per il profilo](../profile/privacy.md#delete) per ulteriori informazioni.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all’elaborazione delle richieste di privacy per il data lake. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la comprensione su come gestire i dati di identità e creare processi di privacy.

Visualizza il documento in [elaborazione della richiesta di accesso a dati personali per Profilo cliente in tempo reale](../profile/privacy.md) per i passaggi relativi all’elaborazione delle richieste di privacy per [!DNL Profile] archiviare.

## Appendice

La sezione seguente contiene informazioni aggiuntive per l’elaborazione delle richieste di privacy nel data lake.

### Etichettatura dei campi nidificati del tipo di mappa {#nested-maps}

È importante notare che esistono due tipi di campi di tipo mappa nidificati che non supportano l’etichettatura sulla privacy:

* Campo di tipo mappa all’interno di un campo di tipo matrice
* Campo di tipo mappa all’interno di un altro campo di tipo mappa

L’elaborazione dei processi per la privacy per uno dei due esempi di cui sopra avrà esito negativo. Per questo motivo, si consiglia di evitare di utilizzare campi nidificati del tipo di mappa per memorizzare i dati privati dei clienti. Gli ID consumer rilevanti devono essere memorizzati come tipo di dati non mappato all’interno di `identityMap` campo (stesso campo di tipo mappa) per set di dati basati su record o `endUserID` campo per i set di dati basati su serie temporali.
