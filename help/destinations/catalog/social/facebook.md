---
keywords: Connessione facebook;connessione facebook;destinazioni facebook;facebook;instagram;messenger;messenger facebook messenger
title: Connessione facebook
description: Attiva profili per le campagne Facebook per il targeting del pubblico, la personalizzazione e la soppressione in base a e-mail con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 357916aa925c7b3ada4abe64a2bc6ad090d70cc0
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Facebook] connection

## Panoramica {#overview}

Attiva profili per i [!DNL Facebook] campagne per il targeting del pubblico, la personalizzazione e la soppressione basate su e-mail con hash.

Puoi utilizzare questa destinazione per il targeting del pubblico in [!DNL Facebook’s] famiglia di app supportate da [!DNL Custom Audiences], tra cui [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]e [!DNL Messenger]. La selezione dell’app su cui desideri eseguire la campagna è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

![Destinazione facebook nell’interfaccia utente Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casi di utilizzo

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Facebook] destinazione : di seguito sono riportati due esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

### Caso d&#39;uso n. 1

Un rivenditore online vuole raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate in base ai loro ordini precedenti. Il rivenditore online può acquisire indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti a [!DNL Facebook] piattaforma sociale, ottimizzando la spesa pubblicitaria.

### Caso d&#39;uso n. 2

Una compagnia aerea ha diversi livelli di clienti (Bronze, Silver e Gold) e vuole fornire a ciascuno dei livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l’app mobile della compagnia aerea e alcuni di essi non hanno effettuato l’accesso al sito web della società. Gli unici identificatori che l&#39;azienda ha di questi clienti sono gli ID di iscrizione e gli indirizzi e-mail.

Per eseguire il targeting su tali utenti attraverso i social media, possono integrare i dati del cliente dal CRM in Adobe Experience Platform, utilizzando gli indirizzi e-mail come identificatori.

Quindi, possono utilizzare i loro dati offline, inclusi gli ID di appartenenza associati e i livelli di cliente, per creare nuovi segmenti di pubblico di cui possono eseguire il targeting tramite [!DNL Facebook] destinazione.

## Identità supportate {#supported-identities}

[!DNL Facebook Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256 | Hash dei numeri di telefono con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizzare i namespace appropriati rispettivamente per il testo normale e i numeri di telefono con hash. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per gli indirizzi e-mail con testo normale e con hash. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi personalizzato. |

## Tipo di esportazione {#export-type}

**Esportazione segmento** - stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Facebook.

## Prerequisiti per l’account facebook {#facebook-account-prerequisites}

Prima di inviare i segmenti di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* Le [!DNL Facebook] l&#39;account utente deve avere **[!DNL Manage campaigns]** autorizzazione abilitata per l’account annuncio che intendi utilizzare.
* La **Adobe Experience Cloud** l&#39;account aziendale deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Vedi [Aggiungi i partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook per ulteriori informazioni.
   >[!IMPORTANT]
   >
   > Quando configuri le autorizzazioni per Adobe Experience Cloud, devi abilitare il **Gestire le campagne** autorizzazione. È necessaria l&#39;autorizzazione per [!DNL Adobe Experience Platform] integrazione.
* Leggi e firma i [!DNL Facebook Custom Audiences] Termini di servizio Per farlo, vai a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].
   >[!IMPORTANT]
   >
   >Al momento della firma del [!DNL Facebook Custom Audiences] Termini di servizio, assicurati di utilizzare lo stesso account utente utilizzato per l’autenticazione nell’API Facebook.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Facebook] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, il pubblico è stato attivato in [!DNL Facebook] può essere disattivato *distrutto* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

## Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Facebook]:

* **Inserimento di numeri di telefono non elaborati**: è possibile inserire numeri di telefono non elaborati nel [!DNL E.164] in formato [!DNL Platform]. Hanno automaticamente eseguito l’hash al momento dell’attivazione. Se scegli questa opzione, assicurati di inserire sempre i tuoi numeri di telefono non elaborati nel `Phone_E.164` spazio dei nomi.
* **Inserimento di numeri di telefono con hash**: è possibile pre-hash i numeri di telefono prima dell&#39;inserimento in [!DNL Platform]. Se scegli questa opzione, assicurati di inserire sempre i tuoi numeri di telefono con hash nel `Phone_SHA256` spazio dei nomi.

>[!NOTE]
>
>Numeri di telefono acquisiti nel `Phone` Impossibile attivare lo spazio dei nomi in [!DNL Facebook].


