---
keywords: attivare destinazioni profilo;attivare destinazioni;attivare dati; attivare destinazioni e-mail marketing; attivare destinazioni archiviazione cloud
title: Attivare i tipi di pubblico per le destinazioni di esportazione dei profili di streaming
type: Tutorial
description: Scopri come attivare i dati sul pubblico disponibili in Adobe Experience Platform inviando tipi di pubblico a destinazioni basate su profili di streaming.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---


# Attivare i tipi di pubblico per le destinazioni di esportazione dei profili di streaming

>[!IMPORTANT]
> 
> * Per attivare i dati e abilitare [passaggio di mappatura](#mapping) del flusso di lavoro, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions).
> * Per attivare i dati senza passare attraverso [passaggio di mappatura](#mapping) del flusso di lavoro, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attiva segmento senza mappatura]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions).
> 
> Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica {#overview}

Questo articolo spiega il flusso di lavoro necessario per attivare i dati sul pubblico nelle destinazioni basate su profili di streaming di Adobe Experience Platform, come Amazon Kinesis.

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario aver completato [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, accedi al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda.

   ![Immagine che mostra la scheda del catalogo di destinazione.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva tipi di pubblico]** sulla scheda corrispondente alla destinazione in cui desideri attivare i tipi di pubblico, come illustrato nell’immagine seguente.

   ![Immagine che evidenzia il controllo Attiva pubblico nella scheda del catalogo delle destinazioni.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Seleziona la connessione di destinazione da utilizzare per attivare i tipi di pubblico, quindi fai clic su **[!UICONTROL Successivo]**.

   ![Immagine che mostra una selezione di due destinazioni a cui è possibile connettersi.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Passa alla sezione successiva a [seleziona i tipi di pubblico](#select-audiences).

## Seleziona i tipi di pubblico {#select-audiences}

Per selezionare i tipi di pubblico da attivare nella destinazione, utilizza le caselle di controllo a sinistra dei nomi dei tipi di pubblico, quindi seleziona **[!UICONTROL Successivo]**.

Puoi scegliere tra più tipi di pubblico, a seconda della loro origine:

* **[!UICONTROL Servizio di segmentazione]**: tipi di pubblico generati all’interno di Experience Platform dal servizio di segmentazione. Consulta la [documentazione sulla segmentazione](../../segmentation/ui/overview.md) per ulteriori dettagli.
* **[!UICONTROL Caricamento personalizzato]**: tipi di pubblico generati al di fuori di Experience Platform e caricati in Platform come file CSV. Per ulteriori informazioni sui tipi di pubblico esterni, consulta la documentazione su [importazione di un pubblico](../../segmentation/ui/overview.md#import-audience).
* Altri tipi di pubblico, derivanti da altre soluzioni di Adobe, quali [!DNL Audience Manager].

![Immagine che evidenzia la selezione delle caselle di controllo nel passaggio Seleziona pubblico del flusso di lavoro di attivazione.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Seleziona attributi profilo {#select-attributes}

In **[!UICONTROL Mappatura]** fase, seleziona gli attributi del profilo che desideri inviare alla destinazione target.

1. In **[!UICONTROL Seleziona attributi]** pagina, seleziona **[!UICONTROL Aggiungi nuovo campo]**.

   ![Immagine che evidenzia il controllo Aggiungi nuovo campo nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selezionare la freccia a destra della **[!UICONTROL Campo schema]** voce.

   ![Immagine che evidenzia come selezionare un campo sorgente nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. In **[!UICONTROL Seleziona campo]** , selezionare gli attributi XDM da inviare alla destinazione, quindi scegliere **[!UICONTROL Seleziona]**.

   ![Immagine che mostra una selezione di campi XDM da selezionare come campi sorgente.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Per aggiungere altri campi, ripeti i passaggi da 1 a 3, quindi seleziona **[!UICONTROL Successivo]**.

## Revisione {#review}

Il giorno **[!UICONTROL Revisione]** pagina, è possibile visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Riepilogo della selezione nel passaggio di revisione.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Valutazione dei criteri di consenso {#consent-policy-evaluation}

Se l’organizzazione ha acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleziona **[!UICONTROL Visualizza i criteri di consenso applicabili]** per vedere quali criteri di consenso vengono applicati e quanti profili vengono inclusi di conseguenza nell’attivazione. Ulteriori informazioni [valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per ulteriori informazioni.

### Controlli dei criteri di utilizzo dei dati {#data-usage-policy-checks}

In **[!UICONTROL Revisione]** step, Experience Platform controlla anche eventuali violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di una policy. Non puoi completare il flusso di lavoro di attivazione del pubblico finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedere [violazioni dei criteri di utilizzo dei dati](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) nella sezione documentazione sulla governance dei dati.

![violazione dei criteri per i dati](../assets/common/data-policy-violation.png)

### Filtrare i tipi di pubblico {#filter-audiences}

Inoltre, in questo passaggio puoi utilizzare i filtri disponibili nella pagina per visualizzare solo i tipi di pubblico la cui pianificazione o mappatura è stata aggiornata come parte di questo flusso di lavoro.

![Registrazione dello schermo che mostra i filtri del pubblico disponibili nel passaggio di revisione.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Se si è soddisfatti della selezione e non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

## Verificare l’attivazione del pubblico {#verify}

Il tuo esportato [!DNL Experience Platform] I dati vengono consegnati nella destinazione target in formato JSON. Ad esempio, l’evento seguente contiene l’attributo dell’indirizzo e-mail di un profilo idoneo per un determinato pubblico ed uscito da un altro pubblico. Le identità per questo potenziale cliente sono `ECID` e `email_lc_sha256`.

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
