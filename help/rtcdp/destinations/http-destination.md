---
keywords: streaming;
title: La destinazione HTTP è una destinazione della piattaforma dati cliente in tempo reale che consente di inviare dati di profilo a endpoint HTTP di terze parti.
seo-title: La destinazione HTTP è una destinazione della piattaforma dati cliente in tempo reale che consente di inviare dati di profilo a endpoint HTTP di terze parti.
description: La destinazione HTTP è una destinazione della piattaforma dati cliente in tempo reale che consente di inviare dati di profilo a endpoint HTTP di terze parti.
seo-description: La destinazione HTTP è una destinazione della piattaforma dati cliente in tempo reale che consente di inviare dati di profilo a endpoint HTTP di terze parti.
translation-type: tm+mt
source-git-commit: 6eabcd70b133051205b669253f280cb92c24412f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---


# (Alfa) [!DNL HTTP] Destinazione

>[!IMPORTANT]
>
>La [!DNL HTTP] destinazione in CDP in tempo reale  Adobe è attualmente in alfa. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La [!DNL HTTP] destinazione è una destinazione di [!DNL Real-time Customer Data Platform] streaming che consente di inviare i dati del profilo agli [!DNL HTTP] endpoint di terze parti.

Per inviare i dati del profilo agli [!DNL HTTP] endpoint, è innanzitutto necessario connettersi alla destinazione nell&#39; [[!DNL Real-time Customer Data Platform]](#connect-destination).

## Casi d’uso {#use-cases}

La [!DNL HTTP] destinazione è destinata ai clienti che devono esportare dati di profilo XDM e segmenti di pubblico in [!DNL HTTP] endpoint generici.

[!DNL HTTP] gli endpoint possono essere sistemi propri dei clienti o soluzioni di terze parti.

## Connetti a destinazione {#connect-destination}

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL HTTP API], quindi **[!UICONTROL Configure]**.

   ![Attiva destinazione HTTP](assets/activate-http-destination.png)

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](../destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.
   >
   >![Attiva destinazione HTTP](assets/connect-http-destination.png)

2. Nel [!UICONTROL Account] passaggio, è necessario definire i dettagli di connessione dell&#39;endpoint HTTP. Selezionate **[!UICONTROL New account]** e immettete i dettagli di connessione per l’endpoint HTTP a cui desiderate connettervi.
   * **[!UICONTROL httpEndpoint]**: il completamento [!DNL URL] dell’endpoint HTTP a cui si desidera inviare i dati del profilo.
      * Facoltativamente è possibile aggiungere parametri di query al [!UICONTROL httpEndpoint][!DNL URL].
   * **[!UICONTROL authEndpoint]**: il completamento [!DNL URL] dell’endpoint HTTP utilizzato per l’ [!DNL OAuth2] autenticazione.
   * **[!UICONTROL Client ID]**: il [!DNL clientID] parametro utilizzato nelle credenziali [!DNL OAuth2] client.
   * **[!UICONTROL Client Secret]**: il [!DNL clientSecret] parametro utilizzato nelle credenziali [!DNL OAuth2] client.

   >[!NOTE]
   >
   >Al momento sono supportate solo le credenziali [!DNL OAuth2] client.

   ![Connessione endpoint HTTP](assets/connect-http-endpoint.png)
3. Fai clic su **[!UICONTROL Connect to destination]**.
4. Dopo che la connessione ha esito positivo, fate clic su **[!UICONTROL Next]**.
5. Nel [!UICONTROL Authentication] passaggio, immettete le credenziali di autenticazione dell&#39;account:
   * **[!UICONTROL Name]**: immettete un nome in base al quale riconoscerete questa destinazione in futuro.
   * **[!UICONTROL Description]**: immettete una descrizione che vi aiuterà a identificare questa destinazione in futuro.
   * **[!UICONTROL Custom Headers]**: immettete le intestazioni personalizzate che desiderate includere nelle chiamate di destinazione, in questo formato: `header1:value1,header2:value2,...headerN:valueN`.

      >[!IMPORTANT]
      >
      >L&#39;implementazione corrente richiede almeno un&#39;intestazione personalizzata. Questa limitazione verrà risolta in un aggiornamento futuro.
   ![Autenticazione HTTP](assets/authentication-http-connection.png)

6. **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](../privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](../../data-governance/policies/overview.md#core-actions)dati.
7. Fai clic su **[!UICONTROL Create destination]**.

## Attiva segmenti

Consulta [Attivare profili e segmenti su una destinazione](activate-destinations.md#select-attributes) per informazioni sul flusso di lavoro di attivazione dei segmenti.

## Attributi di destinazione

Durante il [[!UICONTROL Select attributes]](activate-destinations.md#select-attributes) passaggio, durante l&#39; [attivazione dei segmenti](activate-destinations.md) a una [!DNL HTTP] destinazione, si consiglia di selezionare un identificatore univoco dallo schema [](../../profile/home.md#profile-fragments-and-union-schemas)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione.

## Dati esportati {#exported-data}

I [!DNL Experience Platform] dati esportati vengono inseriti nella [!DNL HTTP] destinazione in formato JSON. Ad esempio, l&#39;evento seguente contiene l&#39;attributo di profilo dell&#39;indirizzo e-mail di un&#39;audience qualificata per un determinato segmento ed uscita da un altro segmento. Le identità di questo potenziale sono [!DNL ECID] e-mail.

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
