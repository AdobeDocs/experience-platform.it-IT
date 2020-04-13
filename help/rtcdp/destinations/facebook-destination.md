---
title: Destinazione Facebook
seo-title: Destinazione Facebook
description: Attiva profili per le tue campagne Facebook per il targeting dell'audience, la personalizzazione e la soppressione basate su e-mail con hash.
seo-description: Attiva profili per le tue campagne Facebook per il targeting dell'audience, la personalizzazione e la soppressione basate su e-mail con hash.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Destinazione Facebook

>[!IMPORTANT]
>
>La destinazione Facebook in Adobe Real-time CDP è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

## Panoramica

Attiva profili per le tue campagne Facebook per il targeting dell&#39;audience, la personalizzazione e la soppressione basate su e-mail con hash.

## Specifiche di destinazione

### Tipo di attivazione

Esportazione segmento - vengono esportati tutti i membri di un segmento (pubblico) con i loro identificatori (nome, numero di telefono, ecc.) utilizzato nella destinazione Facebook

## Prerequisiti

Prima di inviare i segmenti di pubblico a [!DNL Facebook], accertati di soddisfare i seguenti requisiti:

1. Il tuo account [!DNL Facebook] utente deve avere l&#39;autorizzazione **Gestisci campagne** abilitata per l&#39;account annuncio che intendi utilizzare.
2. Aggiungi l&#39;account aziendale di **Adobe Experience Cloud** come partner pubblicitario all&#39;interno dell&#39; [!DNL Facebook Ad Account]azienda. Seleziona `business ID=206617933627973`. Per informazioni, consulta [Aggiunta di partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) .
   >[!IMPORTANT]
   > Quando configuri le autorizzazioni per Adobe Experience Cloud, devi abilitare l&#39;autorizzazione **Gestisci campagne** . Questo è richiesto per l&#39; [!DNL Adobe Real-time CDP] integrazione.
3. Leggi e firma le [!DNL Facebook Custom Audiences] Condizioni del servizio. Per fare questo, andate a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dov&#39; `accountID` è il vostro [!DNL Facebook Ad Account ID].


## Destinazione Connect

Per collegare la destinazione Facebook, vedi Flusso di lavoro [di autenticazione delle destinazioni della rete](/help/rtcdp/destinations/social-network-destinations-workflow.md)social.


## Attivare i segmenti su Facebook

Per istruzioni su come attivare i segmenti in Facebook, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).