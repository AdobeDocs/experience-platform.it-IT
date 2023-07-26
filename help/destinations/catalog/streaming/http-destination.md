---
keywords: streaming; destinazione HTTP
title: Connessione API HTTP
description: Utilizza la destinazione API HTTP in Adobe Experience Platform per inviare i dati del profilo all’endpoint HTTP di terze parti per eseguire le tue analisi o eseguire qualsiasi altra operazione necessaria sui dati del profilo esportati al di fuori di Experienci Platform.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '2486'
ht-degree: 8%

---

# Connessione API HTTP

## Panoramica {#overview}

>[!IMPORTANT]
>
> Questa destinazione è disponibile solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

La destinazione API HTTP è un [!DNL Adobe Experience Platform] destinazione di streaming che consente di inviare i dati del profilo agli endpoint HTTP di terze parti.

Per inviare i dati del profilo agli endpoint HTTP, devi prima [connettersi alla destinazione](#connect-destination) in [!DNL Adobe Experience Platform].

## Casi d’uso {#use-cases}

La destinazione API HTTP consente di esportare i dati di profilo XDM e i tipi di pubblico in endpoint HTTP generici. A questo punto puoi eseguire analisi personalizzate o eseguire qualsiasi altra operazione necessaria sui dati del profilo esportati da Experienci Platform.

Gli endpoint HTTP possono essere sistemi propri del cliente o soluzioni di terze parti.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive tutti i tipi di pubblico che puoi esportare in questa destinazione.

Tutte le destinazioni supportano l’attivazione dei tipi di pubblico generati tramite l’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md).

Inoltre, questa destinazione supporta anche l’attivazione dei tipi di pubblico descritti nella tabella seguente.