## Requisiti di hash e-mail {#email-hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare gli indirizzi e-mail in modo chiaro nell’Experience Platform e avere [!DNL Platform] hashing su attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione in batch](/help/ingestion/batch-ingestion/overview.md) e [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere con hash gli indirizzi e-mail, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail; esempio: `johndoe@example.com`, not `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di utilizzare l’hash della stringa in minuscolo;
   * Esempio: `example@email.com`, not `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutto minuscola
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non saldare la stringa.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] all&#39;attivazione.
> I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione.
> La **[!UICONTROL Applica trasformazione]** viene visualizzata solo quando selezioni gli attributi come campi di origine. Non viene visualizzato quando si selezionano i namespace.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare il `Extern_ID` spazio dei nomi a cui inviare i dati [!DNL Facebook], assicurati di sincronizzare i tuoi identificatori personalizzati utilizzando [!DNL Facebook Pixel]. Consulta la sezione [Documentazione ufficiale di facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) per informazioni dettagliate.

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Il video seguente illustra anche i passaggi per configurare un [!DNL Facebook] destinazione e attivazione dei segmenti.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L&#39;interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione di questo video. Per informazioni aggiornate, consulta la sezione [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: le [!DNL Facebook Ad Account ID]. Puoi trovare questo ID nel tuo [!DNL Facebook Ads Manager] conto. Quando immetti questo ID, devi sempre prescriverlo con `act_`.

## Attiva i segmenti in questa destinazione {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origine del pubblico"
>abstract="Scegli come sono stati raccolti i dati cliente nel segmento. I dati verranno visualizzati in Facebook quando un utente è oggetto di targeting da parte del segmento"
>additional-url="http://www.adobe.com/go/destinations-facebook-activate-section-en" text="Ulteriori informazioni nella documentazione"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Origine del pubblico"
>abstract="Gli inserzionisti raccolgono i dati direttamente dai clienti."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Origine del pubblico"
>abstract="Gli inserzionisti raccolgono i dati direttamente dai loro partner."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Origine del pubblico"
>abstract="Gli inserzionisti raccolgono i dati direttamente dai loro clienti e partner."

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

In **[!UICONTROL Pianificazione del segmento]** devi fornire [!UICONTROL Origine del pubblico] quando si inviano segmenti a [!DNL Facebook Custom Audiences].

![Origine del pubblico in facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Esempio di mappatura: attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience] {#example-facebook}

Di seguito è riportato un esempio di corretta mappatura dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience].

Selezione dei campi di origine:

* Seleziona la `Email` spazio dei nomi come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità sorgente se hai hashing gli indirizzi e-mail dei clienti all’inserimento di dati in [!DNL Platform], secondo [!DNL Facebook] [requisiti di hashing e-mail](#email-hashing-requirements).
* Seleziona la `PHONE_E.164` spazio dei nomi come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per rispettare [!DNL Facebook] requisiti.
* Seleziona la `Phone_SHA256` spazio dei nomi come identità sorgente se durante l’inserimento dei dati i numeri di telefono sono stati hashing in [!DNL Platform], secondo [!DNL Facebook] [requisiti di hashing del numero di telefono](#phone-number-hashing-requirements).
* Seleziona la `IDFA` spazio dei nomi come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona la `GAID` spazio dei nomi come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona la `Custom` spazio dei nomi come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Seleziona la `Phone_SHA256` spazio dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Seleziona la `IDFA` o `GAID` spazi dei nomi come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona la `Extern_ID` spazio dei nomi come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

>[!IMPORTANT]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] all&#39;attivazione.
> 
>I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione.

![Mappatura identità](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Dati esportati {#exported-data}

Per [!DNL Facebook], un&#39;attivazione riuscita significa che un [!DNL Facebook] il pubblico personalizzato viene creato a livello di programmazione in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’appartenenza al segmento nel pubblico verrà aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>Integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta i backfills dello storico del pubblico. Tutte le qualifiche dei segmenti storici vengono inviate a [!DNL Facebook] quando attivi i segmenti sulla destinazione.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potresti ricevere il seguente errore:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando i clienti utilizzano account appena creati e [!DNL Facebook] le autorizzazioni non sono ancora attive.

Se ricevi `400 Bad Request` messaggio di errore dopo aver seguito i passaggi in [Prerequisiti per l’account facebook](#facebook-account-prerequisites), per favore, consenti alcuni giorni per il [!DNL Facebook] i permessi per entrare in vigore.
