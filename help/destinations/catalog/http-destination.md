---
keywords: streaming;
title: connessione HTTP
description: La destinazione HTTP in Adobe Experience Platform ti consente di inviare dati di profilo a endpoint HTTP di terze parti.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---


# (Alfa) [!DNL HTTP] connessione

>[!IMPORTANT]
>
>La destinazione [!DNL HTTP] in Platform è attualmente in alfa. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La destinazione [!DNL HTTP] è una destinazione di streaming [!DNL Adobe Experience Platform] che consente di inviare dati di profilo a endpoint di terze parti [!DNL HTTP].

Per inviare i dati del profilo agli endpoint [!DNL HTTP], è innanzitutto necessario connettersi alla destinazione in [[!DNL Adobe Experience Platform]](#connect-destination).

## Casi d’uso {#use-cases}

La destinazione [!DNL HTTP] è destinata ai clienti che devono esportare dati di profilo XDM e segmenti di pubblico in endpoint [!DNL HTTP] generici.

[!DNL HTTP] gli endpoint possono essere sistemi propri dei clienti o soluzioni di terze parti.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL HTTP API] e selezionare **[!UICONTROL Configure]**.

![Attiva destinazione HTTP](../assets/catalog/http/activate.png)

Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

![Attiva destinazione HTTP](../assets/catalog/http/connect.png)

Nel passaggio [!UICONTROL Account] , devi definire i dettagli della connessione dell’endpoint HTTP. Seleziona **[!UICONTROL New account]** e immetti i dettagli di connessione per l’endpoint HTTP a cui desideri connetterti.
- **[!UICONTROL httpEndpoint]**: l’intero  [!DNL URL] dell’endpoint HTTP a cui desideri inviare i dati del profilo.
   - Facoltativamente è possibile aggiungere parametri di query al [!UICONTROL httpEndpoint] [!DNL URL].
- **[!UICONTROL authEndpoint]**: il completamento  [!DNL URL] dell’endpoint HTTP utilizzato per l’ [!DNL OAuth2] autenticazione.
- **[!UICONTROL Client ID]**: il  [!DNL clientID] parametro utilizzato nelle credenziali  [!DNL OAuth2] client.
- **[!UICONTROL Client Secret]**: il  [!DNL clientSecret] parametro utilizzato nelle credenziali  [!DNL OAuth2] client.

>[!NOTE]
>
>Al momento sono supportate solo le credenziali client [!DNL OAuth2].

![Connessione endpoint HTTP](../assets/catalog/http/connect.png)

Fai clic su **[!UICONTROL Connect to destination]**. Una volta completata la connessione, fare clic su **[!UICONTROL Next]**.

Nel passaggio [!UICONTROL Authentication] , immetti le credenziali di autenticazione dell’account:
- **[!UICONTROL Name]**: immetti un nome in base al quale riconoscerai questa destinazione in futuro.
- **[!UICONTROL Description]**: inserisci una descrizione che ti aiuterà a identificare questa destinazione in futuro.
- **[!UICONTROL Custom Headers]**: inserisci le intestazioni personalizzate che desideri includere nelle chiamate di destinazione, in questo formato:  `header1:value1,header2:value2,...headerN:valueN`.
- **[!UICONTROL Marketing actions]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](/help/data-governance/policies/overview.md) . Per informazioni sulle singole azioni di marketing definite da Adobe, consulta la [Panoramica sui criteri di utilizzo dei dati](/help/data-governance/policies/overview.md).

>[!IMPORTANT]
>
>L&#39;implementazione corrente richiede almeno un&#39;intestazione personalizzata. Questa limitazione verrà risolta in un aggiornamento futuro.

![Autenticazione HTTP](../assets/catalog/http/authenticate.png)

**[!UICONTROL Marketing action]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../data-governance/policies/overview.md).

Fai clic su **[!UICONTROL Create destination]**.

## Attiva segmenti

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../ui/activate-destinations.md#select-attributes) .

## Attributi di destinazione

Durante il passaggio [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes), quando [attivi segmenti](../ui/activate-destinations.md) in una destinazione [!DNL HTTP], ti consigliamo di selezionare un identificatore univoco dal tuo [schema di unione](../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione.

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
