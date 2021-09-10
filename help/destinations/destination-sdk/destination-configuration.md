---
description: Questa configurazione ti consente di indicare informazioni di base come il nome di destinazione, la categoria, la descrizione, il logo e altro ancora. Le impostazioni di questa configurazione determinano anche come gli utenti di Experience Platform si autenticano nella destinazione, come vengono visualizzati nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.
title: Opzioni di configurazione della destinazione per l’SDK di destinazione
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 5%

---

# Configurazione della destinazione {#destination-configuration}

## Panoramica {#overview}

Questa configurazione ti consente di indicare informazioni di base come il nome di destinazione, la categoria, la descrizione, il logo e altro ancora. Le impostazioni di questa configurazione determinano anche come gli utenti di Experience Platform si autenticano nella destinazione, come vengono visualizzati nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.

Puoi configurare la funzionalità descritta in questo documento utilizzando l’endpoint API `/authoring/destinations` . Leggi [Operazioni endpoint API delle destinazioni](./destination-configuration-api.md) per un elenco completo delle operazioni che puoi eseguire sull&#39;endpoint.

## Esempio di configurazione {#example-configuration}

Di seguito è riportato un esempio di configurazione per una destinazione fittizia, Moviestar, che ha endpoint in quattro posizioni nel mondo. La destinazione appartiene alla categoria delle destinazioni mobili. Le sezioni che seguono spiegano come viene costruita questa configurazione.

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
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
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
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
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
   }
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform. |
| `description` | Stringa | Immetti una descrizione che Adobe utilizzerà nel catalogo delle destinazioni Experience Platform per la tua scheda di destinazione. Mirare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizza `TEST` per configurare la destinazione per la prima volta. |

{style=&quot;table-layout:auto&quot;}

## Configurazioni di autenticazione dei clienti {#customer-authentication-configurations}

Questa sezione genera la pagina dell’account nell’interfaccia utente di Experience Platform, in cui gli utenti collegano Experience Platform agli account che hanno con la tua destinazione. A seconda dell’opzione di autenticazione indicata nel campo `authType` , la pagina di Experience Platform viene generata per gli utenti come segue:

**Autenticazione portatore**

Gli utenti devono inserire il token portatore ottenuto dalla destinazione.

![Rendering dell’interfaccia utente con autenticazione al portatore](./assets/bearer-authentication-ui.png)

**Autenticazione OAuth 2**

Gli utenti selezionano **[!UICONTROL Connetti a destinazione]** per attivare il flusso di autenticazione OAuth 2 nella destinazione.

![Rendering dell’interfaccia utente con autenticazione OAuth 2](./assets/oauth2-authentication-ui.png)


| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experience Platform nel server. Per i valori accettati, vedi `authType` di seguito. |
| `authType` | Stringa | I valori accettati sono `OAUTH2, BEARER`. <br><ul><li> Se la destinazione supporta l’autenticazione OAuth 2, seleziona il valore `OAUTH2` e aggiungi i campi richiesti per OAuth 2, come mostrato nella pagina di autenticazione dell’SDK di destinazione OAuth 2. Inoltre, devi selezionare `authenticationRule=CUSTOMER_AUTHENTICATION` nella sezione [consegna di destinazione](./destination-configuration.md). </li><li>Per l&#39;autenticazione al portatore, seleziona `BEARER` e seleziona `authenticationRule=CUSTOMER_AUTHENTICATION` nella sezione [consegna di destinazione](./destination-configuration.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Campi dati cliente {#customer-data-fields}

Questa sezione consente ai partner di introdurre campi personalizzati. Nella configurazione di esempio precedente, `customerDataFields` richiede agli utenti di selezionare un endpoint nel flusso di autenticazione e di indicare il proprio ID cliente con la destinazione. La configurazione si riflette nel flusso di autenticazione come mostrato di seguito:

