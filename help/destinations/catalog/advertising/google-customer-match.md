---
keywords: Google customer match;Google customer match;Google Customer Match
title: Connessione Customer Match di Google
description: Customer Match di Google consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti su proprietà possedute e gestite da Google, come ad esempio Search, Shopping, Gmail e YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 1%

---

# [!DNL Google Customer Match] connection

## Panoramica {#overview}

[Customer Match di Google](https://support.google.com/google-ads/answer/6379332?hl=en) consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti su proprietà possedute e gestite da Google, ad esempio: [!DNL Search], [!DNL Shopping], [!DNL Gmail]e [!DNL YouTube].

![Destinazione Customer Match di Google nell’interfaccia utente di Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Google Customer Match] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

### Caso d&#39;uso n. 1

Un marchio di abbigliamento atletico vuole raggiungere i clienti esistenti attraverso [!DNL Google Search] e [!DNL Google Shopping] personalizzare offerte ed articoli in base ai loro acquisti e alla cronologia di navigazione precedenti. Il marchio dell’abbigliamento può acquisire indirizzi e-mail dal proprio CRM all’Experience Platform e creare segmenti dai propri dati offline. Quindi possono inviare questi segmenti a [!DNL Google Customer Match] da utilizzare in [!DNL Search] e [!DNL Shopping], ottimizzando le spese pubblicitarie.

### Caso d&#39;uso n. 2

Un&#39;importante azienda tecnologica ha lanciato un nuovo telefono. Per promuovere questo nuovo modello di telefono, stanno cercando di sensibilizzare i clienti sulle nuove caratteristiche e funzionalità del telefono ai clienti che possiedono i modelli precedenti dei loro telefoni.

Per promuovere il rilascio, caricano gli indirizzi e-mail dal loro database CRM in Experience Platform, utilizzando gli indirizzi e-mail come identificatori. I segmenti vengono creati in base ai clienti che possiedono modelli di telefono precedenti. Quindi i segmenti vengono inviati a [!DNL Google Customer Match], in modo che l&#39;azienda possa rivolgersi ai clienti attuali, ai clienti che possiedono modelli di telefono precedenti e a clienti simili su [!DNL YouTube].

## Governance dei dati per [!DNL Google Customer Match] destinazioni {#data-governance}

Alcune destinazioni in Experience Platform hanno determinate regole e obblighi per i dati inviati o ricevuti dalla piattaforma di destinazione. Sei responsabile di comprendere i limiti e gli obblighi dei tuoi dati e come li utilizzi in Adobe Experience Platform e nella piattaforma di destinazione. Adobe Experience Platform fornisce strumenti di governance dei dati per aiutarti a gestire alcuni di questi obblighi di utilizzo dei dati. [Ulteriori informazioni](../../../data-governance/labels/overview.md) informazioni sugli strumenti e sulle policy di governance dei dati.

## Identità supportate {#supported-identities}

[!DNL Google Customer Match] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256_e.164 | Numeri di telefono in formato E164, con hash con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizzare i namespace appropriati rispettivamente per il testo normale e i numeri di telefono con hash. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per gli indirizzi e-mail con testo normale e con hash. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| user_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi personalizzato. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono e altri) utilizzati nel [!DNL Google Customer Match] destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] prerequisiti dell’account {#google-account-prerequisites}

Prima di configurare un [!DNL Google Customer Match] destinazione in Experience Platform, assicurati di leggere e rispettare i criteri di Google per l&#39;utilizzo [!DNL Customer Match], descritti nella [Documentazione di supporto per Google](https://support.google.com/google-ads/answer/6299717).

Successivamente, assicurati che [!DNL Google] account configurato per un [!DNL Standard] o livello di autorizzazione superiore. Consulta la sezione [Documentazione di Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) per i dettagli.

### Elenco consentiti {#allowlist}

Prima di creare il [!DNL Google Customer Match] destinazione in Experience Platform, assicurati che [!DNL Google Ads] l&#39;account rispetta [Criteri di corrispondenza cliente Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

I clienti con account conformi vengono automaticamente inseriti nell’elenco Consentiti da Google.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Google] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, il pubblico è stato attivato in [!DNL Google Customer Match] può essere disattivato *distrutto* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

### Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Google Customer Match]:

* **Inserimento di numeri di telefono non elaborati**: è possibile inserire numeri di telefono non elaborati nel [!DNL E.164] in formato [!DNL Platform]e vengono automaticamente crittografati al momento dell’attivazione. Se scegli questa opzione, assicurati di inserire sempre i tuoi numeri di telefono non elaborati nel `Phone_E.164` spazio dei nomi.
* **Inserimento di numeri di telefono con hash**: è possibile pre-hash i numeri di telefono prima dell&#39;inserimento in [!DNL Platform]. Se scegli questa opzione, assicurati di inserire sempre i tuoi numeri di telefono con hash nel `PHONE_SHA256_E.164` spazio dei nomi.

