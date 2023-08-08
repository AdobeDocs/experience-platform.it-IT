---
keywords: destinazioni; domande; domande frequenti; FAQ; FAQ destinazioni
title: Domande frequenti
description: Risposte alle domande più frequenti sulle destinazioni Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 75b9cc3e2c9a18ec8c08c9c3ca774accae31eb7e
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 3%

---

# Domande frequenti {#faq}

## Panoramica {#overview}

Questo documento fornisce le risposte alle domande frequenti sulle destinazioni di Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri [!DNL Platform] servizi, inclusi quelli riscontrati in tutti [!DNL Platform] API, consulta la sezione [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

## Domande generali sulle destinazioni {#general}

### Perché trovo conteggi di profili diversi nell’interfaccia utente di Experienci Platform e nei file CSV esportati?

+++Risposta Questo è un comportamento normale a causa del modo in cui Experienci Platform esegue la segmentazione.

La segmentazione in streaming aggiorna il conteggio dei profili per i tipi di pubblico in streaming nel corso della giornata, mentre la segmentazione batch aggiorna il conteggio dei profili per i tipi di pubblico in batch una volta ogni 24 ore.

Quando la pianificazione dell’esportazione del pubblico differisce dalla pianificazione della segmentazione, il profilo conta tra l’interfaccia utente e la pianificazione esportata [!DNL CSV] sarà diverso, soprattutto per quanto riguarda i tipi di pubblico in streaming.

Consulta la [Documentazione del servizio di segmentazione](../segmentation/home.md) per ulteriori dettagli.
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


## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL Facebook Custom Audiences]?

+++Rispondi prima di poter inviare i tuoi tipi di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* Il tuo [!DNL Facebook] l&#39;account utente deve avere **[!DNL Manage campaigns]** Autorizzazione abilitata per l’account annuncio che intendi utilizzare.
* Il **Adobe Experience Cloud** l&#39;account aziendale deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Consulta [Aggiunta di partner a Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook per ulteriori dettagli.
  >[!IMPORTANT]
  >
  > Durante la configurazione delle autorizzazioni per Adobe Experience Cloud, devi abilitare **Gestire le campagne** autorizzazione. Questa è richiesta per l’integrazione di [!DNL Adobe Experience Platform].
* Leggi e firma la [!DNL Facebook Custom Audiences] Termini di servizio. Per fare questo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].
+++

### Devo aggiungere app o pixel al mio [!DNL Facebook] account inserzionista?

+++Risposta n. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.
+++

### Quanto tempo richiede Facebook per elaborare le informazioni da Adobe Experience Platform?

+++Risposta aggiornata a marzo 2021, [!DNL Facebook Custom Audiences] richiede fino a un&#39;ora per elaborare le informazioni ricevute da [!DNL Platform].
+++

### Posso utilizzare [!DNL Facebook Custom Audiences] per il targeting di pubblico in altri [!DNL Facebook] app, come [!DNL Instagram]?

+++Risposta È possibile utilizzare [!DNL Facebook Custom Audiences] destinazione per il targeting del pubblico in tutta la famiglia di app di Facebook supportate da [!DNL Facebook Custom Audiences], tra cui [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], e [!DNL Messenger]. La selezione dell’app su cui gli inserzionisti desiderano eseguire campagne è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].
+++

### Qual è la differenza tra [!DNL Facebook Custom Audiences] connessione e [!DNL Facebook Pixel] estensione?

+++Rispondi [!DNL Facebook Custom Audiences] utilizzi di connessione [!DNL Platform] identità durante l’invio di tipi di pubblico a [!DNL Facebook], mentre [[!DNL Facebook Pixel] connessione](../destinations/catalog/advertising/facebook-pixel.md) utilizza [!DNL Facebook] pixel integrato in un sito web.

Queste due integrazioni sono complementari; puoi utilizzare entrambe per garantire una migliore copertura del pubblico. Ad esempio, puoi utilizzare [!DNL Facebook Pixel] estensione per la ricerca di visitatori di siti web che non hanno creato un account, mentre [!DNL Facebook Custom Audiences] può aiutarti a eseguire il targeting dei clienti esistenti, in base a [!DNL Platform] identità.
+++

### L’integrazione di Adobe Experience Platform con [!DNL Facebook Custom Audiences] supporta la rimozione degli utenti qualificati da un pubblico quando non sono più idonei per tale pubblico?**

+++Risposta Sì, l’integrazione supporta la rimozione di utenti da [!DNL Facebook Custom Audiences] quando non sono più idonei.
+++

