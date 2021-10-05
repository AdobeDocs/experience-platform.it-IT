---
description: Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando l'endpoint API `/authoring/destinations`.
title: Operazioni degli endpoint API delle destinazioni
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 32b61276f3fe81ffa82fec1debf335ea51020ccd
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 5%

---

# Operazioni API per gli endpoint delle destinazioni {#destination-configuration}

>[!IMPORTANT]
>
>**Endpoint** API:  `platform.adobe.io/data/core/activation/authoring/destinations`

In questa pagina sono elencate e descritte tutte le operazioni API che puoi eseguire utilizzando l’endpoint API `/authoring/destinations`. Per una descrizione delle funzionalità supportate da questo endpoint, leggere [configurazione di destinazione](./destination-configuration.md).

## Guida introduttiva alle operazioni API di destinazione {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare una configurazione per una destinazione {#create}

Puoi creare una nuova configurazione di destinazione effettuando una richiesta POST all’endpoint `/authoring/destinations` .

**Formato API**


```http
POST /authoring/destinations
```

**Richiesta**

La richiesta seguente crea una nuova configurazione di destinazione, configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dall’endpoint `/authoring/destinations`. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "name":"endpointsInstance",
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
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
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
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform |
| `description` | Stringa | Immetti una descrizione che Adobe utilizzerà nel catalogo delle destinazioni Experience Platform per la tua scheda di destinazione. Mirare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizza `TEST` per configurare la destinazione per la prima volta. |
| `customerAuthenticationConfigurations` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experience Platform nel server. Per i valori accettati, vedi `authType` di seguito. |
| `customerAuthenticationConfigurations.authType` | Stringa | I valori accettati sono `OAUTH2, BEARER`. |
| `customerDataFields.name` | Stringa | Specifica un nome per il campo personalizzato che stai introducendo. |
| `customerDataFields.type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer` |
| `customerDataFields.title` | Stringa | Indica il nome del campo, come visualizzato dai clienti nell’interfaccia utente di Experience Platform |
| `customerDataFields.description` | Stringa | Immetti una descrizione del campo personalizzato. |
| `customerDataFields.isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `customerDataFields.enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l’utente. |
| `customerDataFields.pattern` | Stringa | Applica un pattern per il campo personalizzato, se necessario. Utilizzare espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o caratteri di sottolineatura, immetti `^[A-Za-z]+$` in questo campo. |
| `uiAttributes.documentationLink` | Stringa | Fa riferimento alla pagina della documentazione nel [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizza `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione denominata Moviestar, utilizzare `https://www.adobe.com/go/destinations-moviestar-en`. |
| `uiAttributes.category` | Stringa | Si riferisce alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilizzare uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Stringa | `Server-to-server` al momento è l’unica opzione disponibile. |
| `uiAttributes.frequency` | Stringa | `Streaming` al momento è l’unica opzione disponibile. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se la destinazione accetta attributi di profilo standard. Di solito, questi attributi sono evidenziati nella documentazione dei nostri partner. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se i clienti possono impostare spazi dei nomi personalizzati nella destinazione. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Stringa | _Non mostrato nella configurazione_ di esempio. Utilizzato, ad esempio, quando il cliente [!DNL Platform] ha indirizzi e-mail semplici come attributo e la piattaforma accetta solo e-mail con hash. Qui puoi fornire la trasformazione da applicare (ad esempio, trasforma l’e-mail in minuscolo e quindi hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Utilizzato per i casi in cui la piattaforma accetta [spazi dei nomi di identità standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (ad esempio, IDFA), in modo da limitare gli utenti Platform alla selezione solo di questi spazi dei nomi di identità. <br> Quando utilizzi  `acceptedGlobalNamespaces`, puoi utilizzare  `"requiredTransformation":"sha256(lower($))"` per utilizzare lettere minuscole e indirizzi e-mail o numeri di telefono. |
| `destinationDelivery.authenticationRule` | Stringa | Indica il modo in cui i clienti [!DNL Platform] si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizza `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al tuo sistema tramite un nome utente e una password, un token portatore o un altro metodo di autenticazione. Ad esempio, puoi selezionare questa opzione se hai selezionato anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizza `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando la configurazione [Credentials](./credentials-configuration.md). </li><li>Utilizza `NONE` se non è necessaria alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationDelivery.destinationServerId` | Stringa | Il `instanceId` del [modello del server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`:  [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`:  [!DNL Platform] include solo i profili utente qualificati per il segmento dopo l’attivazione del segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione viene immesso dall&#39;utente. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è l&#39;ID del segmento di Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è il nome del segmento di Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | Il `instanceId` del [modello di metadati del pubblico](./audience-metadata-api.md) utilizzato per questa destinazione. |
| `schemaConfig.profileFields` | Array | Quando aggiungi gli attributi predefiniti `profileFields` come mostrato nella configurazione precedente, gli utenti avranno la possibilità di mappare gli attributi Experienci Platform agli attributi predefiniti sul lato della destinazione. |
| `schemaConfig.profileRequired` | Booleano | Utilizza `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sul lato della destinazione, come mostrato nell’esempio di configurazione precedente. |
| `schemaConfig.segmentRequired` | Booleano | Utilizza sempre `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Utilizza `true` se gli utenti devono essere in grado di mappare i namespace di identità dall’Experience Platform allo schema desiderato. |
| `aggregation.aggregationType` | - | Seleziona `BEST_EFFORT` o `CONFIGURABLE_AGGREGATION`. Anche se la configurazione di esempio precedente include entrambi i tipi di aggregazione, è necessario selezionarne solo uno per la destinazione. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Intero | Experience Platform può aggregare più profili esportati in una singola chiamata HTTP. Specifica il numero massimo di profili che l&#39;endpoint deve ricevere in una singola chiamata HTTP. Tieni presente che si tratta di un’aggregazione dello sforzo migliore. Ad esempio, se specifichi il valore 100, Platform potrebbe inviare un numero qualsiasi di profili inferiore a 100 in una chiamata . <br> Se il server non accetta più utenti per richiesta, imposta questo valore su 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Booleano | Usa questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per un determinato namespace. |
| `aggregation.configurableAggregation.splitUserById` | Booleano | Usa questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per un determinato namespace. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Intero | *Valore massimo: 3600*. Insieme a `maxNumEventsInBatch`, questo determina per quanto tempo Experience Platform deve attendere fino a quando non invia una chiamata API all’endpoint. <br> Ad esempio, se utilizzi il valore massimo per entrambi i parametri, Experience Platform attenderà 3600 secondi OR fino a quando non saranno disponibili 10.000 profili qualificati prima di effettuare la chiamata API, a seconda di quale dei due eventi si verifica per primo. |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Intero | *Valore massimo: 10000*. Vedi `maxBatchAgeInSecs` qui sopra. |
| `aggregation.configurableAggregation.aggregationKey` | Booleano | Consente di aggregare i profili esportati mappati alla destinazione in base ai parametri seguenti: <br> <ul><li>ID segmento</li><li> stato del segmento </li><li> spazio dei nomi identità </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Imposta questo valore su `true` se desideri raggruppare i profili esportati nella destinazione per ID segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | È necessario impostare sia `includeSegmentId:true` che `includeSegmentStatus:true` se si desidera raggruppare i profili esportati nella destinazione in base allo stato dell’ID segmento E. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Booleano | Imposta questo valore su `true` se desideri raggruppare i profili esportati nella destinazione per namespace di identità. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Usa questo parametro per specificare se desideri che i profili esportati siano aggregati in gruppi di una singola identità (GAID, IDFA, numeri di telefono, e-mail, ecc.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Stringa | Crea elenchi di gruppi di identità se desideri raggruppare i profili esportati nella destinazione per gruppi di namespace di identità. Ad esempio, puoi combinare profili che contengono gli identificatori mobili IDFA e GAID in una chiamata alla tua destinazione ed e-mail in un&#39;altra utilizzando la configurazione nell&#39;esempio. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione di destinazione appena creata.

## Elenca configurazioni di destinazione {#retrieve-list}

Puoi recuperare un elenco di tutte le configurazioni di destinazione per la tua organizzazione IMS effettuando una richiesta di GET all’ endpoint `/authoring/destinations` .

**Formato API**


```http
GET /authoring/destinations
```

**Richiesta**

La richiesta seguente recupererà l’elenco delle configurazioni di destinazione a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di configurazioni di destinazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Un `instanceId` corrisponde al modello per una destinazione. La risposta viene troncata per brevità.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "name":"endpointsInstance",
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
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
         "segmentMappingConfig":{
            "mapExperiencePlatformSegmentName":false,
            "mapExperiencePlatformSegmentId":false,
            "mapUserInput":false,
            "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
         },
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "aggregation":{
            "aggregationType":"CONFIGURABLE_AGGREGATION",
            "configurableAggregation":{
               "splitUserById":true,
               "maxBatchAgeInSecs":0,
               "maxNumEventsInBatch":0,
               "aggregationKey":{
                  "includeSegmentId":true,
                  "includeSegmentStatus":true,
                  "includeIdentity":true,
                  "oneIdentityPerGroup":false,
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
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform. |
| `description` | Stringa | Immetti una descrizione che Adobe utilizzerà nel catalogo delle destinazioni Experience Platform per la tua scheda di destinazione. Mirare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizza `TEST` per configurare la destinazione per la prima volta. |
| `customerAuthenticationConfigurations` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experience Platform nel server. Per i valori accettati, vedi `authType` di seguito. |
| `customerAuthenticationConfigurations.authType` | Stringa | I valori accettati sono `OAUTH2, BEARER`. |
| `customerDataFields.name` | Stringa | Specifica un nome per il campo personalizzato che stai introducendo. |
| `customerDataFields.type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer` |
| `customerDataFields.title` | Stringa | Indica il nome del campo, come visualizzato dai clienti nell’interfaccia utente di Experience Platform |
| `customerDataFields.description` | Stringa | Immetti una descrizione del campo personalizzato. |
| `customerDataFields.isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `customerDataFields.enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l’utente. |
| `customerDataFields.pattern` | Stringa | Applica un pattern per il campo personalizzato, se necessario. Utilizzare espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o caratteri di sottolineatura, immetti `^[A-Za-z]+$` in questo campo. |
| `uiAttributes.documentationLink` | Stringa | Fa riferimento alla pagina della documentazione nel [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizza `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione denominata Moviestar, utilizza `https://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | Stringa | Si riferisce alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilizzare uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Stringa | `Server-to-server` al momento è l’unica opzione disponibile. |
| `uiAttributes.frequency` | Stringa | `Streaming` al momento è l’unica opzione disponibile. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se la destinazione accetta attributi di profilo standard. Di solito, questi attributi sono evidenziati nella documentazione dei nostri partner. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se i clienti possono impostare spazi dei nomi personalizzati nella destinazione. Ulteriori informazioni su [spazi dei nomi personalizzati](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) in Adobe Experience Platform. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Stringa | _Non mostrato nella configurazione_ di esempio. Utilizzato, ad esempio, quando il cliente [!DNL Platform] ha indirizzi e-mail semplici come attributo e la piattaforma accetta solo e-mail con hash. Qui puoi fornire la trasformazione da applicare (ad esempio, trasforma l’e-mail in minuscolo e quindi hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Utilizzato per i casi in cui la piattaforma accetta [spazi dei nomi di identità standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (ad esempio, IDFA), in modo da limitare gli utenti Platform alla selezione solo di questi spazi dei nomi di identità. |
| `destinationDelivery.authenticationRule` | Stringa | Indica il modo in cui i clienti [!DNL Platform] si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizza `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al tuo sistema tramite un nome utente e una password, un token portatore o un altro metodo di autenticazione. Ad esempio, puoi selezionare questa opzione se hai selezionato anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizza `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando la configurazione [Credentials](./credentials-configuration.md). </li><li>Utilizza `NONE` se non è necessaria alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationDelivery.destinationServerId` | Stringa | Il `instanceId` del [modello del server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |
| `destConfigId` | Stringa | Questo campo viene generato automaticamente e non richiede l’input. |
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`:  [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`:  [!DNL Platform] include solo i profili utente qualificati per il segmento dopo l’attivazione del segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione viene immesso dall&#39;utente. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è l&#39;ID del segmento di Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è il nome del segmento di Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | Il `instanceId` del [modello di metadati del pubblico](./audience-metadata-management.md) utilizzato per questa destinazione. Per impostare un modello di metadati del pubblico, leggi [riferimento API per i metadati del pubblico](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Aggiornare una configurazione di destinazione esistente {#update}

È possibile aggiornare una configurazione di destinazione esistente effettuando una richiesta di PUT all&#39;endpoint `/authoring/destinations` e fornendo l&#39;ID di istanza della configurazione di destinazione che si desidera aggiornare. Nel corpo della chiamata , fornisci la configurazione di destinazione aggiornata.

**Formato API**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione di destinazione da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna una configurazione di destinazione esistente, configurata dai parametri forniti nel payload. Nell’esempio di chiamata riportato di seguito, stiamo aggiornando la configurazione [creata in precedenza](./destination-configuration-api.md#create) per accettare ora identificatori GAID, IDFA e e-mail con hash come spazi dei nomi di identità.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "name":"endpointsInstance",
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
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
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
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Recupera una configurazione di destinazione specifica {#get}

Puoi recuperare informazioni dettagliate su una configurazione di destinazione specifica effettuando una richiesta di GET all’ endpoint `/authoring/destinations` e fornendo l’ID di istanza della configurazione di destinazione che desideri recuperare.

**Formato API**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione di destinazione da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla configurazione di destinazione specificata.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "name":"endpointsInstance",
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
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
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
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Eliminare una configurazione di destinazione specifica {#delete}

Puoi eliminare la configurazione di destinazione specificata effettuando una richiesta DELETE all’ endpoint `/authoring/destinations` e fornendo l’ID della configurazione di destinazione che desideri eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `id` della configurazione di destinazione che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API SDK di destinazione seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [richiedi errori di intestazione](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come configurare la destinazione utilizzando l’endpoint API `/authoring/destinations`. Leggi [come utilizzare l&#39;SDK di destinazione per configurare la destinazione](./configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
