---
keywords: streaming; destinazione HTTP
title: Connessione API HTTP
description: Utilizza la destinazione API HTTP in Adobe Experience Platform per inviare i dati del profilo all’endpoint HTTP di terze parti per eseguire le tue analisi o eseguire qualsiasi altra operazione necessaria sui dati del profilo esportati al di fuori di Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: fffeb2221c4e25bae8386419de1646c89aa93a06
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 8%

---

# Connessione API HTTP

## Panoramica {#overview}

>[!IMPORTANT]
>
> Questa destinazione è disponibile solo per [clienti Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html).

La destinazione API HTTP è una destinazione di streaming [!DNL Adobe Experience Platform] che consente di inviare i dati del profilo agli endpoint HTTP di terze parti.

Per inviare i dati del profilo agli endpoint HTTP, devi prima [connetterti alla destinazione](#connect-destination) in [!DNL Adobe Experience Platform].

## Casi d’uso {#use-cases}

La destinazione API HTTP consente di esportare i dati di profilo XDM e i tipi di pubblico in endpoint HTTP generici. A questo punto puoi eseguire analisi personalizzate o eseguire qualsiasi altra operazione necessaria sui dati del profilo esportati da Experience Platform.

Gli endpoint HTTP possono essere sistemi propri del cliente o soluzioni di terze parti.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata di mappatura del [flusso di lavoro di attivazione della destinazione](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per utilizzare la destinazione API HTTP per esportare dati da Experience Platform, è necessario soddisfare i seguenti prerequisiti:

* È necessario disporre di un endpoint HTTP che supporti l’API REST.
* L’endpoint HTTP deve supportare lo schema del profilo di Experience Platform. Nella destinazione API HTTP non è supportata alcuna trasformazione in uno schema di payload di terze parti. Consulta la sezione [dati esportati](#exported-data) per un esempio dello schema di output Experience Platform.
* L&#39;endpoint HTTP deve supportare le intestazioni.

>[!TIP]
>
> È inoltre possibile utilizzare [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) per impostare un&#39;integrazione e inviare i dati del profilo di Experience Platform a un endpoint HTTP.

## Supporto e certificato del protocollo mTLS {#mtls-protocol-support}

È possibile utilizzare [!DNL Mutual Transport Layer Security] ([!DNL mTLS]) per garantire una maggiore sicurezza nelle connessioni in uscita alle connessioni di destinazione API HTTP.

[!DNL mTLS] è un metodo di sicurezza end-to-end per l&#39;autenticazione reciproca che garantisce che entrambe le parti che condividono le informazioni siano quelle che dichiarano di essere prima che i dati vengano condivisi. [!DNL mTLS] include un passaggio aggiuntivo rispetto a [!DNL TLS], in cui il server richiede anche il certificato del client e lo verifica alla fine.

Se si desidera utilizzare [!DNL mTLS] con [!DNL HTTP API] destinazioni, l&#39;indirizzo del server inserito nella pagina [dettagli destinazione](#destination-details) deve avere [!DNL TLS] protocolli disabilitati e solo [!DNL mTLS] abilitati. Se il protocollo [!DNL TLS] 1.2 è ancora abilitato sull&#39;endpoint, non verrà inviato alcun certificato per l&#39;autenticazione client. Ciò significa che per utilizzare [!DNL mTLS] con la destinazione [!DNL HTTP API], l&#39;endpoint del server &quot;ricevente&quot; deve essere un endpoint di connessione abilitato solo per [!DNL mTLS].

### Scarica certificato {#certificate}

Se si desidera verificare che [!DNL Common Name] (CN) e [!DNL Subject Alternative Names] (SAN) eseguano un&#39;ulteriore convalida di terze parti, è possibile scaricare il certificato seguente:

* [Certificato pubblico mTLS API HTTP](../../../landing/images/governance-privacy-security/encryption/destinations-public-certificate.zip)

Puoi anche recuperare in modo sicuro i certificati pubblici effettuando una richiesta GET all’endpoint MTLS. Per ulteriori informazioni, consulta la [documentazione dell&#39;endpoint del certificato pubblico](../../../data-governance/mtls-api/public-certificate-endpoint.md).

## Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allowlist}

Per soddisfare i requisiti di sicurezza e conformità dei clienti, Experience Platform inserire nell&#39;elenco Consentiti fornisce un elenco di IP statici che puoi per la destinazione API HTTP. Per l&#39;elenco completo degli indirizzi IP da inserire nell&#39;elenco Consentiti, consulta il inserisco nell&#39;elenco Consentiti di [degli indirizzi IP per le destinazioni di streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md).

## Tipi di autenticazione supportati {#supported-authentication-types}

La destinazione API HTTP supporta diversi tipi di autenticazione per l’endpoint HTTP:

* Endpoint HTTP senza autenticazione;
* Autenticazione token Bearer;
* Autenticazione di [credenziali client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) con il form del corpo, con [!DNL client ID], [!DNL client secret] e [!DNL grant type] nel corpo della richiesta HTTP, come illustrato nell&#39;esempio seguente.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenziali client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) con autorizzazione di base, con un&#39;intestazione di autorizzazione che contiene [!DNL client ID] e [!DNL client secret] codificati in URL.

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Concessione password OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Connettersi alla destinazione {#connect-destination}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Quando ti connetti a questa destinazione, devi fornire le seguenti informazioni:

### Informazioni di autenticazione {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo di credenziali client"
>abstract="Seleziona **Codificato nel corpo del modulo** per includere l’ID client e il segreto client nel corpo della richiesta, oppure seleziona **Autorizzazione di base** per includere l’ID client e il segreto client in un’intestazione di autorizzazione. Puoi trovare alcuni esempi nella documentazione."

#### Autenticazione token Bearer {#bearer-token-authentication}

Se si seleziona il tipo di autenticazione **[!UICONTROL Token Bearer]** per connettersi all&#39;endpoint HTTP, immettere i campi seguenti e selezionare **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP utilizzando l&#39;autenticazione token bearer.](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Token Bearer]**: inserisci il token Bearer per l&#39;autenticazione nel percorso HTTP.

#### Nessuna autenticazione {#no-authentication}

Se si seleziona il tipo di autenticazione **[!UICONTROL None]** per connettersi all&#39;endpoint HTTP:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP, senza autenticazione.](../../assets/catalog/http/http-api-authentication-none.png)

Quando selezioni questa autenticazione aperta, devi solo selezionare **[!UICONTROL Connetti alla destinazione]** e la connessione all&#39;endpoint è stata stabilita.

#### Autenticazione password OAuth 2 {#oauth-2-password-authentication}

Se si seleziona il tipo di autenticazione **[!UICONTROL Password OAuth 2]** per connettersi all&#39;endpoint HTTP, immettere i campi seguenti e selezionare **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP utilizzando OAuth 2 con autenticazione tramite password.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL token di accesso]**: l&#39;URL sul lato dell&#39;utente che rilascia i token di accesso e, facoltativamente, aggiorna i token.
* **[!UICONTROL ID client]**: [!DNL client ID] assegnato dal sistema a Adobe Experience Platform.
* **[!UICONTROL Segreto client]**: [!DNL client secret] assegnato dal sistema a Adobe Experience Platform.
* **[!UICONTROL Nome utente]**: il nome utente per accedere all&#39;endpoint HTTP.
* **[!UICONTROL Password]**: password per accedere all&#39;endpoint HTTP.

#### Autenticazione credenziali client OAuth 2 {#oauth-2-client-credentials-authentication}

Se si seleziona il tipo di autenticazione **[!UICONTROL Credenziali client OAuth 2]** per connettersi all&#39;endpoint HTTP, immettere i campi seguenti e selezionare **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione API HTTP utilizzando OAuth 2 con autenticazione delle credenziali client.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL URL token di accesso]**: l&#39;URL sul lato dell&#39;utente che rilascia i token di accesso e, facoltativamente, aggiorna i token.
* **[!UICONTROL ID client]**: [!DNL client ID] assegnato dal sistema a Adobe Experience Platform.
* **[!UICONTROL Segreto client]**: [!DNL client secret] assegnato dal sistema a Adobe Experience Platform.
* **[!UICONTROL Tipo di credenziali client]**: selezionare il tipo di concessione credenziali client OAuth2 supportata dall&#39;endpoint:
   * **[!UICONTROL Corpo del modulo codificato]**: in questo caso, [!DNL client ID] e [!DNL client secret] sono inclusi *nel corpo della richiesta* inviata alla tua destinazione. Ad esempio, consulta la sezione [Tipi di autenticazione supportati](#supported-authentication-types).
   * **[!UICONTROL Autorizzazione di base]**: in questo caso, [!DNL client ID] e [!DNL client secret] sono inclusi *in un&#39;intestazione `Authorization`* dopo essere stati codificati in base64 e inviati alla destinazione. Ad esempio, consulta la sezione [Tipi di autenticazione supportati](#supported-authentication-types).

### Inserire i dettagli della destinazione {#destination-details}

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

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli della destinazione HTTP.](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nome]**: immetti un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: immetti una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Intestazioni]**: immettere le intestazioni personalizzate che si desidera includere nelle chiamate di destinazione, nel seguente formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Endpoint HTTP]**: URL dell&#39;endpoint HTTP a cui si desidera inviare i dati del profilo.
* **[!UICONTROL Parametri query]**: facoltativamente, è possibile aggiungere parametri di query all&#39;URL dell&#39;endpoint HTTP. I parametri di query che vuoi utilizzare devono essere nel formato seguente: `parameter1=value&parameter2=value`.
* **[!UICONTROL Includi nomi segmento]**: attiva questa opzione se vuoi che l&#39;esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Per un esempio di esportazione di dati con questa opzione selezionata, consulta la sezione [Dati esportati](#exported-data) più avanti.
* **[!UICONTROL Includi marche temporali segmento]**: attiva questa opzione se desideri che l&#39;esportazione dei dati includa la marca temporale UNIX di quando i tipi di pubblico sono stati creati e aggiornati, nonché la marca temporale UNIX di quando i tipi di pubblico sono stati mappati alla destinazione per l&#39;attivazione. Per un esempio di esportazione di dati con questa opzione selezionata, consulta la sezione [Dati esportati](#exported-data) più avanti.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* [La valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) non è attualmente supportata nelle esportazioni nella destinazione API HTTP. [Ulteriori informazioni](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione del profilo di streaming](../../ui/activate-streaming-profile-destinations.md).

### Attributi di destinazione {#attributes}

Nel passaggio [[!UICONTROL Seleziona attributi]](../../ui/activate-streaming-profile-destinations.md#select-attributes), l&#39;Adobe consiglia di selezionare un identificatore univoco dallo [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione.

## Comportamento di esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione API HTTP per esportare i dati nell’endpoint API solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica di un pubblico o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle seguenti situazioni:

* L’aggiornamento del profilo è stato determinato da una modifica nell’appartenenza al pubblico per almeno uno dei tipi di pubblico mappati alla destinazione. Ad esempio, il profilo è idoneo per uno dei tipi di pubblico mappati sulla destinazione o è uscito da uno dei tipi di pubblico mappati sulla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo che si era già qualificato per uno dei tipi di pubblico mappati sulla destinazione è stata aggiunta una nuova identità nell’attributo identity map.
* L’aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati sulla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti sopra, solo i profili in cui si sono verificati aggiornamenti rilevanti vengono esportati nella destinazione. Ad esempio, se un pubblico mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono idonei per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Quindi, nell’esempio precedente, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono stati modificati.

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *che determinano un&#39;esportazione di dati nella destinazione API HTTP* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i tipi di pubblico mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che se uno dei tipi di pubblico mappati cambia stato (da `null` a `realized` o da `realized` a `exiting`) o se uno qualsiasi degli attributi mappati viene aggiornato, viene avviata un&#39;esportazione di destinazione.</li><li>Poiché al momento non è possibile mappare le identità sulle destinazioni API HTTP, anche le modifiche apportate a un’identità in un determinato profilo determinano le esportazioni delle destinazioni.</li><li>Per modifica di un attributo si intende qualsiasi aggiornamento dell&#39;attributo, indipendentemente dal fatto che si tratti o meno dello stesso valore. Ciò significa che una sovrascrittura su un attributo è considerata una modifica anche se il valore stesso non è cambiato.</li></ul> | <ul><li>L&#39;oggetto `segmentMembership` include il pubblico mappato nel flusso di dati di attivazione, per il quale lo stato del profilo è cambiato a seguito di un evento di qualificazione o uscita dal pubblico. Tieni presente che altri tipi di pubblico non mappati per i quali il profilo si è qualificato possono far parte dell&#39;esportazione di destinazione, se tali tipi di pubblico appartengono allo stesso [criterio di unione](/help/profile/merge-policies/overview.md) del pubblico mappato nel flusso di dati di attivazione. </li><li>Sono incluse anche tutte le identità nell&#39;oggetto `identityMap` (l&#39;Experience Platform attualmente non supporta la mappatura delle identità nella destinazione API HTTP).</li><li>Nell’esportazione della destinazione sono inclusi solo gli attributi mappati.</li></ul> |

{style="table-layout:fixed"}

Ad esempio, considera questo flusso di dati come una destinazione HTTP in cui tre tipi di pubblico vengono selezionati nel flusso di dati e quattro attributi vengono mappati sulla destinazione.

![Esempio di flusso di dati di destinazione API HTTP.](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un&#39;esportazione di profilo nella destinazione può essere determinata da un profilo idoneo o in uscita da uno dei *tre segmenti mappati*. Tuttavia, nell&#39;esportazione dei dati, nell&#39;oggetto `segmentMembership` (vedi la sezione [Dati esportati](#exported-data) di seguito), potrebbero essere visualizzati altri tipi di pubblico non mappati, se quel particolare profilo è un membro di essi e se questi condividono lo stesso criterio di unione del pubblico che ha attivato l&#39;esportazione. Se un profilo è idoneo per il segmento **Cliente con auto DeLorean** ma è anche membro dei segmenti **Guardato &quot;Ritorno al futuro&quot;** filmato e **Fantascienza**, anche questi altri due tipi di pubblico saranno presenti nell&#39;oggetto `segmentMembership` dell&#39;esportazione dati, anche se non sono mappati nel flusso di dati, se condividono lo stesso criterio di unione con il segmento **Cliente con auto DeLorean**.

Dal punto di vista degli attributi di profilo, eventuali modifiche ai quattro attributi mappati in precedenza determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti nel profilo sarà presente nell’esportazione di dati.

## Recupero dati storici {#historical-data-backfill}

Quando aggiungi un nuovo pubblico a una destinazione esistente o quando crei una nuova destinazione e mappi i tipi di pubblico a essa, Experience Platform esporta i dati storici di qualificazione del pubblico nella destinazione. I profili qualificati per il pubblico *prima* che il pubblico sia stato aggiunto alla destinazione vengono esportati nella destinazione entro circa un&#39;ora.

## Dati esportati {#exported-data}

I dati di [!DNL Experience Platform] esportati arrivano nella destinazione di [!DNL HTTP] in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo idoneo per un determinato segmento, è membro di altri due segmenti ed è uscito da un altro segmento. L’esportazione include anche l’attributo del profilo nome, cognome, data di nascita e indirizzo e-mail personale. Le identità per questo profilo sono ECID e e-mail.

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

Di seguito sono riportati ulteriori esempi di dati esportati, a seconda delle impostazioni dell&#39;interfaccia utente selezionate nel flusso di destinazione di connessione per le opzioni **[!UICONTROL Includi nomi segmento]** e **[!UICONTROL Includi marche temporali segmento]**:

+++ L&#39;esempio di esportazione dei dati seguente include i nomi del pubblico nella sezione `segmentMembership`

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

+++ L&#39;esempio di esportazione dei dati seguente include i timestamp del pubblico nella sezione `segmentMembership`

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

Nel 95% del tempo, Experience Platform tenta di offrire una latenza di velocità effettiva inferiore a 10 minuti per i messaggi inviati correttamente con una frequenza inferiore a 10.000 richieste al secondo per ogni flusso di dati a una destinazione HTTP.

In caso di richieste non riuscite alla destinazione API HTTP, Experience Platform memorizza le richieste non riuscite e tenta di inviarle all’endpoint due volte.