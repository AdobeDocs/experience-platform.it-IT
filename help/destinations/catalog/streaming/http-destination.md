---
keywords: streaming;
title: connessione HTTP
description: La destinazione API HTTP in Adobe Experience Platform ti consente di inviare dati di profilo a endpoint HTTP di terze parti.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3bec18f1b7209b1f329dc90aadb597edb6143291
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 3%

---

# (Beta) [!DNL HTTP] Connessione API

>[!IMPORTANT]
>
>La [!DNL HTTP] la destinazione in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La [!DNL HTTP] La destinazione API è un [!DNL Adobe Experience Platform] destinazione in streaming che consente di inviare dati di profilo a terze parti [!DNL HTTP] endpoint.

Per inviare i dati del profilo a [!DNL HTTP] endpoint, è necessario prima connettersi alla destinazione in [[!DNL Adobe Experience Platform]](#connect-destination).

## Casi di utilizzo {#use-cases}

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

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati arrivano nel tuo [!DNL HTTP] destinazione in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico qualificato per un determinato segmento ed uscito da un altro segmento. Le identità di questa prospettiva sono [!DNL ECID] e-mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
