---
description: Questa configurazione ti consente di indicare informazioni di base come il nome della destinazione, la categoria, la descrizione, il logo e altro ancora. Le impostazioni di questa configurazione determinano anche il modo in cui gli utenti Experienci Platform si autenticano nella destinazione, il modo in cui viene visualizzata nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.
title: Opzioni di configurazione della destinazione di streaming per Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 3%

---

# Configurazione della destinazione di streaming {#destination-configuration}

## Panoramica {#overview}

Questa configurazione consente di indicare informazioni essenziali per la destinazione di streaming, come il nome della destinazione, la categoria, la descrizione e altro ancora. Le impostazioni di questa configurazione determinano anche il modo in cui gli utenti Experienci Platform si autenticano nella destinazione, il modo in cui viene visualizzata nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.

Questa configurazione collega a questa anche le altre configurazioni necessarie per il funzionamento della destinazione (metadati del server di destinazione e del pubblico). Scopri come fare riferimento alle due configurazioni in una [sezione più avanti](./destination-configuration.md#connecting-all-configurations).

È possibile configurare la funzionalità descritta in questo documento utilizzando `/authoring/destinations` Endpoint API Letto [Operazioni degli endpoint API per le destinazioni](./destination-configuration-api.md) per un elenco completo delle operazioni che è possibile eseguire sull&#39;endpoint.

## Esempio di configurazione dello streaming {#example-configuration}

Questa è una configurazione di esempio di una destinazione di streaming fittizia, Moviestar, che ha endpoint in quattro posizioni sul globo. La destinazione appartiene alla categoria delle destinazioni mobili.

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointRegion",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "backfillHistoricalProfileData":true
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo di Experienci Platform. |
| `description` | Stringa | Fornisci una descrizione della scheda di destinazione nel catalogo delle destinazioni di Experience Platform. Puntare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizzare `TEST` la prima volta che configuri la destinazione. |

{style="table-layout:auto"}

## Configurazioni di autenticazione del cliente {#customer-authentication-configurations}

Questa sezione nella configurazione delle destinazioni genera il [Configurare una nuova destinazione](/help/destinations/ui/connect-destination.md) nell’interfaccia utente di Experience Platform, in cui gli utenti connettono Experience Platform agli account che hanno con la tua destinazione. A seconda dell’opzione di autenticazione indicata nella `authType` , la pagina di Experience Platform viene generata come segue per gli utenti:

### Autenticazione Bearer

Quando configuri il tipo di autenticazione bearer, gli utenti devono immettere il token bearer ottenuto dalla destinazione.

![Rendering dell’interfaccia utente con autenticazione bearer](assets/bearer-authentication-ui.png)

### Autenticazione OAuth 2

Gli utenti selezionano **[!UICONTROL Connetti alla destinazione]** per attivare il flusso di autenticazione OAuth 2 nella destinazione, come mostrato nell’esempio seguente per la destinazione Tipi di pubblico personalizzati di Twitter. Per informazioni dettagliate sulla configurazione dell’autenticazione OAuth 2 per l’endpoint di destinazione, consulta la sezione dedicata [Destination SDK pagina di autenticazione OAuth 2](./oauth2-authentication.md).

![Rendering dell’interfaccia utente con autenticazione OAuth 2](assets/oauth2-authentication-ui.png)

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experienci Platform sul server. Consulta `authType` per i valori accettati. |
| `authType` | Stringa | I valori accettati per le destinazioni di streaming sono:<ul><li>`BASIC`. Se la destinazione supporta l&#39;autenticazione di base, impostare `"authType":"Basic"` e  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` nel [sezione di consegna della destinazione](./destination-configuration.md).</li><li>`BEARER`. Se la destinazione supporta l&#39;autenticazione bearer, impostare `"authType":"Bearer"` e  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` nel [sezione di consegna della destinazione](./destination-configuration.md).</li><li>`OAUTH2`. Se la destinazione supporta l&#39;autenticazione OAuth 2, impostare `"authType":"OAUTH2"` e aggiungere i campi obbligatori per OAuth 2, come mostrato nella [Destination SDK pagina di autenticazione OAuth 2](./oauth2-authentication.md). Inoltre, imposta `"authenticationRule":"CUSTOMER_AUTHENTICATION"` nel [sezione di consegna della destinazione](./destination-configuration.md).</li> |

{style="table-layout:auto"}

## Campi dati cliente {#customer-data-fields}

Utilizza questa sezione per chiedere agli utenti di compilare campi personalizzati, specifici per la tua destinazione, durante la connessione alla destinazione nell’interfaccia utente di Experience Platform. La configurazione si riflette nel flusso di autenticazione come mostrato di seguito.

![Flusso di autenticazione campo personalizzato](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>Puoi accedere e utilizzare gli input dei clienti dai campi dati dei clienti nei modelli. Utilizzare la macro `{{customerData.name}}`. Ad esempio, se chiedi agli utenti di inserire un campo ID cliente, con il nome `userId`, è possibile accedervi nei modelli utilizzando la macro `{{customerData.userId}}`. Visualizza un esempio di come un campo di dati cliente viene utilizzato nell’URL dell’endpoint API, nel [configurazione del server di destinazione](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs).

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Immetti un nome per il campo personalizzato che stai presentando. |
| `type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer`. |
| `title` | Stringa | Indica il nome del campo, così come viene visualizzato dai clienti nell’interfaccia utente di Experience Platform. |
| `description` | Stringa | Fornisci una descrizione per il campo personalizzato. |
| `isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l&#39;utente. |
| `pattern` | Stringa | Se necessario, applica un pattern per il campo personalizzato. Utilizza espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o trattini bassi, immetti `^[A-Za-z]+$` in questo campo. |

{style="table-layout:auto"}

## Attributi dell’interfaccia utente {#ui-attributes}

Questa sezione fa riferimento agli elementi dell’interfaccia utente nella configurazione precedente che l’Adobe deve utilizzare per la destinazione nell’interfaccia utente di Adobe Experience Platform. Vedi sotto:

![Immagine della configurazione degli attributi dell’interfaccia utente.](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `documentationLink` | Stringa | Fa riferimento alla pagina della documentazione in [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizzare `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione chiamata Moviestar, puoi utilizzare `http://www.adobe.com/go/destinations-moviestar-en`. Tieni presente che questo collegamento funziona solo dopo che Adobe ha impostato la destinazione live e che la documentazione è stata pubblicata. |
| `category` | Stringa | Fa riferimento alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, consulta [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilizza uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br> Al momento è possibile selezionare una sola categoria per destinazione. |
| `connectionType` | Stringa | `Server-to-server` è attualmente l’unica opzione disponibile. |
| `frequency` | Stringa | Si riferisce al tipo di esportazione dei dati supportato dalla destinazione. Valori supportati: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style="table-layout:auto"}

## Configurazione dello schema nel passaggio di mappatura {#schema-configuration}

![Abilita passaggio di mappatura](./assets/enable-mapping-step.png)

Utilizzare i parametri in `schemaConfig` per abilitare il passaggio di mappatura del flusso di lavoro di attivazione della destinazione. Utilizzando i parametri descritti di seguito, puoi determinare se gli utenti Experienci Platform possono mappare gli attributi e/o le identità del profilo allo schema desiderato sul lato della destinazione.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `profileFields` | Array | *Non mostrato nella configurazione di esempio precedente.* Quando si aggiungono impostazioni predefinite `profileFields`Tuttavia, gli utenti Experienci Platform possono scegliere di mappare gli attributi di Platform agli attributi predefiniti sul lato della destinazione. |
| `profileRequired` | Booleano | Utilizzare `true` gli utenti devono essere in grado di mappare gli attributi del profilo da Experience Platform ad attributi personalizzati sul lato della destinazione, come mostrato nella configurazione di esempio precedente. |
| `segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilizzare `true` gli utenti devono essere in grado di mappare gli spazi dei nomi delle identità dall’Experience Platform allo schema desiderato. |

{style="table-layout:auto"}

## Identità e attributi {#identities-and-attributes}

I parametri di questa sezione determinano le identità accettate dalla destinazione. Questa configurazione popola anche le identità e gli attributi di destinazione in [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) dell’interfaccia utente di Experience Platform, in cui gli utenti mappano identità e attributi dai loro schemi XDM allo schema nella destinazione.

Indicare quale [!DNL Platform] identità che i clienti possono esportare nella tua destinazione. Alcuni esempi sono [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono [!DNL Platform] spazi dei nomi di identità che i clienti possono mappare su spazi dei nomi di identità dalla tua destinazione. Puoi anche indicare se i clienti possono mappare spazi dei nomi personalizzati alle identità supportate dalla destinazione (`acceptsCustomNamespaces: true`) e se i clienti possono mappare gli attributi XDM standard sulle identità supportate dalla destinazione (`acceptsAttributes: true`).

Gli spazi dei nomi delle identità non richiedono una corrispondenza da 1 a 1 tra [!DNL Platform] e la tua destinazione.
Ad esempio, i clienti possono mappare una [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL IDFA] dalla destinazione, oppure possono mappare lo stesso [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL Customer ID] dello spazio dei nomi nella destinazione.

Ulteriori informazioni sulle identità in [Panoramica sullo spazio dei nomi delle identità](/help/identity-service/namespaces.md).

![Rendering delle identità di destinazione nell’interfaccia utente](./assets/target-identities-ui.png)

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `acceptsAttributes` | Booleano | Indica se i clienti possono mappare gli attributi di profilo standard all’identità che stai configurando. |
| `acceptsCustomNamespaces` | Booleano | Indica se i clienti possono impostare spazi dei nomi personalizzati nella destinazione. |
| `transformation` | Stringa | *Non visualizzato nella configurazione di esempio*. Utilizzato, ad esempio, quando [!DNL Platform] il cliente ha come attributo indirizzi e-mail semplici e la tua piattaforma accetta solo e-mail con hash. In questo oggetto, puoi applicare la trasformazione necessaria (ad esempio, trasformare l’e-mail in minuscolo, quindi in hash). Per un esempio, vedi `requiredTransformation` nel [riferimento API per la configurazione di destinazione](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | Indica quale [spazi dei nomi di identità standard](/help/identity-service/namespaces.md#standard) (ad esempio, IDFA) i clienti possono effettuare il mapping all’identità che stai configurando. <br> Quando si utilizza `acceptedGlobalNamespaces`, è possibile utilizzare `"requiredTransformation":"sha256(lower($))"` agli indirizzi e-mail o ai numeri di telefono in minuscolo e con hash. |

{style="table-layout:auto"}

## Consegna della destinazione {#destination-delivery}

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla tua destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzare `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite un nome utente e una password, un token bearer o un altro metodo di autenticazione. Ad esempio, puoi selezionare questa opzione se hai selezionato anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizzare `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la tua destinazione e il [!DNL Platform] Il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare un oggetto credenziali utilizzando [Credenziali](./credentials-configuration-api.md) configurazione. </li><li>Utilizzare `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationServerId` | Stringa | Il `instanceId` del [configurazione del server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |

{style="table-layout:auto"}

## Configurazione della mappatura dei segmenti {#segment-mapping}

![Sezione configurazione mappatura segmenti](./assets/segment-mapping-configuration.png)

Questa sezione della configurazione di destinazione fa riferimento al modo in cui i metadati del segmento come i nomi di segmento o gli ID devono essere condivisi tra Experience Platform e la destinazione.

Attraverso il `audienceTemplateId`, anche questa sezione unisce questa configurazione con [configurazione dei metadati del pubblico](./audience-metadata-management.md).

I parametri mostrati nella configurazione precedente sono descritti nella [riferimento API per l’endpoint &quot;destinations&quot;](./destination-configuration-api.md).

## Criterio di aggregazione {#aggregation}

![Criteri di aggregazione nel modello di configurazione](./assets/aggregation-configuration.png)

Questa sezione ti consente di impostare i criteri di aggregazione da utilizzare in Experience Platform per l’esportazione dei dati nella destinazione.

Un criterio di aggregazione determina il modo in cui i profili esportati vengono combinati nelle esportazioni di dati. Le opzioni disponibili sono:
* Aggregazione ottimale
* Aggregazione configurabile (mostrata nella configurazione precedente)

Leggi la sezione su [utilizzo dei modelli](./message-format.md#using-templating) e [esempi chiave di aggregazione](./message-format.md#template-aggregation-key) per informazioni su come includere il criterio di aggregazione nel modello di trasformazione dei messaggi in base al criterio di aggregazione selezionato.

### Aggregazione ottimale {#best-effort-aggregation}

>[!TIP]
>
>Utilizza questa opzione se l’endpoint API accetta meno di 100 profili per chiamata API.

Questa opzione funziona meglio per le destinazioni che preferiscono meno profili per richiesta e che preferiscono richiedere più richieste con meno dati rispetto a meno richieste con più dati.

Utilizza il `maxUsersPerRequest` per specificare il numero massimo di profili che la destinazione può accettare in una richiesta.

### Aggregazione configurato {#configurable-aggregation}

Questa opzione funziona meglio se preferisci prendere batch di grandi dimensioni con migliaia di profili nella stessa chiamata. Questa opzione consente inoltre di aggregare i profili esportati in base a regole di aggregazione complesse.

Questa opzione consente di:

* Imposta il tempo massimo e il numero massimo di profili da aggregare prima che venga effettuata una chiamata API alla destinazione.
* Aggrega i profili esportati mappati sulla destinazione in base a:
   * ID segmento;
   * Stato del segmento;
   * Identità o gruppi di identità.

>[!NOTE]
>
>Quando utilizzi l’opzione di aggregazione configurabile per la destinazione, presta attenzione ai valori minimo e massimo che puoi utilizzare per i due parametri `maxBatchAgeInSecs` (minimo 1,800 e massimo 3,600) e `maxNumEventsInBatch` (minimo 1.000, massimo 10.000).

Per spiegazioni dettagliate sui parametri di aggregazione, fare riferimento al [Operazioni degli endpoint API per le destinazioni](./destination-configuration-api.md) pagina di riferimento, in cui è descritto ciascun parametro.

## Qualifiche del profilo storico {#profile-backfill}

È possibile utilizzare `backfillHistoricalProfileData` nella configurazione delle destinazioni per determinare se le qualifiche storiche del profilo devono essere esportate nella destinazione.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`: [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`: [!DNL Platform] include solo i profili utente idonei per il segmento dopo l’attivazione del segmento. </li></ul> |

{style="table-layout:auto"}

## Come questa configurazione collega tutte le informazioni necessarie per la destinazione {#connecting-all-configurations}

Alcune delle impostazioni di destinazione devono essere configurate tramite [server di destinazione](./server-and-template-configuration.md) o [configurazione dei metadati del pubblico](./audience-metadata-management.md). La configurazione di destinazione qui descritta collega tutte queste impostazioni facendo riferimento alle altre due configurazioni come segue:

* Utilizza il `destinationServerId` per fare riferimento al server di destinazione e alla configurazione del modello configurati per la destinazione.
* Utilizza il `audienceMetadataId` per fare riferimento alla configurazione dei metadati del pubblico impostata per la destinazione.