### Come posso eseguire l’hashing dei dati sul pubblico prima di inviarli a [!DNL Facebook]?

+++Risposta
[!DNL Facebook] richiede che non vengano inviate informazioni personali (PII, personally identifiable information) in modo chiaro. Pertanto, il pubblico è stato attivato per [!DNL Facebook] può essere disattivato *con hash* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza ID, vedi [Requisiti di corrispondenza ID](catalog/social/facebook.md#id-matching-requirements).
+++

### In che tipo di identità posso attivare [!DNL Facebook Custom Audiences]?

+++Risposta
[!DNL Facebook Custom Audiences] supporta l’attivazione delle seguenti identità: e-mail con hash, numeri di telefono con hash, [!DNL GAID], [!DNL IDFA]e ID esterni personalizzati.
+++

### È possibile creare più destinazioni Facebook nell’interfaccia utente di Platform per account Facebook separati?

+++Risposta Sì. Una destinazione Facebook in Experienci Platform corrisponde a 1:1 per un account annuncio in Facebook. Puoi creare una destinazione Facebook separata per ogni account Facebook Ad della tua azienda. Segui le [tutorial sulla connessione di destinazione](/help/destinations/ui/connect-destination.md) e connettersi a un account Facebook separato per ogni nuova destinazione Facebook nell’interfaccia utente di Platform. Non esiste alcun limite al numero di account Facebook Ad a cui è possibile connettersi.
+++

## Customer Match di Google {#google-customer-match}

### Durante l’esportazione di tipi di pubblico in Google Customer Match, perché trovo numeri aggiuntivi aggiunti alla fine dei nomi del pubblico nell’interfaccia di Google?

+++Answer Google richiede nomi di pubblico univoci. I numeri che state vedendo sono [Marca temporale UNIX](https://www.unixtimestamp.com/) e vengono aggiunti per mantenere univoci i nomi del pubblico, se hai mappato lo stesso pubblico su più destinazioni di Google.
+++

## Tipi di pubblico di linkedIn corrispondenti {#linkedin}

### Devo aggiungere app o pixel al mio [!DNL LinkedIn] account inserzionista?

+++Risposta n. Poiché non si tratta di un’integrazione basata su pixel, non è necessario aggiungere pixel all’account dell’inserzionista.
+++

### Cosa devo fare prima di poter attivare i tipi di pubblico in [!DNL LinkedIn Matched Audiences]?

+++Rispondi prima di usare [!UICONTROL Pubblico linkedIn corrispondente] destinazione, assicurati che il tuo [!DNL LinkedIn Campaign Manager] l&#39;account ha [!DNL Creative Manager] livello di autorizzazione o superiore.

Per scoprire come modificare il [!DNL LinkedIn Campaign Manager] autorizzazioni utente, consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account Advertising](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.
+++

### Come posso eseguire l’hashing dei dati sul pubblico prima di inviarli a [!DNL LinkedIn]?

+++Risposta
[!DNL LinkedIn] richiede che non vengano inviate informazioni personali (PII, personally identifiable information) in modo chiaro. Pertanto, il pubblico è stato attivato per [!DNL LinkedIn] può essere disattivato *con hash* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

Per spiegazioni dettagliate sui requisiti di corrispondenza ID, vedi [Requisiti di corrispondenza ID](catalog/social/linkedin.md#id-matching-requirements).
+++

### In che tipo di identità posso attivare [!DNL LinkedIn]?

+++Risposta
[!DNL LinkedIn Matched Audiences] supporta l’attivazione delle seguenti identità: e-mail con hash, [!DNL GAID], e [!DNL IDFA].

+++

## Personalizzazione della stessa pagina e della pagina successiva tramite le destinazioni Adobe Target e Personalizzazione personalizzata {#same-next-page-personalization}

### È necessario utilizzare Experienci Platform Web SDK per inviare tipi di pubblico e attributi ad Adobe Target?

+++Risposta n., [SDK per web](../edge/home.md) non è necessario per attivare i tipi di pubblico in [Adobe Target](catalog/personalization/adobe-target-connection.md).

Tuttavia, se [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=it) viene utilizzato al posto di Web SDK, è supportata solo la personalizzazione della sessione successiva.

Per [personalizzazione della stessa pagina e della pagina successiva](ui/activate-edge-personalization-destinations.md) casi d’uso, è necessario utilizzare [SDK per web](../edge/home.md) o [API server di rete Edge](../server-api/overview.md). Consulta la documentazione su [attivazione di tipi di pubblico nelle destinazioni edge](ui/activate-edge-personalization-destinations.md) per ulteriori dettagli sull’implementazione.
+++

### Esiste un limite al numero di attributi che posso inviare da Real-time Customer Data Platform ad Adobe Target o a una destinazione di personalizzazione personalizzata?

+++Risposta Sì, i casi d’uso per la personalizzazione della stessa pagina e della pagina successiva supportano un massimo di 30 attributi per sandbox quando si attivano tipi di pubblico in Adobe Target o destinazioni di personalizzazione personalizzata. Per ulteriori informazioni sui guardrail di attivazione, consulta [documentazione sui guardrail](guardrails.md#edge-destinations-activation).
+++

### Quali tipi di attributi sono supportati per l&#39;attivazione (ad esempio array, mappe, ecc.)?

+++Risposta Attualmente, sono supportati solo attributi statici a valore singolo, come `person.name.firstName`. Gli attributi della matrice non sono attualmente supportati.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Dopo aver creato un pubblico in Experienci Platform, quanto tempo ci vorrà per rendere tale pubblico disponibile per i casi di utilizzo della segmentazione Edge?

+++Le definizioni del pubblico di risposte vengono propagate al [Rete Edge](../edge/home.md) entro un&#39;ora. Tuttavia, se un pubblico viene attivato entro questa prima ora, alcuni visitatori che si sarebbero qualificati per tale pubblico potrebbero non essere presenti.
+++

### Dove posso visualizzare gli attributi attivati in Adobe Target?

+++Gli attributi di risposta saranno disponibili per l’utilizzo in Target in [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) e [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=it) offerte.
+++

### È possibile creare una destinazione senza un flusso di dati e quindi aggiungere un flusso di dati alla stessa destinazione in un secondo momento?

+++Risposta Attualmente non è supportato dall’interfaccia utente Destinazioni. Se hai bisogno di assistenza in questo caso, contatta il rappresentante del tuo Adobe.
+++

### Cosa succede se elimino una destinazione Adobe Target?

+++Risposta Quando elimini una destinazione, tutti i tipi di pubblico e gli attributi mappati nella destinazione vengono eliminati da Adobe Target e rimossi anche dalla rete Edge.
+++

### L’integrazione funziona utilizzando l’API del server di rete Edge?

+++Risposta Sì, l&#39;API del server di rete Edge funziona con la destinazione Personalizzazione personalizzata. Poiché gli attributi del profilo possono contenere dati sensibili, per proteggere tali dati la destinazione Personalizzazione personalizzata richiede l’utilizzo dell’API del server di rete Edge per la raccolta dei dati. Inoltre, tutte le chiamate API devono essere effettuate in un [contesto autenticato](../server-api/authentication.md).
+++

### È possibile disporre di un solo criterio di unione attivo su Edge. Posso creare tipi di pubblico che utilizzano un criterio di unione diverso e inviarli comunque ad Adobe Target come pubblico in streaming?

+++Risposta n. Tutti i tipi di pubblico che desideri attivare in Adobe Target devono utilizzare un pubblico attivo su Edge [criterio di unione](../profile/merge-policies/ui-guide.md).
+++

### L’etichettatura e l’applicazione dell’utilizzo dati (DULE) e i criteri di consenso sono applicati?

+++Risposta Sì. Il [Governance dei dati e criteri di consenso](../data-governance/home.md) creato e associato alle azioni di marketing selezionate regolerà l’attivazione degli attributi selezionati.
+++

### Sono [!DNL Adobe Target] e [!DNL Custom Personalization] destinazioni [!DNL HIPAA]Compatibile con?

+++Risposta
[!DNL Adobe Target] non è [!DNL HIPPA]conforme a [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). I clienti devono consultare i propri team legali in merito a [!DNL HIPPA]: preparazione per i canali di ottimizzazione personalizzati prima di utilizzare la personalizzazione edge tramite [!DNL Adobe Target] o [!DNL Custom Personalization] destinazioni.

Per i casi d’uso in cui la gestione dei criteri di consenso deve essere applicata su larga scala, i clienti devono acquistare [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] le funzioni di sono vendute come suite avanzata di funzionalità e non possono essere acquistate separatamente.

Questo servizio include chiavi gestite dal cliente e soglie elevate per gestire il ciclo di vita dei dati del cliente.

Il [!DNL Adobe Target] e [!DNL Custom Personalization] le destinazioni sono integrate con [Experience Platform di etichette di utilizzo dei dati](../data-governance/labels/overview.md) e [Servizio di applicazione dei criteri di consenso](../data-governance/enforcement/overview.md). Queste funzioni sono disponibili per tutti i clienti.




+++

