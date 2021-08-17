---
keywords: streaming;
title: connessione HTTP
description: La destinazione HTTP in Adobe Experience Platform ti consente di inviare dati di profilo a endpoint HTTP di terze parti.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# (Alfa) [!DNL HTTP] connessione

>[!IMPORTANT]
>
>La destinazione [!DNL HTTP] in Platform è attualmente in alfa. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La destinazione [!DNL HTTP] è una destinazione di streaming [!DNL Adobe Experience Platform] che consente di inviare dati di profilo a endpoint di terze parti [!DNL HTTP].

Per inviare i dati del profilo agli endpoint [!DNL HTTP], è innanzitutto necessario connettersi alla destinazione in [[!DNL Adobe Experience Platform]](#connect-destination).

## Casi di utilizzo {#use-cases}

La destinazione [!DNL HTTP] è destinata ai clienti che devono esportare dati di profilo XDM e segmenti di pubblico in endpoint [!DNL HTTP] generici.

[!DNL HTTP] gli endpoint possono essere sistemi propri dei clienti o soluzioni di terze parti.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL httpEndpoint]**: l’endpoint HTTP  [!DNL URL] a cui desideri inviare i dati del profilo.
   * Facoltativamente, puoi aggiungere parametri di query al [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: l’endpoint HTTP  [!DNL URL] utilizzato per l’ [!DNL OAuth2] autenticazione.
* **[!UICONTROL ID]** client: il  [!DNL clientID] parametro utilizzato nelle credenziali  [!DNL OAuth2] client.
* **[!UICONTROL Segreto]** client: il  [!DNL clientSecret] parametro utilizzato nelle credenziali  [!DNL OAuth2] client.

   >[!NOTE]
   >
   >Al momento sono supportate solo le credenziali client [!DNL OAuth2].

* **[!UICONTROL Nome]**: immetti un nome in base al quale riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: inserisci una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Intestazioni]** personalizzate: inserisci le intestazioni personalizzate che desideri includere nelle chiamate di destinazione, in questo formato:  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >L&#39;implementazione corrente richiede almeno un&#39;intestazione personalizzata. Questa limitazione verrà risolta in un aggiornamento futuro.

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico nelle destinazioni, consulta [Attivare profili e segmenti in una destinazione](../ui/activate-destinations.md#select-attributes) .

## Attributi di destinazione {#attributes}

Nel passaggio [[!UICONTROL Seleziona attributi]](../ui/activate-destinations.md#select-attributes), quando [attivi segmenti](../ui/activate-destinations.md) in una destinazione [!DNL HTTP], Adobe consiglia di selezionare un identificatore univoco dal tuo [schema di unione](../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione.

## Dati esportati {#exported-data}

I dati esportati [!DNL Experience Platform] arrivano nella destinazione [!DNL HTTP] in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico qualificato per un determinato segmento ed uscito da un altro segmento. Le identità di questo potenziale cliente sono [!DNL ECID] e-mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
