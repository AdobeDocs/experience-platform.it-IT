---
title: Connessione API HTTP (Beta)
keywords: streaming;
description: La destinazione API HTTP in Adobe Experience Platform ti consente di inviare dati di profilo a endpoint HTTP di terze parti.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 0d58445557490a5539279f55c34183994429c632
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Connessione API HTTP (Beta)

>[!IMPORTANT]
>
>La destinazione API HTTP in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La destinazione API HTTP è un [!DNL Adobe Experience Platform] destinazione di streaming che consente di inviare dati di profilo a endpoint HTTP di terze parti.

Per inviare i dati di profilo agli endpoint HTTP, devi prima [connettersi alla destinazione](#connect-destination) in [!DNL Adobe Experience Platform].

## Casi d’uso {#use-cases}

La destinazione HTTP è indirizzata ai clienti che devono esportare i dati di profilo XDM e i segmenti di pubblico in endpoint HTTP generici.

Gli endpoint HTTP possono essere sistemi propri dei clienti o soluzioni di terze parti.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Per abilitare la funzionalità beta di destinazione dell’API HTTP per la tua azienda, contatta i rappresentanti di Adobe o l’Assistenza clienti Adobe.

Per utilizzare la destinazione API HTTP per esportare i dati da Experience Platform, è necessario soddisfare i seguenti prerequisiti:

* È necessario disporre di un endpoint HTTP che supporti l’API REST.
* L’endpoint HTTP deve supportare lo schema del profilo di Experience Platform. Nella destinazione API HTTP non è supportata alcuna trasformazione in uno schema di payload di terze parti. Fai riferimento a [dati esportati](#exported-data) per un esempio dello schema di output dell&#39;Experience Platform.
* L&#39;endpoint HTTP deve supportare le intestazioni.
* L&#39;endpoint HTTP deve supportare [Credenziali client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticazione. Questo requisito è valido quando la destinazione API HTTP è nella fase beta.
* Le credenziali client devono essere incluse nel corpo delle richieste POST all’endpoint , come illustrato nell’esempio seguente.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

È inoltre possibile utilizzare [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) per impostare un’integrazione e inviare dati di profilo di Experience Platform a un endpoint HTTP.

## inserire nell&#39;elenco Consentiti indirizzo IP {#ip-address-allowlist}

Per soddisfare i requisiti di sicurezza e conformità dei clienti, Experience Platform fornisce un elenco di IP statici che puoi inserire nell&#39;elenco Consentiti per la destinazione API HTTP. Fai riferimento a [ELENCO CONSENTITI di indirizzi IP per le destinazioni di streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) per l’elenco completo degli IP da inserire nell&#39;elenco Consentiti.

## Collegati alla destinazione {#connect-destination}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL httpEndpoint]**: la [!DNL URL] dell’endpoint HTTP a cui desideri inviare i dati del profilo.
   * Facoltativamente, puoi aggiungere parametri di query al [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: la [!DNL URL] dell’endpoint HTTP utilizzato per [!DNL OAuth2] autenticazione.
* **[!UICONTROL ID client]**: la [!DNL clientID] utilizzato nel [!DNL OAuth2] credenziali client.
* **[!UICONTROL Segreto client]**: la [!DNL clientSecret] utilizzato nel [!DNL OAuth2] credenziali client.

   >[!NOTE]
   >
   >Solo [!DNL OAuth2] le credenziali client sono attualmente supportate.

* **[!UICONTROL Nome]**: immetti un nome in base al quale riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: inserisci una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Intestazioni personalizzate]**: inserisci le intestazioni personalizzate che desideri includere nelle chiamate di destinazione, in questo formato: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >L&#39;implementazione corrente richiede almeno un&#39;intestazione personalizzata. Questa limitazione verrà risolta in un aggiornamento futuro.

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](../../ui/activate-streaming-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Attributi di destinazione {#attributes}

In [[!UICONTROL Seleziona attributi]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe consiglia di selezionare un identificatore univoco dal [schema unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione.

## Comportamento dell’esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione API HTTP, in modo da esportare i dati nell’endpoint API solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L’aggiornamento del profilo è stato determinato da una modifica dell’appartenenza al segmento per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nel [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L&#39;aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovino le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

### Cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *cosa determina un’esportazione di dati nella destinazione API HTTP?* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Contenuto dell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i segmenti mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che, se uno dei segmenti mappati cambia stato (da null a Realizzato o da Realizzato/Esistente a Uscire) o qualsiasi attributo mappato viene aggiornato, verrà avviata un’esportazione di destinazione.</li><li>Poiché le identità non possono attualmente essere mappate su destinazioni API HTTP, le modifiche apportate a un dato profilo determinano anche le esportazioni di destinazione.</li><li>Una modifica per un attributo è definita come qualsiasi aggiornamento sull&#39;attributo, che sia o meno lo stesso valore. Ciò significa che una sovrascrittura su un attributo viene considerata una modifica anche se il valore stesso non è stato modificato.</li></ul> | <ul><li>Tutti i segmenti (con lo stato di appartenenza più recente), indipendentemente dal fatto che siano mappati nel flusso di dati o meno, sono inclusi nel `segmentMembership` oggetto.</li><li>Tutte le identità nel `identityMap` sono inclusi anche gli oggetti (l&#39;Experience Platform attualmente non supporta la mappatura delle identità nella destinazione API HTTP).</li><li>Solo gli attributi mappati sono inclusi nell’esportazione di destinazione.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Ad esempio, considera questo flusso di dati come una destinazione HTTP in cui tre segmenti sono selezionati nel flusso di dati e quattro attributi sono mappati sulla destinazione.

![Flusso di dati di destinazione API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo che qualifica o esce da uno dei *tre segmenti mappati*. Tuttavia, nell’esportazione dei dati, nella `segmentMembership` oggetto (vedere [Dati esportati](#exported-data) di seguito), potrebbero essere visualizzati altri segmenti non mappati, se quel particolare profilo è membro di essi. Se un profilo è idoneo per il segmento Cliente con DeLorean Cars ma è anche membro dei segmenti Orologio &quot;Torna al futuro&quot; film e appassionati di fantascienza, allora questi altri due segmenti saranno anche presenti nel `segmentMembership` oggetto dell’esportazione dei dati, anche se non sono mappati nel flusso di dati.

Dal punto di vista degli attributi del profilo, eventuali modifiche ai quattro attributi mappati sopra determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti sul profilo sarà presente nell’esportazione dei dati.

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati arrivano nel tuo [!DNL HTTP] destinazione in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo qualificato per un determinato segmento, è membro di altri due segmenti ed è uscita da un altro segmento. L’esportazione include anche il nome dell’attributo del profilo, il cognome, la data di nascita e l’indirizzo e-mail personale. Le identità di questo profilo sono ECID ed e-mail.

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
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
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
