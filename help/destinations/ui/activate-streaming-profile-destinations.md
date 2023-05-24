---
keywords: attivare destinazioni profilo;attivare destinazioni;attivare dati; attivare destinazioni e-mail marketing; attivare destinazioni archiviazione cloud
title: Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming
type: Tutorial
description: Scopri come attivare i dati sul pubblico disponibili in Adobe Experience Platform inviando segmenti a destinazioni basate su profili di streaming.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 5bb2981b8187fcd3de46f80ca6c892421b3590f6
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming

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

1. Seleziona **[!UICONTROL Attivare segmenti]** sulla scheda corrispondente alla destinazione in cui desideri attivare i segmenti, come illustrato nell’immagine seguente.

   ![Immagine che evidenzia il controllo Attiva segmenti nella scheda del catalogo delle destinazioni.](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Seleziona la connessione di destinazione da utilizzare per attivare i segmenti, quindi fai clic su **[!UICONTROL Successivo]**.

   ![Immagine che mostra una selezione di due destinazioni a cui è possibile connettersi.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Passa alla sezione successiva a [seleziona i segmenti](#select-segments).

## Seleziona i segmenti {#select-segments}

Utilizza le caselle di controllo a sinistra dei nomi dei segmenti per selezionare i segmenti da attivare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Immagine che evidenzia la selezione delle caselle di controllo nel passaggio Seleziona segmenti del flusso di lavoro di attivazione.](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Seleziona attributi profilo {#select-attributes}

In **[!UICONTROL Mappatura]** fase, seleziona gli attributi del profilo che desideri inviare alla destinazione target.

>[!NOTE]
>
> Adobe Experience Platform compila la selezione con quattro attributi consigliati e comunemente utilizzati dallo schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Le esportazioni di file variano nei seguenti modi, a seconda che `segmentMembership.status` è selezionato:
* Se il `segmentMembership.status` è selezionato, i file esportati includono **[!UICONTROL Attivo]** membri nello snapshot completo iniziale e **[!UICONTROL Attivo]** e **[!UICONTROL Scaduto]** membri nelle esportazioni incrementali successive.
* Se il `segmentMembership.status` non è selezionato, i file esportati includono solo **[!UICONTROL Attivo]** membri nello snapshot completo iniziale e nelle esportazioni incrementali successive.

![Immagine che mostra gli attributi preriempiti e consigliati nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. In **[!UICONTROL Seleziona attributi]** pagina, seleziona **[!UICONTROL Aggiungi nuovo campo]**.

   ![Immagine che evidenzia il controllo Aggiungi nuovo campo nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selezionare la freccia a destra della **[!UICONTROL Campo schema]** voce.

   ![Immagine che evidenzia come selezionare un campo sorgente nel passaggio di mappatura.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. In **[!UICONTROL Seleziona campo]** , selezionare gli attributi XDM da inviare alla destinazione, quindi scegliere **[!UICONTROL Seleziona]**.

   ![Immagine che mostra una selezione di campi XDM da selezionare come campi sorgente.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Per aggiungere altre mappature, ripeti i passaggi da 1 a 3, quindi seleziona **[!UICONTROL Successivo]**.

## Revisione {#review}

Il giorno **[!UICONTROL Revisione]** pagina, è possibile visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Riepilogo della selezione nel passaggio di revisione.](/help/destinations/assets/ui/activate-streaming-profile-destinations/review.png)

### Valutazione dei criteri di consenso {#consent-policy-evaluation}

Se l’organizzazione ha acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleziona **[!UICONTROL Visualizza i criteri di consenso applicabili]** per vedere quali criteri di consenso vengono applicati e quanti profili vengono inclusi di conseguenza nell’attivazione. Ulteriori informazioni [valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per ulteriori informazioni.

### Controlli dei criteri di utilizzo dei dati {#data-usage-policy-checks}

In **[!UICONTROL Revisione]** step, Experience Platform controlla anche eventuali violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di una policy. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non risolvi la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedere [violazioni dei criteri di utilizzo dei dati](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) nella sezione documentazione sulla governance dei dati.

![violazione dei criteri per i dati](../assets/common/data-policy-violation.png)

### Filtrare segmenti {#filter-segments}

Inoltre, in questo passaggio puoi utilizzare i filtri disponibili nella pagina per visualizzare solo i segmenti la cui pianificazione o mappatura è stata aggiornata come parte di questo flusso di lavoro.

![Registrazione schermata che mostra i filtri di segmento disponibili nel passaggio di revisione.](/help/destinations/assets/ui/activate-streaming-profile-destinations/filter-segments-review-step.gif)

Se si è soddisfatti della selezione e non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

## Verifica attivazione segmento {#verify}

Il tuo esportato [!DNL Experience Platform] I dati vengono consegnati nella destinazione target in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico che si è qualificato per un determinato segmento ed è uscito da un altro segmento. Le identità per questo potenziale cliente sono ECID e e-mail.

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
