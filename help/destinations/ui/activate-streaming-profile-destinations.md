---
title: Attivare i tipi di pubblico per le destinazioni di esportazione dei profili di streaming
type: Tutorial
description: Scopri come attivare i dati sul pubblico disponibili in Adobe Experience Platform inviando tipi di pubblico a destinazioni basate su profili di streaming.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---


# Attivare i tipi di pubblico per le destinazioni di esportazione dei profili di streaming

>[!IMPORTANT]
> 
> * Per attivare i dati e abilitare il [passaggio di mappatura](#mapping) del flusso di lavoro, sono necessari **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions).
> * Per attivare i dati senza passare attraverso il [passaggio di mappatura](#mapping) del flusso di lavoro, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva segmento senza mappatura]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions).
> 
> Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica {#overview}

Questo articolo spiega il flusso di lavoro necessario per attivare i dati sul pubblico in Adobe Experience Platform nelle destinazioni basate su profili di streaming (dette anche [destinazioni aziendali](/help/destinations/destination-types.md#advanced-enterprise-destinations)).

Il presente articolo si applica alle tre destinazioni seguenti:

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Hub eventi Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [Destinazione API HTTP](/help/destinations/catalog/streaming/http-destination.md).

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, devi avere [connesso correttamente a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**.

   ![Immagine che mostra la scheda del catalogo di destinazione.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva pubblico]** nella scheda corrispondente alla destinazione in cui desideri attivare il pubblico, come illustrato nell&#39;immagine seguente.

   ![Immagine che evidenzia il controllo Attiva pubblico nella scheda del catalogo delle destinazioni.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Seleziona la connessione di destinazione da utilizzare per attivare i tipi di pubblico, quindi seleziona **[!UICONTROL Successivo]**.

   ![Immagine che mostra una selezione di due destinazioni a cui è possibile connettersi.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Passa alla sezione successiva per [selezionare il pubblico](#select-audiences).

## Seleziona i tipi di pubblico {#select-audiences}

Per selezionare i tipi di pubblico che si desidera attivare nella destinazione, utilizzare le caselle di controllo a sinistra dei nomi dei tipi di pubblico, quindi selezionare **[!UICONTROL Avanti]**.

Puoi scegliere tra più tipi di pubblico, a seconda della loro origine:

* **[!UICONTROL Servizio di segmentazione]**: tipi di pubblico generati in Experience Platform dal servizio di segmentazione. Per ulteriori dettagli, consulta la [documentazione di Audience Portal](../../segmentation/ui/audience-portal.md).
* **[!UICONTROL Caricamento personalizzato]**: pubblico generato al di fuori di Experience Platform e caricato in Platform come file CSV. Per ulteriori informazioni sui tipi di pubblico esterni, consulta la documentazione su [importazione di un pubblico](../../segmentation/ui/audience-portal.md#import-audience).
* Altri tipi di pubblico, provenienti da altre soluzioni Adobe, ad esempio [!DNL Audience Manager].

![Immagine che evidenzia la selezione delle caselle di controllo nel passaggio Seleziona tipi di pubblico del flusso di lavoro di attivazione.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Seleziona attributi profilo {#select-attributes}

Nel passaggio **[!UICONTROL Mappatura]**, seleziona gli attributi del profilo che desideri inviare alla destinazione.

1. Nella pagina **[!UICONTROL Seleziona attributi]**, seleziona **[!UICONTROL Aggiungi nuovo campo]**.

   ![Immagine che evidenzia il controllo Aggiungi nuovo campo nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selezionare la freccia a destra della voce **[!UICONTROL Campo schema]**.

   ![Immagine che evidenzia come selezionare un campo di origine nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Nella pagina **[!UICONTROL Seleziona campo]**, seleziona gli attributi XDM da inviare alla destinazione, quindi scegli **[!UICONTROL Seleziona]**.

   ![Immagine che mostra una selezione di campi XDM che è possibile selezionare come campi di origine.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Per aggiungere altri campi, ripetere i passaggi da 1 a 3, quindi selezionare **[!UICONTROL Avanti]**.

## Controlla {#review}

Nella pagina **[!UICONTROL Rivedi]** puoi visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Riepilogo selezioni nel passaggio di revisione.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Valutazione dei criteri di consenso {#consent-policy-evaluation}

[La valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) non è attualmente supportata nelle esportazioni nelle tre destinazioni Enterprise: Amazon Kinesis, Azure Event Hubs e HTTP API.

Ciò significa che i profili che non hanno acconsentito alla destinazione *sono inclusi* nelle esportazioni verso queste tre destinazioni.

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### Controlli dei criteri di utilizzo dei dati {#data-usage-policy-checks}

Nel passaggio **[!UICONTROL Rivedi]**, Experience Platform controlla anche eventuali violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di una policy. Non puoi completare il flusso di lavoro di attivazione del pubblico finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, leggere le [violazioni dei criteri di utilizzo dei dati](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) nella sezione relativa alla governance dei dati.

![violazione criteri dati](../assets/common/data-policy-violation.png)

### Filtrare i tipi di pubblico {#filter-audiences}

Inoltre, in questo passaggio puoi utilizzare i filtri disponibili nella pagina per visualizzare solo i tipi di pubblico la cui pianificazione o mappatura è stata aggiornata come parte di questo flusso di lavoro.

![Registrazione dello schermo che mostra i filtri del pubblico disponibili nel passaggio di revisione.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Se si è soddisfatti della selezione e non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

## Verificare l’attivazione del pubblico {#verify}

I dati di [!DNL Experience Platform] esportati vengono consegnati nella destinazione di destinazione in formato JSON. Ad esempio, l’evento seguente contiene l’attributo dell’indirizzo e-mail di un profilo idoneo per un determinato pubblico ed uscito da un altro pubblico. Le identità per questo prospect sono `ECID` e `email_lc_sha256`.

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
        "status": "realized"
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
