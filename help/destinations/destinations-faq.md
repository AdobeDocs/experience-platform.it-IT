---
keywords: destinazioni; domande; domande frequenti; FAQ; FAQ destinazioni
title: Domande frequenti
description: Risposte alle domande più frequenti sulle destinazioni Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Domande frequenti {#faq}

## Panoramica {#overview}

Questo documento fornisce le risposte alle domande frequenti sulle destinazioni di Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi [!DNL Platform], inclusi quelli incontrati in tutte le API [!DNL Platform], fare riferimento alla [guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande generali sulle destinazioni {#general}

### Perché trovo conteggi di profili diversi nell’interfaccia utente di Experience Platform e nei file CSV esportati?

+++Risposta
Si tratta di un comportamento normale dovuto al modo in cui Experience Platform esegue la segmentazione.

La segmentazione in streaming aggiorna il conteggio dei profili per i tipi di pubblico in streaming nel corso della giornata, mentre la segmentazione batch aggiorna il conteggio dei profili per i tipi di pubblico in batch una volta ogni 24 ore.

Quando la pianificazione dell&#39;esportazione del pubblico differisce dalla pianificazione della segmentazione, i conteggi dei profili tra l&#39;interfaccia utente e il file [!DNL CSV] esportato saranno diversi, soprattutto quando si tratta di tipi di pubblico in streaming.

Per ulteriori dettagli, consulta la [documentazione del servizio di segmentazione](../segmentation/home.md).
+++

### Perché trovo percentuali di corrispondenza basse quando disattivi e riattivi un pubblico aggiornato nella stessa destinazione?

+++Risposta

La disattivazione e la rimozione di un pubblico da una destinazione di streaming non attivano una retrocompilazione dopo la riattivazione del pubblico nella stessa destinazione di streaming.

**Esempio**

Hai attivato un pubblico composto da 10 profili in una destinazione di streaming.

Dopo aver attivato il pubblico, ti rendi conto di voler modificare la sua configurazione in modo da disattivarlo e modificarne i criteri di popolazione, per una popolazione di 100 profili.

Riattivi il pubblico aggiornato nella stessa destinazione, ma poiché non viene attivata alcuna retrocompilazione, la destinazione non riceve gli altri 90 profili.

**Soluzione**

Per garantire che tutti i profili vengano inviati alla destinazione, devi creare un nuovo pubblico con la nuova configurazione, quindi attivarlo nella destinazione.

+++

### Quando un pubblico viene rimosso da una destinazione, esiste un segnale inviato alla destinazione che indica che il pubblico viene rimosso?

+++Risposta

No, non esiste alcuna dipendenza tra la destinazione dell&#39;Experience Platform e l&#39;istanza cliente del sistema di destinazione. Dal lato della ricezione, l’unica indicazione che il sistema di destinazione vedrebbe è che ha smesso di ricevere i dati sul pubblico.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL Facebook Custom Audiences]?

+++Risposta
Prima di poter inviare i tipi di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* L&#39;account utente [!DNL Facebook] deve avere l&#39;autorizzazione **[!DNL Manage campaigns]** abilitata per l&#39;account annuncio che intendi utilizzare.
* L&#39;account aziendale **Adobe Experience Cloud** deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Usa `business ID=206617933627973`. Per ulteriori informazioni, consulta [Aggiungere partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook.

  >[!IMPORTANT]
  >
  > Durante la configurazione delle autorizzazioni per Adobe Experience Cloud, devi abilitare l&#39;autorizzazione **Gestisci campagne**. Questa è richiesta per l&#39;integrazione di [!DNL Adobe Experience Platform].
* Leggi e firma le Condizioni per l&#39;utilizzo di [!DNL Facebook Custom Audiences]. Per eseguire questa operazione, vai a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].
+++

### Devo aggiungere app o pixel al mio account pubblicitario [!DNL Facebook]?

+++Risposta
No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.
+++

### Quanto tempo richiede Facebook per elaborare le informazioni da Adobe Experience Platform?

+++Risposta
A marzo 2021, [!DNL Facebook Custom Audiences] ha bisogno di un&#39;ora per elaborare le informazioni ricevute da [!DNL Platform].
+++

### Posso usare [!DNL Facebook Custom Audiences] per il targeting del pubblico in altre app [!DNL Facebook], come [!DNL Instagram]?

+++Amswer
È possibile utilizzare la destinazione [!DNL Facebook Custom Audiences] per il targeting del pubblico in tutta la famiglia di app di Facebook supportate da [!DNL Facebook Custom Audiences], inclusi [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. La selezione dell&#39;app su cui gli inserzionisti desiderano eseguire le campagne è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].
+++

### Differenza tra la connessione [!DNL Facebook Custom Audiences] e l&#39;estensione [!DNL Facebook Pixel]

+++Risposta
La connessione [!DNL Facebook Custom Audiences] utilizza identità [!DNL Platform] per l&#39;invio di tipi di pubblico a [!DNL Facebook], mentre la connessione [[!DNL Facebook Pixel] connessione](../destinations/catalog/advertising/facebook-pixel.md) utilizza il pixel [!DNL Facebook] integrato in un sito Web.

Queste due integrazioni sono complementari; puoi utilizzare entrambe per garantire una migliore copertura del pubblico. Ad esempio, puoi utilizzare l&#39;estensione [!DNL Facebook Pixel] per cercare i visitatori del sito Web che non hanno creato un account, mentre [!DNL Facebook Custom Audiences] può aiutarti a individuare i clienti esistenti, in base alle identità di [!DNL Platform].
+++

### L&#39;integrazione di Adobe Experience Platform con [!DNL Facebook Custom Audiences] supporta l&#39;esclusione di utenti da un pubblico quando non sono più idonei per tale pubblico?**

+++Risposta
Sì, l&#39;integrazione supporta la rimozione degli utenti da [!DNL Facebook Custom Audiences] quando non sono più idonei.
+++

### Come posso eseguire l&#39;hashing dei dati del pubblico prima di inviarli a [!DNL Facebook]?

+++Risposta
[!DNL Facebook] non richiede l&#39;invio di informazioni personali (PII, personally identifiable information) in chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Facebook] possono essere ricavati da *identificatori con hash*, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza ID, consulta [Requisiti di corrispondenza ID](catalog/social/facebook.md#id-matching-requirements).
+++

### Quali identità posso attivare in [!DNL Facebook Custom Audiences]?

+++Risposta
[!DNL Facebook Custom Audiences] supporta l&#39;attivazione delle seguenti identità: e-mail con hash, numeri di telefono con hash, [!DNL GAID], [!DNL IDFA] e ID esterni personalizzati.
+++

### È possibile creare più destinazioni Facebook nell’interfaccia utente di Platform per account Facebook separati?

+++Risposta
Sì. Una destinazione Facebook in Experience Platform corrisponde a 1:1 per un account annuncio in Facebook. Puoi creare una destinazione Facebook separata per ogni account Facebook Ad della tua azienda. Segui l&#39;[esercitazione sulla connessione di destinazione](/help/destinations/ui/connect-destination.md) e collegati a un account Facebook separato per ogni nuova destinazione Facebook nell&#39;interfaccia utente di Platform. Non esiste alcun limite al numero di account Facebook Ad a cui è possibile connettersi.
+++

## Google Customer Match {#google-customer-match}

### Durante l’esportazione di tipi di pubblico in Google Customer Match, perché trovo numeri aggiuntivi aggiunti alla fine dei nomi del pubblico nell’interfaccia di Google?

+++Risposta
Google richiede nomi di pubblico univoci. I numeri visualizzati sono [marche temporali UNIX](https://www.unixtimestamp.com/) e vengono aggiunti per mantenere univoci i nomi dei tipi di pubblico, se lo stesso pubblico è stato mappato a più destinazioni Google.
+++

## Tipi di pubblico di linkedIn corrispondenti {#linkedin}

### Devo aggiungere app o pixel al mio account pubblicitario [!DNL LinkedIn]?

+++Risposta
No. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.
+++

### Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL LinkedIn Matched Audiences]?

+++Risposta
Prima di poter utilizzare la destinazione [!UICONTROL LinkedIn Matched Audience], assicurati che il tuo account [!DNL LinkedIn Campaign Manager] disponga del livello di autorizzazione [!DNL Creative Manager] o superiore.

Per informazioni su come modificare le autorizzazioni utente di [!DNL LinkedIn Campaign Manager], consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente per gli account Advertising](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.
+++

### Come posso eseguire l&#39;hashing dei dati del pubblico prima di inviarli a [!DNL LinkedIn]?

+++Risposta
[!DNL LinkedIn] non richiede l&#39;invio di informazioni personali (PII, personally identifiable information) in chiaro. Pertanto, i tipi di pubblico attivati in [!DNL LinkedIn] possono essere ricavati da *identificatori con hash*, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza ID, consulta [Requisiti di corrispondenza ID](catalog/social/linkedin.md#id-matching-requirements).
+++

### Quali identità posso attivare in [!DNL LinkedIn]?

+++Risposta
[!DNL LinkedIn Matched Audiences] supporta l&#39;attivazione delle seguenti identità: e-mail con hash, [!DNL GAID] e [!DNL IDFA].

+++

## Personalizzazione della stessa pagina e della pagina successiva tramite le destinazioni Adobe Target e Custom Personalization {#same-next-page-personalization}

### È necessario utilizzare Experience Platform Web SDK per inviare tipi di pubblico e attributi ad Adobe Target?

+++Risposta
No, [Web SDK](../web-sdk/home.md) non è necessario per attivare i tipi di pubblico in [Adobe Target](catalog/personalization/adobe-target-connection.md).

Tuttavia, se [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) viene utilizzato al posto di Web SDK, è supportata solo la personalizzazione della sessione successiva.

Per i casi di utilizzo di [personalizzazione della stessa pagina e della pagina successiva](ui/activate-edge-personalization-destinations.md), è necessario utilizzare [Web SDK](../web-sdk/home.md) o [Edge Network Server API](../server-api/overview.md). Per ulteriori dettagli sull&#39;implementazione, consulta la documentazione sull&#39;[attivazione dei tipi di pubblico nelle destinazioni Edge](ui/activate-edge-personalization-destinations.md).
+++

### Esiste un limite al numero di attributi che posso inviare da Real-time Customer Data Platform ad Adobe Target o a una destinazione Personalization personalizzata?

+++Risposta
Sì, i casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva supportano un massimo di 30 attributi per sandbox, quando si attivano tipi di pubblico su destinazioni Adobe Target o Custom Personalization. Ulteriori informazioni sui guardrail di attivazione sono disponibili nella [documentazione sui guardrail](guardrails.md#edge-destinations-activation).
+++

### Quali tipi di attributi sono supportati per l&#39;attivazione (ad esempio array, mappe, ecc.)?

+++Risposta
Attualmente sono supportati solo attributi statici a valore singolo, ad esempio `person.name.firstName`. Gli attributi della matrice non sono attualmente supportati.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Dopo aver creato un pubblico in Experience Platform, quanto tempo ci vorrà per rendere tale pubblico disponibile per i casi di utilizzo della segmentazione Edge?

+++Risposta
Le definizioni del pubblico vengono propagate all&#39;[Edge Network](../web-sdk/home.md) in un massimo di un&#39;ora. Tuttavia, se un pubblico viene attivato entro questa prima ora, alcuni visitatori che si sarebbero qualificati per tale pubblico potrebbero non essere presenti.
+++

### Dove posso visualizzare gli attributi attivati in Adobe Target?

+++Risposta
Gli attributi saranno disponibili per l&#39;utilizzo in Target nelle offerte [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) e [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).
+++

### È possibile creare una destinazione senza un flusso di dati e quindi aggiungere un flusso di dati alla stessa destinazione in un secondo momento?

+++Risposta
Attualmente questo non è supportato tramite l’interfaccia utente Destinazioni. Se hai bisogno di assistenza in questo caso, contatta il rappresentante del tuo Adobe.
+++

### Cosa succede se elimino una destinazione Adobe Target?

+++Risposta
Quando elimini una destinazione, tutti i tipi di pubblico e gli attributi mappati nella destinazione vengono eliminati da Adobe Target e rimossi anche dall’Edge Network.
+++

### L’integrazione funziona utilizzando l’API del server Edge Network?

+++Risposta
Sì, l’API server di Edge Network funziona con la destinazione Personalization personalizzata. Poiché gli attributi del profilo possono contenere dati sensibili, per proteggere tali dati la destinazione Personalization personalizzata richiede l’utilizzo dell’API server di Edge Network per la raccolta dei dati. Inoltre, tutte le chiamate API devono essere effettuate in un [contesto autenticato](../server-api/authentication.md).
+++

### È possibile disporre di un solo criterio di unione attivo su Edge. Posso creare tipi di pubblico che utilizzano un criterio di unione diverso e inviarli comunque ad Adobe Target come pubblico in streaming?

+++Risposta
No. Tutti i tipi di pubblico che desideri attivare in Adobe Target devono utilizzare un [criterio di unione](../profile/merge-policies/ui-guide.md) attivo sul server Edge.
+++

### L’etichettatura e l’applicazione dell’utilizzo dati (DULE) e i criteri di consenso sono applicati?

+++Risposta
Sì. Le [regole per la governance dei dati e i criteri di consenso](../data-governance/home.md) create e associate alle azioni di marketing selezionate regoleranno l&#39;attivazione degli attributi selezionati.
+++

### Le destinazioni [!DNL Adobe Target] e [!DNL Custom Personalization] [!DNL HIPAA] sono conformi?

+++Risposta
[!DNL Adobe Target] non è conforme a [!DNL HIPPA] con [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). I clienti devono verificare con i propri team legali la disponibilità di [!DNL HIPPA] per i canali di ottimizzazione personalizzati prima di utilizzare la personalizzazione Edge tramite [!DNL Adobe Target] o le destinazioni [!DNL Custom Personalization].

Per i casi d&#39;uso in cui la gestione dei criteri di consenso deve essere applicata su larga scala, i clienti devono acquistare [!DNL Adobe Privacy & Security Shield]. Le funzionalità di [!DNL Adobe Privacy & Security Shield] sono vendute come suite avanzata di funzionalità e non possono essere acquistate separatamente.

Questo servizio include chiavi gestite dal cliente e soglie elevate per gestire il ciclo di vita dei dati del cliente.

Le destinazioni [!DNL Adobe Target] e [!DNL Custom Personalization] sono integrate con le [etichette di utilizzo dati di Experience Platform](../data-governance/labels/overview.md) e il [servizio di applicazione dei criteri di consenso](../data-governance/enforcement/overview.md). Queste funzioni sono disponibili per tutti i clienti.




+++

