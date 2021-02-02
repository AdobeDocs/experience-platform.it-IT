---
keywords: streaming;
title: La destinazione HTTP è una destinazione Adobe Experience Platform che consente di inviare i dati del profilo a endpoint HTTP di terze parti.
seo-title: La destinazione HTTP è una destinazione Adobe Experience Platform che consente di inviare i dati del profilo a endpoint HTTP di terze parti.
description: La destinazione HTTP è una destinazione Adobe Experience Platform che consente di inviare i dati del profilo a endpoint HTTP di terze parti.
seo-description: La destinazione HTTP è una destinazione Adobe Experience Platform che consente di inviare i dati del profilo a endpoint HTTP di terze parti.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 2%

---


# (Alfa) [!DNL HTTP] Destinazione

>[!IMPORTANT]
>
>La destinazione [!DNL HTTP] in Platform è attualmente in alpha. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La destinazione [!DNL HTTP] è una destinazione di streaming [!DNL Adobe Experience Platform] che consente di inviare i dati del profilo a endpoint [!DNL HTTP] di terze parti.

Per inviare i dati del profilo agli endpoint [!DNL HTTP], è innanzitutto necessario connettersi alla destinazione in [[!DNL Adobe Experience Platform]](#connect-destination).

## Casi d’uso {#use-cases}

La destinazione [!DNL HTTP] è destinata ai clienti che devono esportare dati di profilo XDM e segmenti di pubblico in endpoint [!DNL HTTP] generici.

[!DNL HTTP] gli endpoint possono essere sistemi propri dei clienti o soluzioni di terze parti.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL HTTP API], quindi selezionare **[!UICONTROL Configure]**.

![Attiva destinazione HTTP](../assets/catalog/http/activate.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, fare riferimento alla sezione [Catalog](../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.
>
>![Attiva destinazione HTTP](../assets/catalog/http/connect.png)

Nel passaggio [!UICONTROL Account], è necessario definire i dettagli di connessione dell&#39;endpoint HTTP. Selezionare **[!UICONTROL New account]** e immettere i dettagli di connessione per l&#39;endpoint HTTP a cui si desidera connettersi.
- **[!UICONTROL httpEndpoint]**: l&#39;intero endpoint HTTP a cui si desidera inviare i dati  [!DNL URL] del profilo.
   - Facoltativamente è possibile aggiungere parametri di query al [!UICONTROL httpEndpoint] [!DNL URL].
- **[!UICONTROL authEndpoint]**: il completamento  [!DNL URL] dell&#39;endpoint HTTP utilizzato per  [!DNL OAuth2] l&#39;autenticazione.
- **[!UICONTROL Client ID]**: il  [!DNL clientID] parametro utilizzato nelle credenziali  [!DNL OAuth2] client.
- **[!UICONTROL Client Secret]**: il  [!DNL clientSecret] parametro utilizzato nelle credenziali  [!DNL OAuth2] client.

>[!NOTE]
>
>Al momento sono supportate solo le credenziali client [!DNL OAuth2].

![Connessione endpoint HTTP](../assets/catalog/http/connect.png)

Fai clic su **[!UICONTROL Connect to destination]**. Dopo che la connessione ha esito positivo, fare clic su **[!UICONTROL Next]**.

Nel passaggio [!UICONTROL Authentication], immettete le credenziali di autenticazione dell&#39;account:
- **[!UICONTROL Name]**: immettete un nome in base al quale riconoscerete questa destinazione in futuro.
- **[!UICONTROL Description]**: immettete una descrizione che vi aiuterà a identificare questa destinazione in futuro.
- **[!UICONTROL Custom Headers]**: immettete le intestazioni personalizzate che desiderate includere nelle chiamate di destinazione, in questo formato:  `header1:value1,header2:value2,...headerN:valueN`.

>[!IMPORTANT]
>
>L&#39;implementazione corrente richiede almeno un&#39;intestazione personalizzata. Questa limitazione verrà risolta in un aggiornamento futuro.

![Autenticazione HTTP](../assets/catalog/http/authenticate.png)

**[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, vedere la [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md).

Fai clic su **[!UICONTROL Create destination]**.

## Attiva segmenti

Per informazioni sul flusso di lavoro di attivazione dei segmenti, vedere [Attivare profili e segmenti in una destinazione](../ui/activate-destinations.md#select-attributes).

## Attributi di destinazione

Durante il passaggio [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes), quando [si attivano segmenti](../ui/activate-destinations.md) in una destinazione [!DNL HTTP], si consiglia di selezionare un identificatore univoco dal [schema unione](../../profile/home.md#profile-fragments-and-union-schemas). Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione.

## Dati esportati {#exported-data}

I dati esportati [!DNL Experience Platform] vengono inseriti nella destinazione [!DNL HTTP] in formato JSON. Ad esempio, l&#39;evento seguente contiene l&#39;attributo di profilo dell&#39;indirizzo e-mail di un&#39;audience qualificata per un determinato segmento ed uscita da un altro segmento. Le identità per questo potenziale sono [!DNL ECID] e-mail.

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
