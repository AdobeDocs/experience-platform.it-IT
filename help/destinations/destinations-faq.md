---
keywords: destinazioni; domande; domande frequenti; faq; FAQ sulle destinazioni
title: Domande frequenti
seo-title: Frequently asked questions
description: Risposte alle domande più frequenti sulle destinazioni Adobe Experience Platform
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 8f9a601a833149c83d465f68d16ca362ed730b8a
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 4%

---

# Domande frequenti {#faq}

## Panoramica {#overview}

Questo documento fornisce le risposte alle domande frequenti sulle destinazioni Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altre [!DNL Platform] servizi, compresi quelli riscontrati in tutti [!DNL Platform] API, fai riferimento alla [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande generali sulle destinazioni {#general}

**Perché vedo conteggi di profilo diversi nell’interfaccia utente di Experience Platform e nei file CSV esportati?**

Si tratta di un comportamento normale dovuto al modo in cui Experience Platform esegue la segmentazione.

La segmentazione in streaming aggiorna il conteggio dei profili per i segmenti in streaming durante il giorno, mentre la segmentazione in batch aggiorna il conteggio dei profili per i segmenti batch una volta ogni 24 ore.

Quando la pianificazione dell’esportazione dei segmenti si differenzia dalla pianificazione della segmentazione, il profilo viene conteggiato tra l’interfaccia utente e la programmazione esportata [!DNL CSV] Il file sarà diverso, specialmente quando si tratta di segmenti in streaming.

Consulta la sezione [Documentazione del servizio di segmentazione](../segmentation/home.md) per ulteriori dettagli.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL Facebook Custom Audiences]?**

Prima di inviare i segmenti di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* Le [!DNL Facebook] l&#39;account utente deve avere **[!DNL Manage campaigns]** autorizzazione abilitata per l’account annuncio che intendi utilizzare.
* La **Adobe Experience Cloud** l&#39;account aziendale deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Vedi [Aggiungi i partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook per ulteriori informazioni.
   >[!IMPORTANT]
   >
   > Quando configuri le autorizzazioni per Adobe Experience Cloud, devi abilitare il **Gestire le campagne** autorizzazione. Questa è richiesta per l’integrazione di [!DNL Adobe Experience Platform].
* Leggi e firma i [!DNL Facebook Custom Audiences] Termini di servizio Per fare questo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

**Devo aggiungere app o pixel al mio [!DNL Facebook] account inserzionista?**

No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.

**Quanto tempo ci vuole per elaborare le informazioni da Adobe Experience Platform?**

A partire dal marzo 2021, [!DNL Facebook Custom Audiences] richiede fino a un&#39;ora per elaborare le informazioni ricevute da [!DNL Platform].

**Posso usare [!DNL Facebook Custom Audiences] per il targeting del pubblico in altri [!DNL Facebook] app, come [!DNL Instagram]?**

È possibile utilizzare [!DNL Facebook Custom Audiences] destinazione per il targeting del pubblico in tutta la famiglia di app Facebook supportate da [!DNL Facebook Custom Audiences], tra cui [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]e [!DNL Messenger]. La selezione dell’app su cui gli inserzionisti desiderano eseguire le campagne è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

**Qual è la differenza tra [!DNL Facebook Custom Audiences] connessione e [!DNL Facebook Pixel] estensione?**

La [!DNL Facebook Custom Audiences] usi di connessione [!DNL Platform] identità quando si inviano tipi di pubblico a [!DNL Facebook], mentre [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) utilizza [!DNL Facebook] pixel integrato in un sito web.

Queste due integrazioni sono complementari; puoi utilizzare entrambe per garantire una migliore copertura del pubblico. Ad esempio, puoi utilizzare il [!DNL Facebook Pixel] estensione per i visitatori del sito web di ricerca di potenziali clienti che non hanno creato un account, mentre [!DNL Facebook Custom Audiences] può aiutarti a individuare i clienti esistenti in base a [!DNL Platform] identità.

**L’integrazione di Adobe Experience Platform con [!DNL Facebook Custom Audiences] supportare la rimozione degli utenti da un pubblico quando non si qualificano più per esso?**

Sì, l&#39;integrazione supporta la rimozione di utenti da [!DNL Facebook Custom Audiences] quando non si qualificano più.

**Come posso aggiungere hash ai dati del pubblico prima di inviarli a [!DNL Facebook]?**

[!DNL Facebook] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, il pubblico è stato attivato in [!DNL Facebook] può essere disattivato *distrutto* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza degli ID, vedi [Requisiti di corrispondenza ID](catalog/social/facebook.md#id-matching-requirements).

**Che tipo di identità posso attivare? [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] supporta l&#39;attivazione delle seguenti identità: e-mail con hash, numeri di telefono con hash, [!DNL GAID], [!DNL IDFA]e ID esterni personalizzati.

**Posso creare più destinazioni Facebook nell’interfaccia utente di Platform per account Facebook separati?**

Una destinazione Facebook in Experience Platform è 1:1 per un account annuncio in Facebook. Puoi creare una destinazione Facebook separata per ogni account di annunci Facebook nella tua azienda. Segui [esercitazione sulla connessione di destinazione](/help/destinations/ui/connect-destination.md) e collegati a un account Facebook separato per ogni nuova destinazione Facebook nell’interfaccia utente di Platform.

## Tipi di pubblico abbinati a linkedIn {#linkedin}

**Devo aggiungere app o pixel al mio [!DNL LinkedIn] account inserzionista?**

No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.

**Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL LinkedIn Matched Audiences]?**

Prima di poter utilizzare il [!UICONTROL Pubblico abbinato a linkedIn] destinazione, assicurati [!DNL LinkedIn Campaign Manager] l&#39;account [!DNL Creative Manager] livello di autorizzazione o superiore.

Per scoprire come modificare il [!DNL LinkedIn Campaign Manager] autorizzazioni utente, vedi [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account pubblicitari](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

**Come posso aggiungere hash ai dati del pubblico prima di inviarli a [!DNL LinkedIn]?**

[!DNL LinkedIn] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, il pubblico è stato attivato in [!DNL LinkedIn] può essere disattivato *distrutto* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza degli ID, vedi [Requisiti di corrispondenza ID](catalog/social/linkedin.md#id-matching-requirements).

**Che tipo di identità posso attivare? [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] supporta l&#39;attivazione delle seguenti identità: e-mail con hash, [!DNL GAID]e [!DNL IDFA].
