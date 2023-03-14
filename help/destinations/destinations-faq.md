---
keywords: destinazioni; domande; domande frequenti; FAQ; FAQ destinazioni
title: Domande frequenti
description: Risposte alle domande più frequenti sulle destinazioni Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# Domande frequenti {#faq}

## Panoramica {#overview}

Questo documento fornisce le risposte alle domande frequenti sulle destinazioni di Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri [!DNL Platform] servizi, inclusi quelli riscontrati in tutti [!DNL Platform] API, consulta la sezione [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande generali sulle destinazioni {#general}

**Perché trovo conteggi di profili diversi nell’interfaccia utente di Experience Platform e nei file CSV esportati?**

Si tratta di un comportamento normale dovuto al modo in cui Experience Platform esegue la segmentazione.

La segmentazione in streaming aggiorna il conteggio dei profili per i segmenti in streaming nel corso della giornata, mentre la segmentazione batch aggiorna il conteggio dei profili per i segmenti batch una volta ogni 24 ore.

Quando la pianificazione di esportazione del segmento differisce dalla pianificazione di segmentazione, il profilo conta tra l’interfaccia utente e il profilo esportato [!DNL CSV] Il file sarà diverso, soprattutto quando si tratta di segmenti di streaming.

Consulta la [Documentazione del servizio di segmentazione](../segmentation/home.md) per ulteriori dettagli.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL Facebook Custom Audiences]?**

Prima di poter inviare i segmenti di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* Il tuo [!DNL Facebook] l&#39;account utente deve avere **[!DNL Manage campaigns]** Autorizzazione abilitata per l’account annuncio che intendi utilizzare.
* Il **Adobe Experience Cloud** l&#39;account aziendale deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Consulta [Aggiunta di partner a Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook per ulteriori dettagli.
   >[!IMPORTANT]
   >
   > Durante la configurazione delle autorizzazioni per Adobe Experience Cloud, devi abilitare **Gestire le campagne** autorizzazione. Questa è richiesta per l’integrazione di [!DNL Adobe Experience Platform].
* Leggi e firma la [!DNL Facebook Custom Audiences] Termini di servizio. Per fare questo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

**Devo aggiungere app o pixel al mio [!DNL Facebook] account inserzionista?**

No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.

**Quanto tempo richiede Facebook per elaborare le informazioni da Adobe Experience Platform?**

Da marzo 2021, [!DNL Facebook Custom Audiences] richiede fino a un&#39;ora per elaborare le informazioni ricevute da [!DNL Platform].

**Posso utilizzare [!DNL Facebook Custom Audiences] per il targeting di pubblico in altri [!DNL Facebook] app, come [!DNL Instagram]?**

È possibile utilizzare [!DNL Facebook Custom Audiences] destinazione per il targeting del pubblico in tutta la famiglia di app di Facebook supportate da [!DNL Facebook Custom Audiences], tra cui [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], e [!DNL Messenger]. La selezione dell’app su cui gli inserzionisti desiderano eseguire campagne è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

**Qual è la differenza tra [!DNL Facebook Custom Audiences] connessione e [!DNL Facebook Pixel] estensione?**

Il [!DNL Facebook Custom Audiences] utilizzi di connessione [!DNL Platform] identità durante l’invio di tipi di pubblico a [!DNL Facebook], mentre [[!DNL Facebook Pixel] connessione](../destinations/catalog/advertising/facebook-pixel.md) utilizza [!DNL Facebook] pixel integrato in un sito web.

Queste due integrazioni sono complementari; puoi utilizzare entrambe per garantire una migliore copertura del pubblico. Ad esempio, puoi utilizzare [!DNL Facebook Pixel] estensione per la ricerca di visitatori di siti web che non hanno creato un account, mentre [!DNL Facebook Custom Audiences] può aiutarti a eseguire il targeting dei clienti esistenti, in base a [!DNL Platform] identità.

**L’integrazione di Adobe Experience Platform con [!DNL Facebook Custom Audiences] supporta la rimozione degli utenti da un pubblico quando non sono più idonei per tale pubblico?**

Sì, l’integrazione supporta la rimozione di utenti da [!DNL Facebook Custom Audiences] quando non sono più idonei.

**Come posso eseguire l’hashing dei dati sul pubblico prima di inviarli a [!DNL Facebook]?**

[!DNL Facebook] richiede che non vengano inviate informazioni personali (PII, personally identifiable information) in modo chiaro. Pertanto, il pubblico è stato attivato per [!DNL Facebook] può essere disattivato *con hash* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza ID, vedi [Requisiti di corrispondenza ID](catalog/social/facebook.md#id-matching-requirements).

**In che tipo di identità posso attivare [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] supporta l’attivazione delle seguenti identità: e-mail con hash, numeri di telefono con hash, [!DNL GAID], [!DNL IDFA]e ID esterni personalizzati.

**È possibile creare più destinazioni Facebook nell’interfaccia utente di Platform per account Facebook separati?**

Sì.  Una destinazione Facebook in Experience Platform corrisponde a 1:1 per un account annuncio in Facebook. Puoi creare una destinazione Facebook separata per ogni account Facebook Ad della tua azienda. Segui le [tutorial sulla connessione di destinazione](/help/destinations/ui/connect-destination.md) e connettersi a un account Facebook separato per ogni nuova destinazione Facebook nell’interfaccia utente di Platform. Non esiste alcun limite al numero di account Facebook Ad a cui è possibile connettersi.

## Customer Match di Google {#google-customer-match}

**Durante l’esportazione di segmenti in Google Customer Match, perché trovo numeri aggiuntivi aggiunti alla fine dei nomi dei segmenti nell’interfaccia di Google?**

Google richiede nomi di segmenti univoci. I numeri che state vedendo sono [Marca temporale UNIX](https://www.unixtimestamp.com/) e vengono aggiunti per mantenere univoci i nomi dei segmenti, se hai mappato lo stesso segmento a più destinazioni Google.

## Tipi di pubblico di linkedIn corrispondenti {#linkedin}

**Devo aggiungere app o pixel al mio [!DNL LinkedIn] account inserzionista?**

No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.

**Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL LinkedIn Matched Audiences]?**

Prima di utilizzare il [!UICONTROL Pubblico linkedIn corrispondente] destinazione, assicurati che il tuo [!DNL LinkedIn Campaign Manager] l&#39;account ha [!DNL Creative Manager] livello di autorizzazione o superiore.

Per scoprire come modificare il [!DNL LinkedIn Campaign Manager] autorizzazioni utente, consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account Advertising](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

**Come posso eseguire l’hashing dei dati sul pubblico prima di inviarli a [!DNL LinkedIn]?**

[!DNL LinkedIn] richiede che non vengano inviate informazioni personali (PII, personally identifiable information) in modo chiaro. Pertanto, il pubblico è stato attivato per [!DNL LinkedIn] può essere disattivato *con hash* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza ID, vedi [Requisiti di corrispondenza ID](catalog/social/linkedin.md#id-matching-requirements).

**In che tipo di identità posso attivare [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] supporta l’attivazione delle seguenti identità: e-mail con hash, [!DNL GAID], e [!DNL IDFA].