| Tipo di pubblico | Descrizione |
---------|----------|
| Caricamenti personalizzati | Tipi di pubblico acquisiti in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata di mappatura del [flusso di lavoro di attivazione della destinazione](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per utilizzare la destinazione API HTTP per esportare i dati da Experienci Platform, è necessario soddisfare i seguenti prerequisiti:

* È necessario disporre di un endpoint HTTP che supporti l’API REST.
* L’endpoint HTTP deve supportare lo schema del profilo di Experience Platform. Nella destinazione API HTTP non è supportata alcuna trasformazione in uno schema di payload di terze parti. Consulta la sezione [dati esportati](#exported-data) per un esempio dello schema di output Experienci Platform.
* L&#39;endpoint HTTP deve supportare le intestazioni.

>[!TIP]
>
> Puoi anche utilizzare [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) per impostare un’integrazione e inviare i dati del profilo di Experience Platform a un endpoint HTTP.

## Indirizzo IP inserito nell&#39;elenco Consentiti {#ip-address-allowlist}

Per soddisfare i requisiti di sicurezza e conformità dei clienti, Experienci Platform fornisce un elenco di IP statici che è possibile inserire nell&#39;elenco Consentiti per la destinazione API HTTP. Fai riferimento a [ELENCO CONSENTITI di indirizzo IP per destinazioni di streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) inserire nell&#39;elenco Consentiti per l’elenco completo degli IP da.

## Tipi di autenticazione supportati {#supported-authentication-types}

La destinazione API HTTP supporta diversi tipi di autenticazione per l’endpoint HTTP:

* Endpoint HTTP senza autenticazione;
* Autenticazione token Bearer;
* [Credenziali client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticazione con il modulo del corpo, con [!DNL client ID], [!DNL client secret] e [!DNL grant type] nel corpo della richiesta HTTP, come illustrato nell’esempio seguente.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenziali client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) con autorizzazione di base, con un’intestazione di autorizzazione che contiene il codice URL [!DNL client ID] e [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Concessione password OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Connetti alla destinazione {#connect-destination}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Quando ti connetti a questa destinazione, devi fornire le seguenti informazioni:

### Informazioni di autenticazione {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo di credenziali client"
>abstract="Seleziona **Codificato nel corpo del modulo** per includere l’ID client e il segreto client nel corpo della richiesta, oppure seleziona **Autorizzazione di base** per includere l’ID client e il segreto client in un’intestazione di autorizzazione. Puoi trovare alcuni esempi nella documentazione."

#### Autenticazione token Bearer {#bearer-token-authentication}

Se si seleziona la **[!UICONTROL Token Bearer]** tipo di autenticazione per connettersi all’endpoint HTTP, inserisci i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP utilizzando l&#39;autenticazione token bearer](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Token Bearer]**: inserisci il token Bearer per l’autenticazione nella posizione HTTP.

#### Nessuna autenticazione {#no-authentication}

Se si seleziona la **[!UICONTROL Nessuno]** tipo di autenticazione per connettersi all’endpoint HTTP:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP, senza autenticazione](../../assets/catalog/http/http-api-authentication-none.png)

Quando selezioni questa autenticazione aperta, devi solo selezionare **[!UICONTROL Connetti alla destinazione]** e viene stabilita la connessione all’endpoint.

#### Autenticazione password OAuth 2 {#oauth-2-password-authentication}

Se si seleziona la **[!UICONTROL Password OAuth 2]** tipo di autenticazione per connettersi all’endpoint HTTP, inserisci i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP, utilizzando OAuth 2 con autenticazione tramite password](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL token di accesso]**: URL sul lato dell’utente che rilascia i token di accesso e, facoltativamente, aggiorna i token.
* **[!UICONTROL ID client]**: Il [!DNL client ID] che il sistema assegna a Adobe Experience Platform.
* **[!UICONTROL Segreto client]**: Il [!DNL client secret] che il sistema assegna a Adobe Experience Platform.
* **[!UICONTROL Nome utente]**: nome utente per accedere all’endpoint HTTP.
* **[!UICONTROL Password]**: password per accedere all’endpoint HTTP.

#### Autenticazione credenziali client OAuth 2 {#oauth-2-client-credentials-authentication}

Se si seleziona la **[!UICONTROL Credenziali client OAuth 2]** tipo di autenticazione per connettersi all’endpoint HTTP, inserisci i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP utilizzando OAuth 2 con autenticazione delle credenziali client](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL URL token di accesso]**: URL sul lato dell’utente che rilascia i token di accesso e, facoltativamente, aggiorna i token.
* **[!UICONTROL ID client]**: Il [!DNL client ID] che il sistema assegna a Adobe Experience Platform.
* **[!UICONTROL Segreto client]**: Il [!DNL client secret] che il sistema assegna a Adobe Experience Platform.
* **[!UICONTROL Tipo di credenziali client]**: seleziona il tipo di concessione di credenziali client OAuth2 supportata dall’endpoint:
   * **[!UICONTROL Corpo del modulo codificato]**: in questo caso, il [!DNL client ID] e [!DNL client secret] sono inclusi *nel corpo della richiesta* inviato alla tua destinazione. Ad esempio, consulta [Tipi di autenticazione supportati](#supported-authentication-types) sezione.
   * **[!UICONTROL Autorizzazione di base]**: in questo caso, il [!DNL client ID] e [!DNL client secret] sono inclusi *in un `Authorization` intestazione* dopo la codifica base64 e l&#39;invio alla destinazione. Ad esempio, consulta [Tipi di autenticazione supportati](#supported-authentication-types) sezione.

### Inserisci i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Intestazioni"
>abstract="Immetti le intestazioni personalizzate che desideri includere nelle chiamate di destinazione, nel formato seguente: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Endpoint HTTP"
>abstract="URL dell’endpoint HTTP a cui desideri inviare i dati del profilo."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Includi nomi dei segmenti"
>abstract="Attiva o disattiva questa opzione se desideri che l’esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Consulta la documentazione per vedere un esempio di esportazione dei dati con questa opzione selezionata."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Includi timestamp dei segmenti"
>abstract="Attiva o disattiva questa opzione se desideri che l’esportazione dei dati includa il timestamp UNIX al momento della creazione e dell’aggiornamento dei tipi di pubblico, nonché il timestamp UNIX al momento della mappatura dei tipi di pubblico sulla destinazione per l’attivazione. Consulta la documentazione per vedere un esempio di esportazione dei dati con questa opzione selezionata."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Parametri di query"
>abstract="Facoltativamente, puoi aggiungere dei parametri di query all’URL dell’endpoint HTTP. I parametri di query che vuoi utilizzare devono essere nel formato seguente: `parameter1=value&parameter2=value`."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Immagine della schermata dell’interfaccia utente che mostra i campi completati per i dettagli della destinazione HTTP](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nome]**: immetti un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: immetti una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Intestazioni]**: immetti le intestazioni personalizzate che desideri includere nelle chiamate di destinazione, seguendo questo formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Endpoint HTTP]**: URL dell’endpoint HTTP a cui desideri inviare i dati del profilo.
* **[!UICONTROL Parametri di query]**: facoltativamente, puoi aggiungere parametri di query all’URL dell’endpoint HTTP. I parametri di query che vuoi utilizzare devono essere nel formato seguente: `parameter1=value&parameter2=value`.
* **[!UICONTROL Includi nomi segmento]**: attiva questa opzione se desideri che l’esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Per un esempio di esportazione di dati con questa opzione selezionata, fai riferimento al [Dati esportati](#exported-data) più avanti.
* **[!UICONTROL Includi marche temporali segmento]**: attiva questa opzione se desideri che l’esportazione dei dati includa la marca temporale UNIX di quando i tipi di pubblico sono stati creati e aggiornati, nonché la marca temporale UNIX di quando i tipi di pubblico sono stati mappati sulla destinazione per l’attivazione. Per un esempio di esportazione di dati con questa opzione selezionata, fai riferimento al [Dati esportati](#exported-data) più avanti.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](../../ui/activate-streaming-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Attributi di destinazione {#attributes}

In [[!UICONTROL Seleziona attributi]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , l&#39;Adobe consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione.

## Comportamento di esportazione del profilo {#profile-export-behavior}

Experienci Platform ottimizza il comportamento di esportazione del profilo nella destinazione API HTTP per esportare i dati nell’endpoint API solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica di un pubblico o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle seguenti situazioni:

* L’aggiornamento del profilo è stato determinato da una modifica nell’appartenenza al pubblico per almeno uno dei tipi di pubblico mappati alla destinazione. Ad esempio, il profilo è idoneo per uno dei tipi di pubblico mappati sulla destinazione o è uscito da uno dei tipi di pubblico mappati sulla destinazione.
* L’aggiornamento del profilo è stato determinato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo che si era già qualificato per uno dei tipi di pubblico mappati sulla destinazione è stata aggiunta una nuova identità nell’attributo identity map.
* L’aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati sulla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti sopra, solo i profili in cui si sono verificati aggiornamenti rilevanti vengono esportati nella destinazione. Ad esempio, se un pubblico mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono idonei per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Quindi, nell’esempio precedente, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono stati modificati.

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *cosa determina un’esportazione di dati nella destinazione API HTTP* e *quali dati sono inclusi nell’esportazione*.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i tipi di pubblico mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che se un pubblico mappato cambia stato (da `null` a `realized` o da `realized` a `exiting`) o se vengono aggiornati eventuali attributi mappati, viene avviata un’esportazione di destinazione.</li><li>Poiché al momento non è possibile mappare le identità sulle destinazioni API HTTP, anche le modifiche apportate a un’identità in un determinato profilo determinano le esportazioni delle destinazioni.</li><li>Per modifica di un attributo si intende qualsiasi aggiornamento dell&#39;attributo, indipendentemente dal fatto che si tratti o meno dello stesso valore. Ciò significa che una sovrascrittura su un attributo è considerata una modifica anche se il valore stesso non è cambiato.</li></ul> | <ul><li>Il `segmentMembership` L’oggetto include il pubblico mappato nel flusso di dati di attivazione, per il quale lo stato del profilo è cambiato a seguito di un evento di qualificazione o uscita dal pubblico. Tieni presente che altri tipi di pubblico non mappati per i quali il profilo si è qualificato possono far parte dell’esportazione di destinazione, se tali tipi di pubblico appartengono allo stesso [criterio di unione](/help/profile/merge-policies/overview.md) come il pubblico mappato nel flusso di dati di attivazione. </li><li>Tutte le identità in `identityMap` L’oggetto è incluso anche (Experienci Platform attualmente non supporta la mappatura identità nella destinazione API HTTP).</li><li>Nell’esportazione della destinazione sono inclusi solo gli attributi mappati.</li></ul> |

{style="table-layout:fixed"}

Ad esempio, considera questo flusso di dati come una destinazione HTTP in cui tre tipi di pubblico vengono selezionati nel flusso di dati e quattro attributi vengono mappati sulla destinazione.

![Flusso di dati di destinazione API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo idoneo o in uscita da uno dei *tre segmenti mappati*. Tuttavia, nell’esportazione dei dati, nella `segmentMembership` oggetto (vedere [Dati esportati](#exported-data) sezione seguente), potrebbero essere visualizzati altri tipi di pubblico non mappati, se quel particolare profilo è un membro di essi e se questi condividono lo stesso criterio di unione del pubblico che ha attivato l’esportazione. Se un profilo è idoneo per **Cliente con auto DeLorean** ma è anche un membro del **Guarda &quot;Ritorno al futuro&quot;** film e **Fantascienza** segmenti, quindi anche questi altri due tipi di pubblico saranno presenti nel `segmentMembership` oggetto dell’esportazione di dati, anche se non sono mappati nel flusso di dati, se condividono lo stesso criterio di unione con **Cliente con auto DeLorean** segmento.

Dal punto di vista degli attributi di profilo, eventuali modifiche ai quattro attributi mappati in precedenza determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti nel profilo sarà presente nell’esportazione di dati.

## Recupero dati storici {#historical-data-backfill}

Quando aggiungi un nuovo pubblico a una destinazione esistente o quando crei una nuova destinazione e mappi i tipi di pubblico a essa, Experienci Platform esporta i dati storici di qualificazione del pubblico nella destinazione. Profili qualificati per il pubblico *prima di* il pubblico aggiunto alla destinazione viene esportato nella destinazione entro circa un&#39;ora.

## Dati esportati {#exported-data}

Il tuo esportato [!DNL Experience Platform] i dati vengono inseriti nel [!DNL HTTP] destinazione in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo idoneo per un determinato segmento, è membro di altri due segmenti ed è uscito da un altro segmento. L’esportazione include anche l’attributo del profilo nome, cognome, data di nascita e indirizzo e-mail personale. Le identità per questo profilo sono ECID e e-mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

Di seguito sono riportati ulteriori esempi di dati esportati, a seconda delle impostazioni dell’interfaccia utente selezionate nel flusso di destinazione della connessione per **[!UICONTROL Includi nomi segmento]** e **[!UICONTROL Includi marche temporali segmento]** opzioni:

+++ L’esempio di esportazione dei dati riportato di seguito include i nomi dei tipi di pubblico nel `segmentMembership` sezione

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ L’esempio di esportazione dei dati seguente include i timestamp del pubblico in `segmentMembership` sezione

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Limiti e criteri per nuovi tentativi {#limits-retry-policy}

Nel 95% del tempo, Experienci Platform tenta di offrire una latenza di velocità effettiva inferiore a 10 minuti per i messaggi inviati correttamente con una frequenza inferiore a 10.000 richieste al secondo per ogni flusso di dati a una destinazione HTTP.

In caso di richieste non riuscite alla destinazione API HTTP, Experienci Platform memorizza le richieste non riuscite e tenta di inviarle all’endpoint due volte.