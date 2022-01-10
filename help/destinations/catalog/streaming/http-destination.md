---
keywords: streaming;
title: Connessione API HTTP
description: La destinazione API HTTP in Adobe Experience Platform ti consente di inviare dati di profilo a endpoint HTTP di terze parti.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: ba338972be13c7afa6720bba3f0fc96d244b8f9f
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# (Beta) [!DNL HTTP] Connessione API

>[!IMPORTANT]
>
>La [!DNL HTTP] la destinazione in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La [!DNL HTTP] La destinazione API è un [!DNL Adobe Experience Platform] destinazione in streaming che consente di inviare dati di profilo a terze parti [!DNL HTTP] endpoint.

Per inviare i dati del profilo a [!DNL HTTP] endpoint, è necessario prima connettersi alla destinazione in [[!DNL Adobe Experience Platform]](#connect-destination).

## Casi d’uso {#use-cases}

La [!DNL HTTP] La destinazione è destinata ai clienti che devono esportare i dati di profilo XDM e i segmenti di pubblico in segmenti generici [!DNL HTTP] endpoint.

[!DNL HTTP] gli endpoint possono essere sistemi propri dei clienti o soluzioni di terze parti.

## Collegati alla destinazione {#connect}

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

* L’aggiornamento del profilo è stato attivato da una modifica dell’appartenenza al segmento per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato attivato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L’aggiornamento del profilo è stato attivato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovino le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati arrivano nel tuo [!DNL HTTP] destinazione in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo qualificato per un determinato segmento ed uscito da un altro segmento e include il nome dell’attributo del profilo, il cognome, la data di nascita e l’indirizzo e-mail personale. Le identità di questo profilo sono ECID ed e-mail.

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
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
