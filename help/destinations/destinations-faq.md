---
keywords: destinazioni; domande; domande frequenti; faq; FAQ sulle destinazioni
title: Domande frequenti sulle destinazioni
seo-title: Domande frequenti sulle destinazioni
description: Risposte alle domande più frequenti sulle destinazioni Adobe Experience Platform
seo-description: Risposte alle domande più frequenti sulle destinazioni Adobe Experience Platform
source-git-commit: 117f0f82adb764cedaa048e718cd72fa033845a0
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 5%

---


# Domande frequenti sulle destinazioni {#faq}

## [!DNL Facebook Custom Audiences] (#facebook-faq)

**Cosa devo fare prima di poter attivare i tipi di pubblico in  [!DNL Facebook Custom Audiences]?**

Prima di poter inviare i segmenti di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* L&#39;account utente [!DNL Facebook] deve disporre dell&#39;autorizzazione **[!DNL Manage campaigns]** abilitata per l&#39;account annuncio che intendi utilizzare.
* L&#39;account aziendale **Adobe Experience Cloud** deve essere aggiunto come partner pubblicitario nel [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Per ulteriori informazioni, consulta [Aggiungi partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook .
   >[!IMPORTANT]
   >
   > Quando configuri le autorizzazioni per Adobe Experience Cloud, devi abilitare l&#39;autorizzazione **Gestisci campagne**. Questa è richiesta per l’integrazione di [!DNL Adobe Experience Platform].
* Leggi e firma i termini del servizio [!DNL Facebook Custom Audiences]. Per fare questo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

**Devo aggiungere app o pixel al mio account  [!DNL Facebook] inserzionista?**

No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.

**Quanto tempo ci vuole per elaborare le informazioni da Adobe Experience Platform?**

A partire da marzo 2021, [!DNL Facebook Custom Audiences] richiede fino a un&#39;ora per elaborare le informazioni ricevute da [!DNL Platform].

**Posso utilizzare  [!DNL Facebook Custom Audiences] per il targeting del pubblico in altre  [!DNL Facebook] app, come  [!DNL Instagram]?**

Puoi utilizzare la destinazione [!DNL Facebook Custom Audiences] per il targeting del pubblico per la famiglia di app Facebook supportate da [!DNL Facebook Custom Audiences], inclusi [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. La selezione dell’app su cui gli inserzionisti desiderano eseguire le campagne è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

**Qual è la differenza tra  [!DNL Facebook Custom Audiences] connessione ed  [!DNL Facebook Pixel] estensione?**

La connessione [!DNL Facebook Custom Audiences] utilizza le identità [!DNL Platform] quando si inviano tipi di pubblico a [!DNL Facebook], mentre la [[!DNL Facebook Pixel] connessione](../destinations/catalog/advertising/facebook-pixel.md) utilizza il pixel [!DNL Facebook] integrato in un sito web.

Queste due integrazioni sono complementari; puoi utilizzare entrambe per garantire una migliore copertura del pubblico. Ad esempio, puoi utilizzare l’ estensione [!DNL Facebook Pixel] per la ricerca di potenziali visitatori del sito web che non hanno creato un account, mentre [!DNL Facebook Custom Audiences] può aiutarti a individuare i clienti esistenti, in base alle [!DNL Platform] identità.

**L’integrazione di Adobe Experience Platform con  [!DNL Facebook Custom Audiences] supporta la rimozione degli utenti da un pubblico quando non sono più idonei?**

Sì, l&#39;integrazione supporta la rimozione di utenti da [!DNL Facebook Custom Audiences] quando non sono più qualificati.

**Come posso aggiungere hash ai dati del pubblico prima di inviarli a  [!DNL Facebook]?**

[!DNL Facebook] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Facebook] possono essere contrassegnati da identificatori *con hash* come indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza degli ID, consulta [Requisiti di corrispondenza degli ID](catalog/social/facebook.md#id-matching-requirements).

**In che tipo di identità posso attivare  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] supporta l&#39;attivazione delle seguenti identità: e-mail con hash, numeri di telefono con hash,  [!DNL GAID],  [!DNL IDFA] e ID esterni personalizzati.

## Tipi di pubblico abbinati a linkedIn {#linkedin}

**Devo aggiungere app o pixel al mio account  [!DNL LinkedIn] inserzionista?**

No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.

**Cosa devo fare prima di poter attivare i tipi di pubblico in  [!DNL LinkedIn Matched Audiences]?**

Prima di poter utilizzare la destinazione [!UICONTROL LinkedIn Matched Audience] , assicurati che il tuo account [!DNL LinkedIn Campaign Manager] disponga del livello di autorizzazione [!DNL Creative Manager] o superiore.

Per informazioni su come modificare le autorizzazioni utente [!DNL LinkedIn Campaign Manager], consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account pubblicitari](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

**Come posso aggiungere hash ai dati del pubblico prima di inviarli a  [!DNL LinkedIn]?**

[!DNL LinkedIn] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, i tipi di pubblico attivati in [!DNL LinkedIn] possono essere contrassegnati da identificatori *con hash* come indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza degli ID, consulta [Requisiti di corrispondenza degli ID](catalog/social/linkedin.md#id-matching-requirements).

**In che tipo di identità posso attivare  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] supporta l&#39;attivazione delle seguenti identità: indirizzi e-mail con hash  [!DNL GAID] e  [!DNL IDFA].
