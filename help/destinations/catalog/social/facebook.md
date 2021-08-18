---
keywords: Connessione facebook;connessione facebook;destinazioni facebook;facebook;instagram;messenger;messenger facebook messenger
title: Connessione facebook
description: Attiva profili per le campagne Facebook per il targeting del pubblico, la personalizzazione e la soppressione in base a e-mail con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 183aff5a3b6bcc1635ae7b4b0e503a9d4b6d4d31
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 1%

---

# [!DNL Facebook] connection

## Panoramica {#overview}

Attiva profili per le campagne [!DNL Facebook] per il targeting del pubblico, la personalizzazione e la soppressione in base a e-mail con hash.

Puoi utilizzare questa destinazione per il targeting del pubblico tra [!DNL Facebook’s] la famiglia di app supportate da [!DNL Custom Audiences], inclusi [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. La selezione dell’app su cui desideri eseguire la campagna è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

![Destinazione facebook nell’interfaccia utente Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Facebook], ecco due esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

### Caso d&#39;uso n. 1

Un rivenditore online vuole raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate in base ai loro ordini precedenti. Il rivenditore online può acquisire indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti alla piattaforma social [!DNL Facebook] ottimizzando le spese pubblicitarie.

### Caso d&#39;uso n. 2

Una compagnia aerea ha diversi livelli di clienti (Bronze, Silver e Gold) e vuole fornire a ciascuno dei livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l’app mobile della compagnia aerea e alcuni di essi non hanno effettuato l’accesso al sito web della società. Gli unici identificatori che l&#39;azienda ha di questi clienti sono gli ID di iscrizione e gli indirizzi e-mail.

Per eseguire il targeting su tali utenti attraverso i social media, possono integrare i dati del cliente dal CRM in Adobe Experience Platform, utilizzando gli indirizzi e-mail come identificatori.

Successivamente, possono utilizzare i propri dati offline, inclusi gli ID di appartenenza associati e i livelli di cliente, per creare nuovi segmenti di pubblico di cui possono eseguire il targeting attraverso la destinazione [!DNL Facebook].

## Identità supportate {#supported-identities}

[!DNL Facebook Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256 | Hash dei numeri di telefono con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per il testo normale e i numeri di telefono con hash. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per gli indirizzi e-mail in testo normale e con hash. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi personalizzato. |

## Tipo di esportazione {#export-type}

**Esportazione segmento** : esporta tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Facebook.

## Prerequisiti per l’account facebook {#facebook-account-prerequisites}

Prima di poter inviare i segmenti di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* L&#39;account utente [!DNL Facebook] deve disporre dell&#39;autorizzazione **[!DNL Manage campaigns]** abilitata per l&#39;account annuncio che intendi utilizzare.
* L&#39;account aziendale **Adobe Experience Cloud** deve essere aggiunto come partner pubblicitario nel [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Per ulteriori informazioni, consulta [Aggiungi partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook .
   >[!IMPORTANT]
   >
   > Quando configuri le autorizzazioni per Adobe Experience Cloud, devi abilitare l&#39;autorizzazione **Gestisci campagne**. L&#39;autorizzazione è necessaria per l&#39;integrazione [!DNL Adobe Experience Platform].
* Leggi e firma i termini del servizio [!DNL Facebook Custom Audiences]. Per farlo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Facebook] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Facebook] possono essere contrassegnati da identificatori *con hash* come indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

## Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Facebook]:

* **Inserimento di numeri** di telefono non elaborati: è possibile inserire numeri di telefono non elaborati nel  [!DNL E.164] formato in  [!DNL Platform]. Hanno automaticamente eseguito l’hash al momento dell’attivazione. Se scegli questa opzione, accertati di inserire sempre i numeri di telefono non elaborati nello spazio dei nomi `Phone_E.164` .
* **Inserimento di numeri** di telefono con hash: è possibile pre-hash i numeri di telefono prima dell’inserimento in  [!DNL Platform]. Se scegli questa opzione, accertati di inserire sempre i numeri di telefono con hash nello spazio dei nomi `Phone_SHA256` .

>[!NOTE]
>
>I numeri di telefono acquisiti nello spazio dei nomi `Phone` non possono essere attivati in [!DNL Facebook].


## Requisiti di hash e-mail {#email-hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare indirizzi e-mail in modo chiaro nell’Experience Platform e inserirli [!DNL Platform] all’attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere con hash gli indirizzi e-mail, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail; esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di utilizzare l’hash della stringa in minuscolo;
   * Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutto minuscola
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non saldare la stringa.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.
> I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.
> L&#39;opzione **[!UICONTROL Applica trasformazione]** viene visualizzata solo quando selezioni gli attributi come campi di origine. Non viene visualizzato quando si selezionano i namespace.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare lo spazio dei nomi `Extern_ID` per inviare dati a [!DNL Facebook], assicurati di sincronizzare i tuoi identificatori utilizzando [!DNL Facebook Pixel]. Per informazioni dettagliate, consulta la [documentazione ufficiale di Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) .

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

Il video seguente illustra anche i passaggi per configurare una destinazione [!DNL Facebook] e attivare i segmenti.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L&#39;interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione di questo video. Per informazioni aggiornate, consulta l’ [esercitazione sulla configurazione di destinazione](../../ui/connect-destination.md) .

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** account: il tuo  [!DNL Facebook Ad Account ID]. Puoi trovare questo ID nel tuo account [!DNL Facebook Ads Manager] . Quando immetti questo ID, devi sempre prescriverlo con `act_`.

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

Nel passaggio **[!UICONTROL Pianificazione segmento]** , devi fornire l’ [!UICONTROL Origine del pubblico] quando invii segmenti a [!DNL Facebook Custom Audiences].

![Origine del pubblico in facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Esempio di mappatura: attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience] {#example-facebook}

Di seguito è riportato un esempio di mappatura corretta dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience].

Selezione dei campi di origine:

* Seleziona lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se hai hashing gli indirizzi e-mail dei clienti durante l’inserimento dei dati in [!DNL Platform], in base a [!DNL Facebook] [requisiti di hashing e-mail](#email-hashing-requirements).
* Seleziona lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per conformarsi ai  [!DNL Facebook] requisiti.
* Seleziona lo spazio dei nomi `Phone_SHA256` come identità di origine se hai hashing i numeri di telefono durante l’inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing del numero di telefono](#phone-number-hashing-requirements).
* Seleziona lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona lo spazio dei nomi `Custom` come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Selezionare i namespace `IDFA` o `GAID` come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona lo spazio dei nomi `Extern_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

>[!IMPORTANT]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.
> 
>I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.

![Mappatura identità](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Dati esportati {#exported-data}

Per [!DNL Facebook], una corretta attivazione implica la creazione programmatica di un pubblico personalizzato [!DNL Facebook] in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/) a livello di programmazione. L’appartenenza al segmento nel pubblico verrà aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L’integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta le versioni precedenti del pubblico. Tutte le qualifiche dei segmenti storici vengono inviate a [!DNL Facebook] quando attivi i segmenti nella destinazione.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Quando attivi i segmenti su [!DNL Facebook], potresti ricevere il seguente errore:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando i clienti utilizzano account appena creati e le autorizzazioni [!DNL Facebook] non sono ancora attive.

Se ricevi il messaggio di errore `400 Bad Request` dopo aver seguito i passaggi descritti in [Prerequisiti per l’account Facebook](#facebook-account-prerequisites), ti preghiamo di concedere alcuni giorni per l’entrata in vigore delle autorizzazioni [!DNL Facebook] .