![Flusso di autenticazione dei campi personalizzato](./assets/custom-field-authentication-flow.png)

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Specifica un nome per il campo personalizzato che stai introducendo. |
| `type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer`. |
| `title` | Stringa | Indica il nome del campo, come visualizzato dai clienti nell’interfaccia utente di Experience Platform. |
| `description` | Stringa | Immetti una descrizione del campo personalizzato. |
| `isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l’utente. |
| `pattern` | Stringa | Applica un pattern per il campo personalizzato, se necessario. Utilizzare espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o caratteri di sottolineatura, immetti `^[A-Za-z]+$` in questo campo. |

{style=&quot;table-layout:auto&quot;}

## Attributi dell&#39;interfaccia utente {#ui-attributes}

Questa sezione fa riferimento agli elementi dell’interfaccia utente nella configurazione precedente che l’Adobe deve utilizzare per la destinazione nell’interfaccia utente di Adobe Experience Platform. Vedi sotto:

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `documentationLink` | Stringa | Fa riferimento alla pagina della documentazione nel [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizza `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione denominata Moviestar, utilizza `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Stringa | Si riferisce alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilizzare uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Stringa | `Server-to-server` al momento è l’unica opzione disponibile. |
| `frequency` | Stringa | `Streaming` al momento è l’unica opzione disponibile. |

{style=&quot;table-layout:auto&quot;}

## Configurazione dello schema nella fase di mappatura {#schema-configuration}

![Attiva passaggio di mappatura](./assets/enable-mapping-step.png)

Utilizza i parametri in `schemaConfig` per abilitare il passaggio di mappatura del flusso di lavoro di attivazione della destinazione. Utilizzando i parametri descritti di seguito, puoi determinare se gli utenti di Experience Platform possono mappare gli attributi e/o le identità dello schema desiderato sul lato della destinazione.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `profileFields` | Array | *Non mostrato nella configurazione di esempio precedente.* Quando si aggiungono attributi predefiniti  `profileFields`, gli utenti potranno scegliere di mappare gli attributi Experienci Platform agli attributi predefiniti sul lato della destinazione. |
| `profileRequired` | Booleano | Utilizza `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sul lato della destinazione, come mostrato nell’esempio di configurazione precedente. |
| `segmentRequired` | Booleano | Utilizza sempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilizza `true` se gli utenti devono essere in grado di mappare i namespace di identità dall’Experience Platform allo schema desiderato. |

{style=&quot;table-layout:auto&quot;}

## Identità e attributi {#identities-and-attributes}

I parametri in questa sezione determinano come le identità e gli attributi di destinazione vengono compilati nel passaggio di mappatura dell’interfaccia utente di Experience Platform, dove gli utenti mappano i loro schemi XDM sullo schema nella destinazione.