>[!NOTE]
>
>Numeri di telefono acquisiti nel `Phone` Impossibile attivare lo spazio dei nomi in [!DNL Google Customer Match].

### Requisiti di hash e-mail {#hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare gli indirizzi e-mail in modo chiaro nell’Experience Platform e avere [!DNL Platform] hashing su attivazione.

Per ulteriori informazioni sui requisiti di hashing di Google e su altre restrizioni all’attivazione, consulta le sezioni seguenti nella documentazione di Google:

* [[!DNL Customer Match] con indirizzo e-mail, indirizzo o ID utente](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerazioni](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Customer Match con numero di telefono](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Corrispondenza cliente con ID dispositivo mobile](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione in batch](../../../ingestion/batch-ingestion/overview.md) e [panoramica sull’acquisizione in streaming](../../../ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere direttamente l’hash agli indirizzi e-mail, assicurati di soddisfare i requisiti Google, descritti nei collegamenti di cui sopra.

### Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare il `User_ID` spazio dei nomi per inviare dati a Google, assicurati di sincronizzare i tuoi identificatori utilizzando [!DNL gTag]. Fai riferimento a [Documentazione ufficiale di Google](https://support.google.com/google-ads/answer/9199250) per informazioni dettagliate.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: specificare un nome per la connessione di destinazione
* **[!UICONTROL Descrizione]**: fornire una descrizione per la connessione di destinazione
* **[!UICONTROL ID account]**: il tuo ID cliente Google. Il formato dell&#39;ID è xxx-xxx-xxxx.

>[!IMPORTANT]
>
> * La **[!UICONTROL Combinare con PII]** l’azione di marketing è selezionata per impostazione predefinita per [!DNL Google Customer Match] destinazione e non può essere rimossa.


## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

In **[!UICONTROL Pianificazione del segmento]** devi fornire [!UICONTROL ID app] durante l’invio [!DNL IDFA] o [!DNL GAID] segmenti in [!DNL Google Customer Match].

![ID app Customer Match di Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Per informazioni dettagliate su come trovare il [!DNL App ID], fare riferimento alla [Documentazione ufficiale di Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Esempio di mappatura: attivazione dei dati sul pubblico in [!DNL Google Customer Match] {#example-gcm}

Questo è un esempio di mappatura corretta dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Google Customer Match].

Selezione dei campi di origine:

* Seleziona la `Email` spazio dei nomi come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità sorgente se hai hashing gli indirizzi e-mail dei clienti all’inserimento di dati in [!DNL Platform], secondo [!DNL Google Customer Match] [requisiti di hashing e-mail](#hashing-requirements).
* Seleziona la `PHONE_E.164` spazio dei nomi come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per rispettare [!DNL Google Customer Match] requisiti.
* Seleziona la `Phone_SHA256_E.164` spazio dei nomi come identità sorgente se durante l’inserimento dei dati i numeri di telefono sono stati hashing in [!DNL Platform], secondo [!DNL Facebook] [requisiti di hashing del numero di telefono](#phone-number-hashing-requirements).
* Seleziona la `IDFA` spazio dei nomi come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona la `GAID` spazio dei nomi come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona la `Custom` spazio dei nomi come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Seleziona la `Phone_SHA256_E.164` spazio dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256_E.164`.
* Seleziona la `IDFA` o `GAID` spazi dei nomi come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona la `User_ID` spazio dei nomi come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

![Mappatura identità](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

I dati provenienti da spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] all&#39;attivazione.

I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione.

![Trasformazione mappatura identità](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verifica che l’attivazione del segmento sia avvenuta correttamente {#verify-activation}

Dopo aver completato il flusso di attivazione, passa alla **[!UICONTROL Google Ads]** conto. I segmenti attivati vengono visualizzati nel tuo account Google come elenchi di clienti. Tieni presente che a seconda della dimensione del segmento, alcuni tipi di pubblico non vengono compilati a meno che non vi siano più di 100 utenti attivi da servire.

Quando mappi un segmento a entrambi [!DNL IDFA] e [!DNL GAID] ID mobili, [!DNL Google Customer Match] crea un segmento separato per ogni mappatura ID. Le [!DNL Google Ads] l&#39;account mostra due segmenti diversi, uno per il [!DNL IDFA]e uno per il [!DNL GAID] mappatura.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potresti ricevere il seguente errore:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi alla [prerequisiti](#google-account-prerequisites). Per risolvere il problema, contatta Google e assicurati che il tuo account sia inserito nell’elenco Consentiti e sia configurato per un [!DNL Standard] o livello di autorizzazione superiore. Consulta la sezione [Documentazione di Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) per i dettagli.

## Risorse aggiuntive {#additional-resources}

* [Integrare Customer Match di Google - Esercitazione video](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