Adobe deve sapere quali [!DNL Platform] identità i clienti saranno in grado di esportare nella tua destinazione. Alcuni esempi sono [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono spazi dei nomi di identità [!DNL Platform] che i clienti possono mappare ai namespace di identità dalla destinazione.

Gli spazi dei nomi di identità non richiedono una corrispondenza da 1 a 1 tra [!DNL Platform] e la destinazione.
Ad esempio, i clienti possono mappare uno spazio dei nomi [!DNL Platform] [!DNL IDFA] a uno spazio dei nomi [!DNL IDFA] dalla destinazione oppure mappare lo stesso spazio dei nomi [!DNL Platform] [!DNL IDFA] a uno spazio dei nomi [!DNL Customer ID] nella destinazione.

Per ulteriori informazioni, consulta [Panoramica spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it).

![Eseguire il rendering delle identità di destinazione nell’interfaccia utente](./assets/target-identities-ui.png)

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `acceptsAttributes` | Booleano | Indica se la destinazione accetta attributi di profilo standard. Di solito, questi attributi sono evidenziati nella documentazione dei nostri partner. |
| `acceptsCustomNamespaces` | Booleano | Indica se i clienti possono impostare spazi dei nomi personalizzati nella destinazione. |
| `allowedAttributesTransformation` | Stringa | *Non mostrato nella configurazione* di esempio. Utilizzato, ad esempio, quando il cliente [!DNL Platform] ha indirizzi e-mail semplici come attributo e la piattaforma accetta solo e-mail con hash. Qui puoi fornire la trasformazione da applicare (ad esempio, trasforma l’e-mail in minuscolo e quindi hash). |
| `acceptedGlobalNamespaces` | - | *Non mostrato nella configurazione* di esempio. Utilizzato per i casi in cui la piattaforma accetta [spazi dei nomi di identità standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (ad esempio, IDFA), in modo da limitare gli utenti Platform alla selezione solo di questi spazi dei nomi di identità. |

{style=&quot;table-layout:auto&quot;}

## Consegna delle destinazioni {#destination-delivery}

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authenticationRule` | Stringa | Indica il modo in cui i clienti [!DNL Platform] si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizza `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al tuo sistema tramite un nome utente e una password, un token portatore o un altro metodo di autenticazione. Ad esempio, puoi selezionare questa opzione se hai selezionato anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizza `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando la configurazione [Credentials](./credentials-configuration.md). </li><li>Utilizza `NONE` se non è necessaria alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationServerId` | Stringa | La `instanceId` della [configurazione del server di destinazione](./destination-server-api.md) utilizzata per questa destinazione. |
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`:  [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`:  [!DNL Platform] include solo i profili utente qualificati per il segmento dopo l’attivazione del segmento. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Configurazione della mappatura dei segmenti {#segment-mapping}

![Sezione di configurazione della mappatura dei segmenti](./assets/segment-mapping-configuration.png)

Questa sezione della configurazione di destinazione si riferisce al modo in cui i metadati del segmento come i nomi dei segmenti o gli ID devono essere condivisi tra l’Experience Platform e la destinazione.

Attraverso `audienceTemplateId`, questa sezione collega anche questa configurazione con la [configurazione dei metadati del pubblico](./audience-metadata-management.md).

I parametri mostrati nella configurazione di cui sopra sono descritti nel [riferimento API dell&#39;endpoint di destinazione](./destination-configuration-api.md).

## Criteri di aggregazione {#aggregation}

![Criteri di aggregazione nel modello di configurazione](./assets/aggregation-configuration.png)

Questa sezione ti consente di impostare i criteri di aggregazione che Experience Platform utilizzerà per esportare i dati nella destinazione.

Un criterio di aggregazione determina il modo in cui i profili esportati vengono combinati insieme nelle esportazioni di dati. Le opzioni disponibili sono:
* Aggregazione degli sforzi migliori
* Aggregazione configurabile (mostrata nella configurazione precedente)

### Aggregazione degli sforzi migliori {#best-effort-aggregation}

>[!TIP]
>
>Utilizza questa opzione se l’endpoint API accetta meno di 100 profili per chiamata API.

Questa opzione funziona meglio per le destinazioni che preferiscono meno profili per richiesta e preferiscono più richieste con meno dati che meno richieste con più dati.

Utilizza il parametro `maxUsersPerRequest` per specificare il numero massimo di profili che la destinazione può assumere in una richiesta.

### Aggregazione configurabile {#configurable-aggregation}

Questa opzione funziona meglio se preferisci prendere batch di grandi dimensioni, con migliaia di profili sulla stessa chiamata. Questa opzione ti consente inoltre di aggregare i profili esportati in base a regole di aggregazione complesse.

Questa opzione consente di:
* Imposta il tempo massimo e il numero di profili da aggregare prima che venga effettuata una chiamata API alla destinazione.
* Aggrega i profili esportati mappati alla destinazione in base a:
   * ID segmento
   * stato del segmento
   * identità o gruppi di identità

Per spiegazioni dettagliate sui parametri di aggregazione, fai riferimento alla pagina di riferimento [Operazioni endpoint API delle destinazioni](./destination-configuration-api.md) , in cui è descritto ogni parametro.

<!--

commenting out the `backfillHistoricalProfileData` parameter, which will only be used after an April release

|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

-->
